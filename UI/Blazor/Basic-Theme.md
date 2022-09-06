# Blazor UI: Basic Theme

````json
//[doc-params]
{
    "UI": ["Blazor", "BlazorServer"]
}
````

The Basic Theme is a theme implementation for the Blazor UI. It is a minimalist theme that doesn't add any styling on top of the plain [Bootstrap](https://getbootstrap.com/). You can take the Basic Theme as the **base theme** and build your own theme or styling on top of it. See the *Customization* section.

> If you are looking for a professional, enterprise ready theme, you can check the [Lepton Theme](https://commercial.jellog.io/themes), which is a part of the [JELLOG Commercial](https://commercial.jellog.io/).

> See the [Theming document](Theming.md) to learn about themes.

## Installation

**This theme is already installed** when you create a new solution using the [startup templates](../../Startup-Templates/Index.md). If you need to manually install it, follow the steps below:

{{if UI == "Blazor"}}

* Install the [DataGap.Jellog.AspNetCore.Components.WebAssembly.BasicTheme](https://www.nuget.org/packages/DataGap.Jellog.AspNetCore.Components.WebAssembly.BasicTheme) NuGet package to your web project.
* Add `JellogAspNetCoreComponentsWebAssemblyBasicThemeModule` into the `[DependsOn(...)]` attribute for your [module class](../../Module-Development-Basics.md) in the your Blazor UI project.
* Use `DataGap.Jellog.AspNetCore.Components.WebAssembly.BasicTheme.Themes.Basic.App` as the root component of your application in the `ConfigureServices` method of your module:

    ```csharp
    var builder = context.Services.GetSingletonInstance<WebAssemblyHostBuilder>();
    builder.RootComponents.Add<App>("#ApplicationContainer");
    ```
    `#ApplicationContainer` is a selector (like `<div id="ApplicationContainer">Loading...</div>`) in the `index.html`.

* Execute `jellog bundle` command under blazor project once.

{{end}}

{{if UI == "BlazorServer"}}

* Make sure [AspNetCore Basic Theme](../AspNetCore/Basic-Theme.md) installation steps are completed. 

* Install the [DataGap.Jellog.AspNetCore.Components.Server.BasicTheme](https://www.nuget.org/packages/DataGap.Jellog.AspNetCore.Components.Server.BasicTheme) NuGet package to your web project.

* Add `JellogAspNetCoreComponentsServerBasicThemeModule` into the `[DependsOn(...)]` attribute for your [module class](../../Module-Development-Basics.md) in the your Blazor UI project.

* Perform following changes in `Pages/_Host.cshtml` file
  * Add usings at the top of the page.
    ```html
    @using DataGap.Jellog.AspNetCore.Components.Server.BasicTheme.Bundling
    @using DataGap.Jellog.AspNetCore.Components.Web.BasicTheme.Themes.Basic
    ```
  * Add Basic theme style bundles between `<head>` tags.
    ```html
    <jellog-style-bundle name="@BlazorBasicThemeBundles.Styles.Global" />
    ```
  * Add `App` component of Basic Theme in the body section of page.
    ```html
    <component type="typeof(App)" render-mode="Server" />
    ```

{{end}}

## The Layout

![basic-theme-application-layout](../../images/basic-theme-application-layout.png)

Application Layout implements the following parts, in addition to the common parts mentioned above;

* [Branding](Branding.md) Area
* Main [Menu](Navigation-Menu.md)
* Main [Toolbar](Toolbars.md) with Language Selection & User Menu
* [Page Alerts](Page-Alerts.md)

## Customization

You have two options two customize this theme:

### Overriding Styles / Components

In this approach, you continue to use the theme as NuGet and NPM packages and customize the parts you need to. There are several ways to customize it;

#### Override the Styles

You can simply override the styles in the Global Styles file of your application.

#### Override the Components

See the [Customization / Overriding Components](Customization-Overriding-Components.md) to learn how you can replace components, customize and extend the user interface.

### Copy & Customize

You can run the following [JELLOG CLI](../../CLI.md) command in **Blazor{{if UI == "Blazor"}}WebAssembly{{else}} Server{{end}}** project directory to copy the source code to your solution:

{{if UI == "Blazor"}}

`jellog add-package DataGap.Jellog.AspNetCore.Components.WebAssembly.BasicTheme --with-source-code --add-to-solution-file`

Then, navigate to downloaded `DataGap.Jellog.AspNetCore.Components.WebAssembly.BasicTheme` project directory and run:

`jellog add-package DataGap.Jellog.AspNetCore.Components.Web.BasicTheme --with-source-code --add-to-solution-file`

{{end}}

{{if UI == "BlazorServer"}}

`jellog add-package DataGap.Jellog.AspNetCore.Components.Server.BasicTheme --with-source-code --add-to-solution-file`

Then, navigate to downloaded `DataGap.Jellog.AspNetCore.Components.Server.BasicTheme` project directory and run:

`jellog add-package DataGap.Jellog.AspNetCore.Components.Web.BasicTheme --with-source-code --add-to-solution-file`

{{end}}

----

Or, you can download the source code of the Basic Theme, manually copy the project content into your solution, re-arrange the package/module dependencies (see the Installation section above to understand how it was installed to the project) and freely customize the theme based on your application requirements.

{{if UI == "Blazor"}}
- [Basic Theme Source Code](https://github.com/jellogframework/jellog/blob/dev/modules/basic-theme/src/DataGap.Jellog.AspNetCore.Components.WebAssembly.BasicTheme)
{{end}}

{{if UI == "BlazorServer"}}
- [Basic Theme Source Code](https://github.com/jellogframework/jellog/blob/dev/modules/basic-theme/src/DataGap.Jellog.AspNetCore.Components.Server.BasicTheme)
{{end}}

## See Also

* [Theming](Theming.md)
