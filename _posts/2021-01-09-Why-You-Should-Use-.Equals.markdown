---
title:  "Why You Should Use .Equals in C#"
date:   2021-01-09 11:13:48 +0100
categories: C# Equality
tags: C# Equals == IEquatable
---

## The Problem
By default, up to now I always used <code>==</code> to compare Objects and ValueTypes in C#. But this has led to some serious issues in my last project.

While I was well aware of the fact that this does an equality check on the reference in case of objects (when not overloaded) and a comparison of values in case of most ValueTypes[^1], I didn't foresee that the unreflected usage of <code>==</code> would cause a quite exhaustive round of refactoring in my project.

To be able to better explain the problem, let's first create a setting. Let's assume we have a class <code>Product</code> that implements an <code>IProduct</code> interface.

~~~c#
public class Product : IProduct
{
    public string Id { get; set; }
    public double Price { get; set; }
}
~~~

~~~c#
public interface IProduct
{
    string Id { get; }
    double Price { get; set; }
}
~~~

Now instances of <code>Product</code> are passed around your application as <code>IProduct</code>, ensuring that the Id property is not changed. Now you could have another class like

~~~csharp 
public class ProductCatalogue
{
    public IProduct SelectedProduct { get; set; }

    public bool IsProductSelected(IProduct product)
    {
        return SelectedProduct == product;
    }
}
~~~

By default, the code in <code>IsProductSelected</code> will perform a check on reference equality[^2]. But the catch is, since we compare interfaces and not the implementations, **we have no means of overloading the operator**. Why is that a problem? In my case it turned out after some significant development time that the default equality check for the class <code>Product</code> should no longer be a check upon the reference but a check if the Id property coincides.

## Some Objects Are More .Equals Than Others
A more future-proof way of performing equality checks on objects is to use the [Equals](https://docs.microsoft.com/de-de/dotnet/api/system.object.equals?view=net-5.0) method or the [ReferenceEquals](https://docs.microsoft.com/de-de/dotnet/api/system.object.referenceequals?view=net-5.0) method if you are sure that you will only want to compare references. Using these methods has two advantages:

1. They make the intent very clear. <code>ReferenceEquals</code> tells any fellow developer that the author thought about it and was reasonably sure that he/she needed to do a comparison of references. <code>Equals</code> signals that there may be a comparison of values going on.
2. The <code>Equals</code> method may be overriden[^3] and the overriden comparison will also be used when comparing implementations as their common interface. Thus, you can later on change your mind about how you want to compare two objects without having to refactor maybe hundreds of lines of code.

Let's see this in action. Using the [automatically generated implementation](https://docs.microsoft.com/de-de/visualstudio/ide/reference/generate-equals-gethashcode-methods?view=vs-2019) for our <code>Product</code> class we get the following code:

~~~c#
public class Product : IProduct
{
    public string Id { get; set; }
    public double Price { get; set; }

    public override bool Equals(object obj)
    {
        return obj is Product product &&
                Id == product.Id;
    }

    public override int GetHashCode()
    {
        return HashCode.Combine(Id);
    }
}
~~~

Now the Equals method returns true for two instances of the <code>Product</code> class, if their Id coincides. Moreover, Equals still works as expected when used with <code>IProduct</code> Objects. Note that Lists, Dictionaries etc. and many LINQ methods also essentially use <code>Equals</code> when comparing entries. As an example you cannot have two different Product instances with the same Id as Keys in a Dictionary.

~~~c#
IProduct product1 = new Product { Id = "test" };
IProduct product2 = new Product { Id = "test" };

Console.WriteLine(product1 == product2); //Output: false
Console.WriteLine(product1.Equals(product2)); //Output: true 

Dictionary<IProduct, int> dict = new Dictionary<IProduct, int> 
{ 
    { product1, 1 } 
};
dict[product2] = 2;
Console.WriteLine(dict[product1]); //Output: 2
~~~

To emphasize on that again: We cannot change the behaviour of == when cmparing <code>product1</code> and <code>product2</code>, it's a public static operator defined for <code>Object</code>. But by overriding Equals we may achieve to compare two interfaces based on values.

In order to implement the requested behaviour into our ProductCatalogue from above, we simply change it to
~~~c#
public class ProductCatalogue
{
    public IProduct SelectedProduct { get; set; }

    public bool IsProductSelected(IProduct product)
    {
        return SelectedProduct?.Equals(product) ?? false;
    }
}
~~~

Here we use the null-conditional operator to make sure that no exception is thrown when <code>SelectedProduct</code> is <code>null</code>. Of course there are also scenarios where you would **want** that to throw an exception.

## A Word About IEquatable&lt;T&gt;
If you are new to an existing codebase, it can be quite cumbersome to distinguish whether an <code>Equals</code> check compares references or values. To make the intent clearer I definitely recommend also implementing <code>IEquatable&lt;T&gt;</code> whenever you override <code>Equals</code>. You will also gain a slight performance increase in [some situations](https://stackoverflow.com/a/19241925).
Again using the Visual Studio generated methods we end up with 

~~~c#
public class Product : IProduct, IEquatable<Product>
{
    public string Id { get; set; }
    public double Price { get; set; }

    public override bool Equals(object obj)
    {
        return Equals(obj as Product);
    }

    public virtual bool Equals(Product other)
    {
        return other != null &&
                Id == other.Id;
    }

    public override int GetHashCode()
    {
        return HashCode.Combine(Id);
    }
}
~~~

It is best practice to either mark <code>Product</code> as sealed or the<code>Equals</code> method as virtual. The background is that if you don't do that, possible derived classes will default to use the comparison of their base class. Thus instances of two entirely different classes may be considered as equal and you probably don't want that. See also this [SonarSource Rule](https://rules.sonarsource.com/csharp/RSPEC-4035).

## Footnotes
[^1]: Like <code>int, double, char</code> and also <code>string</code> albeit it's not a ValueType.
[^2]: In Production Code you would probably like to have a null check in your public methods accepting references.
[^3]: See the [guidelines](https://docs.microsoft.com/en-us/previous-versions/ms173147(v=vs.90)?redirectedfrom=MSDN) for overwriting <code>Equals()</code> when you decide to do so.