---
title:  "Why You Should Use .Equals (Instead Of ==)"
date:   2021-01-09 11:13:48 +0100
categories: C# Equality
tags: C# Equals == IEquatable
---

## The Problem

By default, up to now I always used <code>==</code> to compare Objects and ValueTypes in C#. While I was well aware of the fact that this does an equality check on the reference in case of objects (when not overloaded) and a comparison of values in case of most ValueTypes (like <code>int, double, char</code> and also <code>string</code> albeit it's not a ValueTyp
e)

{% highlight ruby %} def print_hi(name) puts "Hi, #{name}" end print_hi('Tom') #=> prints 'Hi, Tom' to STDOUT. {% endhighlight %}

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit.

## Some great heading (h2)

Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu.

Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris. Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc. Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

## Another great heading (h2)

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit.

### Some great subheading (h3)

Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum.

Phasellus et hendrerit mauris. Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc.

### Some great subheading (h3)

Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

> This quote will *change* your life. It will reveal the <i>secrets</i> of the universe, and all the wonders of humanity. Don't <em>misuse</em> it.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt.

### Some great subheading (h3)

Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit. Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum.

```html
<html>
  <head>
  </head>
  <body>
    <p>Hello, World!</p>
  </body>
</html>
```


In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

#### You might want a sub-subheading (h4)

In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

#### But it's probably overkill (h4)

In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

##### Could be a smaller sub-heading, `pacman` (h5)

In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

###### Small yet significant sub-heading  (h6)

In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

### Oh hai, an unordered list!!

In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

- First item, yo
- Second item, dawg
- Third item, what what?!
- Fourth item, fo sheezy my neezy

### Oh hai, an ordered list!!

In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris.

1. First item, yo
2. Second item, dawg
3. Third item, what what?!
4. Fourth item, fo sheezy my neezy



## Headings are cool! (h2)

Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc. Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc.

### Tables

Title 1               | Title 2               | Title 3               | Title 4
--------------------- | --------------------- | --------------------- | ---------------------
lorem                 | lorem ipsum           | lorem ipsum dolor     | lorem ipsum dolor sit
lorem ipsum dolor sit | lorem ipsum dolor sit | lorem ipsum dolor sit | lorem ipsum dolor sit
lorem ipsum dolor sit | lorem ipsum dolor sit | lorem ipsum dolor sit | lorem ipsum dolor sit
lorem ipsum dolor sit | lorem ipsum dolor sit | lorem ipsum dolor sit | lorem ipsum dolor sit


Title 1 | Title 2 | Title 3 | Title 4
--- | --- | --- | ---
lorem | lorem ipsum | lorem ipsum dolor | lorem ipsum dolor sit
lorem ipsum dolor sit amet | lorem ipsum dolor sit amet consectetur | lorem ipsum dolor sit amet | lorem ipsum dolor sit
lorem ipsum dolor | lorem ipsum | lorem | lorem ipsum
lorem ipsum dolor | lorem ipsum dolor sit | lorem ipsum dolor sit amet | lorem ipsum dolor sit amet consectetur


---
layout: post
title: Example content
---

**Howdy!** This is an example blog post that shows several types of HTML content supported in this theme.
{: .message }

Cum sociis natoque penatibus et magnis <a href="#">dis parturient montes</a>, nascetur ridiculus mus. *Aenean eu leo quam.* Pellentesque ornare sem lacinia quam venenatis vestibulum. Sed posuere consectetur est at lobortis. Cras mattis consectetur purus sit amet fermentum.

> Curabitur blandit tempus porttitor. Nullam quis risus eget urna mollis ornare vel eu leo. Nullam id dolor id nibh ultricies vehicula ut id elit.

Etiam porta **sem malesuada magna** mollis euismod. Cras mattis consectetur purus sit amet fermentum. Aenean lacinia bibendum nulla sed consectetur.

## Inline HTML elements

