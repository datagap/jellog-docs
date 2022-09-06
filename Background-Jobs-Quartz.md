# Quartz Background Job Manager

[Quartz](https://www.quartz-scheduler.net/) is an advanced background job manager. You can integrate Quartz with the JELLOG Framework to use it instead of the [default background job manager](Background-Jobs.md). In this way, you can use the same background job API for Quartz and your code will be independent of Quartz. If you like, you can directly use Quartz's API, too.

> See the [background jobs document](Background-Jobs.md) to learn how to use the background job system. This document only shows how to install and configure the Quartz integration.

## Installation

It is suggested to use the [JELLOG CLI](CLI.md) to install this package.

### Using the JELLOG CLI

Open a command line window in the folder of the project (.csproj file) and type the following command:

````bash
jellog add-package DataGap.Jellog.BackgroundJobs.Quartz
````

### Manual Installation

If you want to manually install;

1. Add the [DataGap.Jellog.BackgroundJobs.Quartz](https://www.nuget.org/packages/DataGap.Jellog.BackgroundJobs.Quartz) NuGet package to your project:

   ````
   Install-Package DataGap.Jellog.BackgroundJobs.Quartz
   ````

2. Add the `JellogBackgroundJobsQuartzModule` to the dependency list of your module:

````csharp
[DependsOn(
    //...other dependencies
    typeof(JellogBackgroundJobsQuartzModule) //Add the new module dependency
    )]
public class YourModule : JellogModule
{
}
````

## Configuration

Quartz is a very configurable library,and the JELLOG framework provides `JellogQuartzOptions` for this. You can use the `PreConfigure` method in your module class to pre-configure this option. JELLOG will use it when initializing the Quartz module. For example:

````csharp
[DependsOn(
    //...other dependencies
    typeof(JellogBackgroundJobsQuartzModule) //Add the new module dependency
    )]
public class YourModule : JellogModule
{
    public override void PreConfigureServices(ServiceConfigurationContext context)
    {
        var configuration = context.Services.GetConfiguration();

        PreConfigure<JellogQuartzOptions>(options =>
        {
            options.Properties = new NameValueCollection
            {
                ["quartz.jobStore.dataSource"] = "BackgroundJobsDemoApp",
                ["quartz.jobStore.type"] = "Quartz.Impl.AdoJobStore.JobStoreTX, Quartz",
                ["quartz.jobStore.tablePrefix"] = "QRTZ_",
                ["quartz.serializer.type"] = "json",
                ["quartz.dataSource.BackgroundJobsDemoApp.connectionString"] = configuration.GetConnectionString("Quartz"),
                ["quartz.dataSource.BackgroundJobsDemoApp.provider"] = "SqlServer",
                ["quartz.jobStore.driverDelegateType"] = "Quartz.Impl.AdoJobStore.SqlServerDelegate, Quartz",
            };
        });
    }
}
````

Starting from JELLOG 3.1 version, we have added `Configurator` to `JellogQuartzOptions` to configure Quartz. For example:

````csharp
[DependsOn(
    //...other dependencies
    typeof(JellogBackgroundJobsQuartzModule) //Add the new module dependency
    )]
public class YourModule : JellogModule
{
    public override void PreConfigureServices(ServiceConfigurationContext context)
    {
        var configuration = context.Services.GetConfiguration();

        PreConfigure<JellogQuartzOptions>(options =>
        {
            options.Configurator = configure =>
            {
                configure.UsePersistentStore(storeOptions =>
                {
                    storeOptions.UseProperties = true;
                    storeOptions.UseJsonSerializer();
                    storeOptions.UseSqlServer(configuration.GetConnectionString("Quartz"));
                    storeOptions.UseClustering(c =>
                    {
                        c.CheckinMisfireThreshold = TimeSpan.FromSeconds(20);
                        c.CheckinInterval = TimeSpan.FromSeconds(10);
                    });
                });
            };
        });
    }
}
````

> You can choose the way you favorite to configure Quaratz.

Quartz stores job and scheduling information **in memory by default**. In the example, we use the pre-configuration of [options pattern](Options.md) to change it to the database. For more configuration of Quartz, please refer to the Quartz's [documentation](https://www.quartz-scheduler.net/).

## Exception handling

### Default exception handling strategy

When an exception occurs in the background job,JELLOG provide the **default handling strategy** retrying once every 3 seconds, up to 3 times. You can change the retry count and retry interval via `JellogBackgroundJobQuartzOptions` options:

```csharp
[DependsOn(
    //...other dependencies
    typeof(JellogBackgroundJobsQuartzModule) //Add the new module dependency
    )]
public class YourModule : JellogModule
{
    public override void ConfigureServices(ServiceConfigurationContext context)
    {
        Configure<JellogBackgroundJobQuartzOptions>(options =>
        {
            options.RetryCount = 1;
            options.RetryIntervalMillisecond = 1000;
        });
    }
}
```

### Customize exception handling strategy

You can customize the exception handling strategy via `JellogBackgroundJobQuartzOptions` options:

```csharp
[DependsOn(
    //...other dependencies
    typeof(JellogBackgroundJobsQuartzModule) //Add the new module dependency
    )]
public class YourModule : JellogModule
{
    public override void ConfigureServices(ServiceConfigurationContext context)
    {
        Configure<JellogBackgroundJobQuartzOptions>(options =>
        {
            options.RetryStrategy = async (retryIndex, executionContext, exception) =>
            {
                // customize exception handling
            };
        });
    }
}
```