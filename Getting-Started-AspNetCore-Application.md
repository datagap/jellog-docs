# Getting Started With an JELLOG and AspNet Core MVC Web Application

This tutorial explains how to start JELLOG from scratch with minimal dependencies. You generally want to start with the **[startup template](Getting-Started-AspNetCore-MVC-Template.md)**.

## Create a New Project

1. Create a new AspNet Core Web Application with Visual Studio 2022 (17.0.0+):

![](images/create-new-aspnet-core-application-v2.png)

2. Configure your new project:

![](images/select-empty-web-application-v2.png)

3. Press the create button:

![create-aspnet-core-application](images/create-aspnet-core-application.png)

## Install DataGap.Jellog.AspNetCore.Mvc Package

DataGap.Jellog.AspNetCore.Mvc is the AspNet Core MVC integration package for JELLOG. So, install it on your project:

````
Install-Package DataGap.Jellog.AspNetCore.Mvc
````

## Create the First JELLOG Module

JELLOG is a modular framework and it requires a **startup (root) module** class derived from ``JellogModule``:

````C#
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.Hosting;
using DataGap.Jellog;
using DataGap.Jellog.AspNetCore.Mvc;
using DataGap.Jellog.Modularity;

namespace BasicAspNetCoreApplication
{
    [DependsOn(typeof(JellogAspNetCoreMvcModule))]
    public class AppModule : JellogModule
    {
        public override void OnApplicationInitialization(ApplicationInitializationContext context)
        {
            var app = context.GetApplicationBuilder();
            var env = context.GetEnvironment();

            // Configure the HTTP request pipeline.
            if (env.IsDevelopment())
            {
                app.UseExceptionHandler("/Error");
                // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
                app.UseHsts();
            }

            app.UseHttpsRedirection();
            app.UseStaticFiles();
            app.UseRouting();
            app.UseConfiguredEndpoints();
        }
    }
}
````

``AppModule`` is a good name for the startup module for an application.

JELLOG packages define module classes and a module can depend on another. In the code above, the ``AppModule`` depends on the ``JellogAspNetCoreMvcModule`` (defined by the [DataGap.Jellog.AspNetCore.Mvc](https://www.nuget.org/packages/DataGap.Jellog.AspNetCore.Mvc) package). It's common to add a ``DependsOn`` attribute after installing a new JELLOG NuGet package.

Instead of the Startup class, we are configuring an ASP.NET Core pipeline in this module class.

## The Program Class

Next step is to modify the Program class to integrate to the JELLOG module system:

````C#
using BasicAspNetCoreApplication;

var builder = WebApplication.CreateBuilder(args);

await builder.AddApplicationAsync<AppModule>();

var app = builder.Build();

await app.InitializeApplicationAsync();
await app.RunAsync();
````

``builder.AddApplicationAsync<AppModule>();`` adds all services defined in all modules starting from the ``AppModule``.

``app.InitializeApplicationAsync()`` initializes and starts the application.

## Run the Application!

That's all! Run the application, it will just work as expected.

## Using Autofac as the Dependency Injection Framework

While ASP.NET Core's Dependency Injection (DI) system is fine for basic requirements, [Autofac](https://autofac.org/) provides advanced features like Property Injection and Method Interception which are required by JELLOG to perform advanced application framework features.

Replacing ASP.NET Core's DI system by Autofac and integrating to JELLOG is pretty easy.

1. Install [DataGap.Jellog.Autofac](https://www.nuget.org/packages/DataGap.Jellog.Autofac) package

````
Install-Package DataGap.Jellog.Autofac
````

2. Add the ``JellogAutofacModule`` Dependency

````C#
[DependsOn(typeof(JellogAspNetCoreMvcModule))]
[DependsOn(typeof(JellogAutofacModule))] //Add dependency to JELLOG Autofac module
public class AppModule : JellogModule
{
    ...
}
````

3. Update `Program.cs` to use Autofac:

````C#
using BasicAspNetCoreApplication;

var builder = WebApplication.CreateBuilder(args);

builder.Host.UseAutofac();  //Add this line

await builder.AddApplicationAsync<AppModule>();

var app = builder.Build();

await app.InitializeApplicationAsync();
await app.RunAsync();
````

## Source Code

Get source code of the sample project created in this tutorial from [here](https://github.com/jellogframework/jellog-samples/tree/master/BasicAspNetCoreApplication).