HTML defines a long list of available inline tags, a complete list of which can be found on the [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

- **To bold text**, use `<strong>`.
- *To italicize text*, use `<em>`.
- <mark>To highlight</mark>, use `<mark>`.
- Abbreviations, like <abbr title="HyperText Markup Langage">HTML</abbr> should use `<abbr>`, with an optional `title` attribute for the full phrase.
- Citations, like <cite>&mdash; Mark Otto</cite>, should use `<cite>`.
- <del>Deleted</del> text should use `<del>` and <ins>inserted</ins> text should use `<ins>`.
- Superscript <sup>text</sup> uses `<sup>` and subscript <sub>text</sub> uses `<sub>`.

Most of these elements are styled by browsers with few modifications on our part.

## Footnotes

Footnotes are supported as part of the Markdown syntax. Here's one in action. Clicking this number[^fn-sample_footnote] will lead you to a footnote. The syntax looks like:

{% highlight text %}
Clicking this number[^fn-sample_footnote]
{% endhighlight %}

Each footnote needs the `^fn-` prefix and a unique ID to be referenced for the footnoted content. The syntax for that list looks something like this:

{% highlight text %}
[^fn-sample_footnote]: Handy! Now click the return link to go back.
{% endhighlight %}

You can place the footnoted content wherever you like. Markdown parsers should properly place it at the bottom of the post.

## Heading

Vivamus sagittis lacus vel augue rutrum faucibus dolor auctor. Duis mollis, est non commodo luctus, nisi erat porttitor ligula, eget lacinia odio sem nec elit. Morbi leo risus, porta ac consectetur ac, vestibulum at eros.

### Code

Inline code is available with the `<code>` element. Snippets of multiple lines of code are supported through Rouge. Longer lines will automatically scroll horizontally when needed. You may also use code fencing (triple backticks) for rendering code.

{% highlight js %}
// Example can be run directly in your JavaScript console

// Create a function that takes two arguments and returns the sum of those arguments
var adder = new Function("a", "b", "return a + b");

// Call the function
adder(2, 6);
// > 8
{% endhighlight %}

You may also optionally show code snippets with line numbers. Add `linenos` to the Rouge tags.

{% highlight js linenos %}
// Example can be run directly in your JavaScript console

// Create a function that takes two arguments and returns the sum of those arguments
var adder = new Function("a", "b", "return a + b");

// Call the function
adder(2, 6);
// > 8
{% endhighlight %}

Aenean lacinia bibendum nulla sed consectetur. Etiam porta sem malesuada magna mollis euismod. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa.

### Gists via GitHub Pages

Vestibulum id ligula porta felis euismod semper. Nullam quis risus eget urna mollis ornare vel eu leo. Donec sed odio dui.

{% gist 13f94b734a4ddb132735 gist.md %}

Aenean eu leo quam. Pellentesque ornare sem lacinia quam venenatis vestibulum. Nullam quis risus eget urna mollis ornare vel eu leo. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sed odio dui. Vestibulum id ligula porta felis euismod semper.

### Lists

Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Aenean lacinia bibendum nulla sed consectetur. Etiam porta sem malesuada magna mollis euismod. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus.

- Praesent commodo cursus magna, vel scelerisque nisl consectetur et.
- Donec id elit non mi porta gravida at eget metus.
- Nulla vitae elit libero, a pharetra augue.

Donec ullamcorper nulla non metus auctor fringilla. Nulla vitae elit libero, a pharetra augue.

1. Vestibulum id ligula porta felis euismod semper.
2. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.
3. Maecenas sed diam eget risus varius blandit sit amet non magna.

Cras mattis consectetur purus sit amet fermentum. Sed posuere consectetur est at lobortis.

<dl>
  <dt>HyperText Markup Language (HTML)</dt>
  <dd>The language used to describe and define the content of a Web page</dd>

  <dt>Cascading Style Sheets (CSS)</dt>
  <dd>Used to describe the appearance of Web content</dd>

  <dt>JavaScript (JS)</dt>
  <dd>The programming language used to build advanced Web sites and applications</dd>
</dl>

Integer posuere erat a ante venenatis dapibus posuere velit aliquet. Morbi leo risus, porta ac consectetur ac, vestibulum at eros. Nullam quis risus eget urna mollis ornare vel eu leo.

### Images

Quisque consequat sapien eget quam rhoncus, sit amet laoreet diam tempus. Aliquam aliquam metus erat, a pulvinar turpis suscipit at.

![placeholder](http://placehold.it/800x400 "Large example image")
![placeholder](http://placehold.it/400x200 "Medium example image")
![placeholder](http://placehold.it/200x200 "Small example image")

### Tables

Aenean lacinia bibendum nulla sed consectetur. Lorem ipsum dolor sit amet, consectetur adipiscing elit.

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Upvotes</th>
      <th>Downvotes</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>Totals</td>
      <td>21</td>
      <td>23</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <td>Bob</td>
      <td>4</td>
      <td>3</td>
    </tr>
    <tr>
      <td>Charlie</td>
      <td>7</td>
      <td>9</td>
    </tr>
  </tbody>
</table>

Nullam id dolor id nibh ultricies vehicula ut id elit. Sed posuere consectetur est at lobortis. Nullam quis risus eget urna mollis ornare vel eu leo.

-----

Want to see something else added? <a href="https://github.com/poole/poole/issues/new">Open an issue.</a>

[^fn-sample_footnote]: Handy! Now click the return link to go back.

