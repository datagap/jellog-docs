# How to Test Blazor Components in JELLOG

## Source Code

You can find the source of the example solution used in this article [here](https://github.com/jellogframework/jellog-samples/tree/master/BlazorPageUniTest).


In this article, I will use [bUnit](https://github.com/bUnit-dev/bUnit) for a simple test of a Blazor component.

## Getting Started

Use the JELLOG CLI to create a blazor app

`jellog new BookStore -t app -u blazor`

Then add the `BookStore.Blazor.Tests` xunit test project to the solution, and add [bUnit](https://github.com/bUnit-dev/bUnit) package and `ProjectReference` to the test project.

The contents of `BookStore.Blazor.Tests.csproj`
```xml
<Project Sdk="Microsoft.NET.Sdk">

    <PropertyGroup>
        <TargetFramework>net6.0</TargetFramework>
        <Nullable>enable</Nullable>
        <IsPackable>false</IsPackable>
    </PropertyGroup>

    <ItemGroup>
        <PackageReference Include="bunit" Version="1.2.49" />
        <PackageReference Include="Microsoft.NET.Test.Sdk" Version="16.11.0" />
        <PackageReference Include="DataGap.Jellog.Authorization.Abstractions" Version="5.0.1" />
        <PackageReference Include="xunit" Version="2.4.1" />
        <PackageReference Include="xunit.runner.visualstudio" Version="2.4.3">
            <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
            <PrivateAssets>all</PrivateAssets>
        </PackageReference>
        <PackageReference Include="coverlet.collector" Version="3.1.0">
            <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
            <PrivateAssets>all</PrivateAssets>
        </PackageReference>
    </ItemGroup>

    <ItemGroup>
      <ProjectReference Include="..\..\src\BookStore.Blazor\BookStore.Blazor.csproj" />
      <ProjectReference Include="..\BookStore.EntityFrameworkCore.Tests\BookStore.EntityFrameworkCore.Tests.csproj" />
    </ItemGroup>

</Project>
```

Create `BookStoreBlazorTestModule` that depends on `JellogAspNetCoreComponentsModule` and `BookStoreEntityFrameworkCoreTestModule`.

```cs
[DependsOn(
    typeof(JellogAspNetCoreComponentsModule),
    typeof(BookStoreEntityFrameworkCoreTestModule)
)]
public class BookStoreBlazorTestModule : JellogModule
{

}
```

Create a `BookStoreBlazorTestBase` class and add the `CreateTestContext` method. The `CreateTestContext` have key code.

It uses JELLOG's `ServiceProvider` as a fallback `ServiceProvider` and add all JELLOG's services to the `TestContext`.

```cs
public abstract class BookStoreBlazorTestBase : BookStoreTestBase<BookStoreBlazorTestModule>
{
    protected virtual TestContext CreateTestContext()
    {
        var testContext = new TestContext();
        testContext.Services.AddFallbackServiceProvider(ServiceProvider);
        foreach (var service in ServiceProvider.GetRequiredService<IJellogApplicationWithExternalServiceProvider>().Services)
        {
            testContext.Services.Add(service);
        }
        testContext.Services.AddBlazorise().AddBootstrap5Providers().AddFontAwesomeIcons();
        return testContext;
    }
}
```

Finally, we add an `Index_Tests` class to test the `Index` component.

```cs
public class Index_Tests : BookStoreBlazorTestBase
{
    [Fact]
    public void Index_Test()
    {
        using (var ctx = CreateTestContext())
        {
            // Act
            var cut = ctx.RenderComponent<BookStore.Blazor.Pages.Index>();

            // Assert
            cut.Find(".lead").InnerHtml.Contains("Welcome to the application. This is a startup project based on the JELLOG framework. For more information, visit jellog.io.").ShouldBeTrue();

            cut.Find("#username").InnerHtml.Contains("Welcome admin").ShouldBeTrue();
        }
    }
}
```

## Reference document

https://github.com/bUnit-dev/bUnit

https://docs.microsoft.com/en-us/aspnet/core/blazor/test
