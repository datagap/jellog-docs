# Bootstrap Modules

JELLOG framework can be bootstrapped in various applications. like ASP NET Core or Console, WPF, etc.

Modules can be started sync or async, Corresponds to various event methods in the module. We recommend using **async**, Especially if you want to make async calls in the module's methods.

The `PreConfigureServices`, `ConfigureServices`, `PostConfigureServices`, `OnPreApplicationInitialization`, `OnApplicationInitialization`, `OnPostApplicationInitialization` methods of module have the Async version. 

> Async methods automatically call sync methods by default.

If you use async methods in your module, please keep the same sync methods for compatibility.

````csharp
public async override Task OnApplicationInitializationAsync(ApplicationInitializationContext context)
{
    await AsyncMethod();
}

public override void OnApplicationInitialization(ApplicationInitializationContext context)
{
    AsyncHelper.RunSync(() => OnApplicationInitializationAsync(context));
}
````

## ASP NET Core

Bootstrap JELLOG by using [WebApplication](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.webapplication?view=aspnetcore-6.0) 

````csharp
var builder = WebApplication.CreateBuilder(args);
builder.Host.AddAppSettingsSecretsJson()
    .UseAutofac();

await builder.Services.AddApplicationAsync<MyProjectNameWebModule>();
var app = builder.Build();

await app.InitializeApplicationAsync();
await app.RunAsync();
````

## Console

Bootstrap JELLOG in Console App.

````csharp
var jellogApplication = await JellogApplicationFactory.CreateAsync<MyProjectNameModule>(options =>
{
    options.UseAutofac();
});

await _jellogApplication.InitializeAsync();

var helloWorldService = _jellogApplication.ServiceProvider.GetRequiredService<HelloWorldService>();

await helloWorldService.SayHelloAsync();
````

Bootstrap JELLOG by using [HostedService](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/host/hosted-services?view=aspnetcore-6.0&tabs=visual-studio#ihostedservice-interface) 

````csharp
public class MyHostedService : IHostedService
{
    private IJellogApplicationWithInternalServiceProvider _jellogApplication;

    private readonly IConfiguration _configuration;
    private readonly IHostEnvironment _hostEnvironment;

    public MyHostedService(IConfiguration configuration, IHostEnvironment hostEnvironment)
    {
        _configuration = configuration;
        _hostEnvironment = hostEnvironment;
    }

    public async Task StartAsync(CancellationToken cancellationToken)
    {
        _jellogApplication = await JellogApplicationFactory.CreateAsync<MyProjectNameModule>(options =>
        {
            options.Services.ReplaceConfiguration(_configuration);
            options.Services.AddSingleton(_hostEnvironment);

            options.UseAutofac();
            options.Services.AddLogging(loggingBuilder => loggingBuilder.AddSerilog());
        });

        await _jellogApplication.InitializeAsync();

        var helloWorldService = _jellogApplication.ServiceProvider.GetRequiredService<HelloWorldService>();

        await helloWorldService.SayHelloAsync();
    }

    public async Task StopAsync(CancellationToken cancellationToken)
    {
        await _jellogApplication.ShutdownAsync();
    }
}
````

## WPF

Bootstrap JELLOG on [OnStartup](https://docs.microsoft.com/en-us/dotnet/api/system.windows.application.onstartup?view=windowsdesktop-6.0) method.

````csharp
public partial class App : Application
{
    private IJellogApplicationWithInternalServiceProvider _jellogApplication;

    protected async override void OnStartup(StartupEventArgs e)
    {
        _jellogApplication =  await JellogApplicationFactory.CreateAsync<MyProjectNameModule>(options =>
        {
            options.UseAutofac();
            options.Services.AddLogging(loggingBuilder => loggingBuilder.AddSerilog(dispose: true));
        });

        await _jellogApplication.InitializeAsync();

        _jellogApplication.Services.GetRequiredService<MainWindow>()?.Show();
    }

    protected async override void OnExit(ExitEventArgs e)
    {
        await _jellogApplication.ShutdownAsync();
    }
}

````

