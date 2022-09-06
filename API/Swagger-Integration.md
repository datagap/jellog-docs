# Swagger Integration

[Swagger (OpenAPI)](https://swagger.io/) is a language-agnostic specification for describing REST APIs. It allows both computers and humans to understand the capabilities of a REST API without direct access to the source code. Its main goals are to:

- Minimize the amount of work needed to connect decoupled services.
- Reduce the amount of time needed to accurately document a service.

JELLOG Framework offers a prebuilt module for full Swagger integration with small configurations. 

## Installation

> This package is already installed by default with the startup template. So, most of the time, you don't need to install it manually.

If installation is needed, it is suggested to use the [JELLOG CLI](../CLI.md) to install this package.

### Using the JELLOG CLI

Open a command line window in the folder of the `Web` or `HttpApi.Host` project (.csproj file) and type the following command:

```bash
jellog add-package DataGap.Jellog.Swashbuckle
```

### Manual Installation

If you want to manually install;

1. Add the [DataGap.Jellog.Swashbuckle](https://www.nuget.org/packages/DataGap.Jellog.Swashbuckle) NuGet package to your `Web` or `HttpApi.Host` project:

   `Install-Package DataGap.Jellog.Swashbuckle`

2. Add the `JellogSwashbuckleModule` to the dependency list of your module:

   ```csharp
   [DependsOn(
       //...other dependencies
       typeof(JellogSwashbuckleModule) // <-- Add module dependency like that
       )]
   public class YourModule : JellogModule
   {
   }
   ```

## Configuration

First, we need to use `AddJellogSwaggerGen` extension to configure Swagger in `ConfigureServices` method of our module.

```csharp
public override void ConfigureServices(ServiceConfigurationContext context)
{
    var services = context.Services;

    //... other configurations.

    services.AddJellogSwaggerGen(
        options =>
        {
            options.SwaggerDoc("v1", new OpenApiInfo { Title = "Test API", Version = "v1" });
            options.DocInclusionPredicate((docName, description) => true);
            options.CustomSchemaIds(type => type.FullName);
        }
    );
}
```

Then we can use Swagger UI by calling `UseJellogSwaggerUI` method in the `OnApplicationInitialization` method of our module.

```csharp
public override void OnApplicationInitialization(ApplicationInitializationContext context)
{
    var app = context.GetApplicationBuilder();

    //... other configarations.

    app.UseJellogSwaggerUI(options =>
    {
        options.SwaggerEndpoint("/swagger/v1/swagger.json", "Test API");
    });
    
    //... other configarations.
}
```

### Hide JELLOG Endpoints on Swagger UI

If you want to hide JELLOG's default endpoints, call the `HideJellogEndpoints` method in your Swagger configuration as shown in the following example:

```csharp
services.AddJellogSwaggerGen(
    options => 
    {
        //... other options
        
        //Hides JELLOG Related endpoints on Swagger UI
        options.HideJellogEndpoints();
    }
)
```

## Using Swagger with OAUTH

For non MVC/Tiered applications, we need to configure Swagger with OAUTH to handle authorization.  

> JELLOG Framework uses IdentityServer by default. To get more information about IDS, check this [documentation](../Modules/IdentityServer.md). 



To do that, we need to use `AddJellogSwaggerGenWithOAuth` extension to configure Swagger with OAuth issuer and scopes in `ConfigureServices` method of our module.

```csharp
public override void ConfigureServices(ServiceConfigurationContext context)
{
    var services = contex.Services;

    //... other configarations.

    services.AddJellogSwaggerGenWithOAuth(
        "https://localhost:44341",             // authority issuer
        new Dictionary<string, string>         //
        {                                      // scopes
            {"Test", "Test API"}               //
        },                                     //
        options =>
        {
            options.SwaggerDoc("v1", new OpenApiInfo { Title = "Test API", Version = "v1" });
            options.DocInclusionPredicate((docName, description) => true);
            options.CustomSchemaIds(type => type.FullName);
        }
    );
}
```

Then we can use Swagger UI by calling `UseJellogSwaggerUI` method in the `OnApplicationInitialization` method of our module.

> Do not forget to set `OAuthClientId` and `OAuthClientSecret`.


```csharp
public override void OnApplicationInitialization(ApplicationInitializationContext context)
{
    var app = context.GetApplicationBuilder();

    //... other configarations.

    app.UseJellogSwaggerUI(options =>
    {
        options.SwaggerEndpoint("/swagger/v1/swagger.json", "Test API");

        var configuration = context.ServiceProvider.GetRequiredService<IConfiguration>();
        options.OAuthClientId("Test_Swagger"); // clientId
        options.OAuthClientSecret("1q2w3e*");  // clientSecret
    });
    
    //... other configarations.
}
```