# Distributed Event Bus Rebus Integration

> This document explains **how to configure the [Rebus](http://mookid.dk/category/rebus/)** as the distributed event bus provider. See the [distributed event bus document](Distributed-Event-Bus.md) to learn how to use the distributed event bus system

## Installation

Use the JELLOG CLI to add [DataGap.Jellog.EventBus.Rebus](https://www.nuget.org/packages/DataGap.Jellog.EventBus.Rebus) NuGet package to your project:

* Install the [JELLOG CLI](https://docs.jellog.io/en/jellog/latest/CLI) if you haven't installed before.
* Open a command line (terminal) in the directory of the `.csproj` file you want to add the `DataGap.Jellog.EventBus.Rebus` package.
* Run `jellog add-package DataGap.Jellog.EventBus.Rebus` command.

If you want to do it manually, install the [DataGap.Jellog.EventBus.Rebus](https://www.nuget.org/packages/DataGap.Jellog.EventBus.Rebus) NuGet package to your project and add `[DependsOn(typeof(JellogEventBusRebusModule))]` to the [JELLOG module](Module-Development-Basics.md) class inside your project.

## Configuration

You can configure using the standard [configuration system](Configuration.md), like using the [options](Options.md) classes.

### The Options Classes

`JellogRebusEventBusOptions` classe can be used to configure the event bus options for the Rebus.

You can configure this options inside the `PreConfigureServices` of your [module](Module-Development-Basics.md).

**Example: Minimize configuration**

```csharp
PreConfigure<JellogRebusEventBusOptions>(options =>
{
    options.InputQueueName = "eventbus";
});
```

Rebus has many options, you can use the `Configurer` property of `JellogRebusEventBusOptions` class to configure.

Default events are **stored in memory**. See the [rebus document](https://github.com/rebus-org/Rebus/wiki/Transport) for more details.

**Example: Configure the store**

````csharp
PreConfigure<JellogRebusEventBusOptions>(options =>
{
    options.InputQueueName = "eventbus";
    options.Configurer = rebusConfigurer =>
    {
        rebusConfigurer.Transport(t => t.UseMsmq("eventbus"));
        rebusConfigurer.Subscriptions(s => s.UseJsonFile(@"subscriptions.json"));
    };
});
````

You can use the `Publish` properpty of `JellogRebusEventBusOptions` class to change the publishing method

**Example: Configure the event publishing**

````csharp
PreConfigure<JellogRebusEventBusOptions>(options =>
{
    options.InputQueueName = "eventbus";
    options.Publish = async (bus, type, data) =>
    {
        await bus.Publish(data);
    };
});
````
