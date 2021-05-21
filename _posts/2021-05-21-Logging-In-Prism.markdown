---
title:  "How To Register Logging in a Prism 8 WPF App"
date:   2021-05-21 11:13:48 +0100
categories: PRISM WPF Logging
tags: prism wpf logging dryioc unity serilog nlog
---
Logging is an essential part of almost every application. However, when writing a PRISM app for WPF, it's hard to find documentation on how to exactly register logging with your IoC Container. In this post we will add logging (using Serilog and Microsoft Logging Abstractions) to either DryIoC or Unity. This approach will work from PRISM 7 upwards.

## Necessary Nuget Packages
You first have to add the following NuGet packages to your startup project (the one containing App.xaml and App.xaml.cs):

* [Microsoft Logging Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/) 
* [Microsoft Extensions DependencyInjection](https://www.nuget.org/packages/Microsoft.Extensions.DependencyInjection) You need this to make use of the IServiceCollection, which facilitates the Logger-Registration.

Also you need packages for your logging framework of choice, we will use Serilog in this example, so include

* [Serilog Extensions Logging](https://www.nuget.org/packages/Serilog.Extensions.Logging/)

However you can easily replace this with nLog or any other logging framework.

And in order to add the IServiceCollection to your IOC Container you need
* [DryIoc.Microsoft.DependencyInjection](https://www.nuget.org/packages/DryIoc.Microsoft.DependencyInjection) for DryIoc or
* [Unity.Microsoft.DependencyInjection](https://www.nuget.org/packages/Unity.Microsoft.DependencyInjection) for Unity.

## Registering Logging with the Container
To register the logging framework with the IoC Container, add the following override to the App.xaml.cs and import all relevant usings from the previously added nuget packages:

### DryIoC
~~~c#
protected override IContainerExtension CreateContainerExtension()
{
    var serviceCollection = new ServiceCollection();
    serviceCollection.AddLogging(loggingBuilder =>
        loggingBuilder.AddSerilog(dispose: true));

    return new DryIocContainerExtension(new Container(CreateContainerRules())
        .WithDependencyInjectionAdapter(serviceCollection));
}
~~~
Here we first create the ServiceCollection which makes it incredibly easy to add logging,by calling... <code>AddLogging()</code>! This is also the place to add another Logging Framework if you prefer nlog or log4net or setup the minimal logging level etc.

Then we have to make sure that the services registered with the ServiceCollection are also registered in the DryIoC Container used in the rest of the application. For this we use the <code>WithDependencyInjectionAdapter</code> extension method, found in DryIoc.Microsoft.DependencyInjection .

### Unity
~~~c#
protected override IContainerExtension CreateContainerExtension()
{
    var serviceCollection = new ServiceCollection();
    serviceCollection.AddLogging(loggingBuilder =>
        loggingBuilder.AddSerilog(dispose: true));

    var container = new UnityContainer();
    container.BuildServiceProvider(serviceCollection);

    return new UnityContainerExtension(container);
}
~~~
The code is almost the same as in the DryIoC case, but Unity.Microsoft.DependencyInjection works slighlty different, thus you have to call <code>BuildServiceProvider</code>.

## Configuring the Logger
Configure the logger before the Shell is created, by e.g. adding the following code to <code>CreateShell</code>:
~~~c#
protected override Window CreateShell()
{
    Log.Logger = new LoggerConfiguration()
        .Enrich.FromLogContext()
        .WriteTo.Debug()
        .CreateLogger();

    return Container.Resolve<MainWindow>();
}
~~~
This is just a basic configuration, more info can be found on the [project page](https://serilog.net/). In order to be able to use Debug as a sink you need [Serilog.Sinks.Debug](https://www.nuget.org/packages/Serilog.Sinks.Debug/).

## Using the logger
In your services you can now inject the generic <code>ILogger</code>, e.g.
~~~c#
public class MyService : IMyService
{
    public MyService(ILogger<MyService> logger)
    {
        logger.LogInformation("Hello World from your logger!");
    }
}
~~~

Happy Logging!