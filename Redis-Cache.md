# Redis Cache

JELLOG Framework [Caching System](Caching.md) extends the [ASP.NET Core distributed cache](https://docs.microsoft.com/en-us/aspnet/core/performance/caching/distributed). So, **any provider** supported by the standard ASP.NET Core distributed cache can be usable in your application and can be configured just like **documented by Microsoft**.

However, JELLOG provides an **integration package** for Redis Cache: [DataGap.Jellog.Caching.StackExchangeRedis](https://www.nuget.org/packages/DataGap.Jellog.Caching.StackExchangeRedis). There are two reasons for using this package, instead of the standard [Microsoft.Extensions.Caching.StackExchangeRedis](https://www.nuget.org/packages/Microsoft.Extensions.Caching.StackExchangeRedis/) package.

1. It implements `SetManyAsync` and `GetManyAsync` methods. These are not standard methods of the Microsoft Caching library, but added by the JELLOG Framework [Caching](Caching.md) system. They **significiantly increases the performance** when you need to set/get multiple cache items with a single method call.
2. It **simplifies** the Redis cache **configuration** (will be explained below).

> DataGap.Jellog.Caching.StackExchangeRedis is already uses the Microsoft.Extensions.Caching.StackExchangeRedis package, but extends and improves it.

## Installation

> This package is already installed in the application startup template if it is using Redis.

Open a command line in the folder of your `.csproj` file and type the following JELLOG CLI command:

````bash
jellog add-package DataGap.Jellog.Caching.StackExchangeRedis
````

## Configuration

DataGap.Jellog.Caching.StackExchangeRedis package automatically gets the Redis [configuration](Configuration.md) from the `IConfiguration`. So, for example, you can set your configuration inside the `appsettings.json`:

````js
"Redis": { 
 "IsEnabled": "true",
 "Configuration": "127.0.0.1"
}
````
The setting `IsEnabled` is optional and will be considered `true` if it is not set.

Alternatively you can configure the standard [RedisCacheOptions](https://docs.microsoft.com/en-us/dotnet/api/microsoft.extensions.caching.stackexchangeredis.rediscacheoptions) [options](Options.md) class in the `ConfigureServices` method of your [module](Module-Development-Basics.md):

````csharp
Configure<RedisCacheOptions>(options =>
{
    //...
});
````

## See Also

* [Caching](Caching.md)