# LeptonX Lite Blazor UI

````json
//[doc-params]
{
    "UI": ["Blazor", "BlazorServer"]
}
````

LeptonX Lite has implementation for the JELLOG Framework Blazor WebAssembly & Blazor Server. It's a simplified variation of the [LeptonX Theme](https://x.leptontheme.com/).

>   If you are looking for a professional, enterprise ready theme, you can check the [LeptonX Theme](https://x.leptontheme.com/), which is a part of [JELLOG Commercial](https://commercial.jellog.io/).

> See the [Theming document](https://docs.jellog.io/en/jellog/latest/UI/AspNetCore/Theming) to learn about themes.

## Installation

{{if UI == "Blazor"}}
- Complete the [MVC Razor Pages Installation](AspNetCore.md#installation) for the **HttpApi.Host** application first. _If the solution is tiered/micro-service, complete the MVC steps for all MVC applications such as **HttpApi.Host** and if identity server is separated, install to the **IdentityServer**_.

- Add **DataGap.Jellog.AspNetCore.Components.WebAssembly.LeptonXLiteTheme** package to your **Blazor WebAssembly** application with the following command:

  ```bash
  dotnet add package DataGap.Jellog.AspNetCore.Components.WebAssembly.LeptonXLiteTheme --prerelease
  ```

- Remove **DataGap.Jellog.AspNetCore.Components.WebAssembly.BasicTheme** reference from the project since it's not necessary after switching to LeptonX Lite.

- Remove the old theme from the **DependsOn** attribute in your module class and add the **JellogAspNetCoreComponentsWebAssemblyLeptonXLiteThemeModule** type to the **DependsOn** attribute.

```diff
[DependsOn(
     // Remove BasicTheme module from DependsOn attribute
-    typeof(JellogAspNetCoreComponentsWebAssemblyBasicThemeModule),

    // Add LeptonX Lite module to DependsOn attribute
+    typeof(JellogAspNetCoreComponentsWebAssemblyLeptonXLiteThemeModule),
)]
```

- Change startup App component with the LeptonX one.

```csharp
// Make sure the 'App' comes from 'DataGap.Jellog.AspNetCore.Components.Web.LeptonXLiteTheme.Themes.LeptonXLite' namespace.
builder.RootComponents.Add<App>("#ApplicationContainer");
```

- Run the `jellog bundle` command in your **Blazor** application folder.

{{end}}


{{if UI == "BlazorServer"}}

- Complete the [MVC Razor Pages Installation](AspNetCore.md#installation) first. _If the solution is tiered/micro-service, complete the MVC steps for all MVC applications such as **HttpApi.Host** and **IdentityServer**_.

- Add **DataGap.Jellog.AspNetCore.Components.Server.LeptonXLiteTheme** package to your **Blazor server** application with the following command:

  ```bash
  dotnet add package DataGap.Jellog.AspNetCore.Components.Server.LeptonXLiteTheme --prerelease
  ```

- Remove **DataGap.Jellog.AspNetCore.Components.Server.BasicTheme** reference from the project since it's not necessary after switching to LeptonX Lite.


- Remove old theme from the **DependsOn** attribute in your module class and add the **JellogAspNetCoreComponentsServerLeptonXLiteThemeModule** type to the **DependsOn** attribute.

  ```diff
  [DependsOn(
      // Remove BasicTheme module from DependsOn attribute
  -    typeof(JellogAspNetCoreComponentsServerBasicThemeModule),

      // Add LeptonX Lite module to DependsOn attribute
  +    typeof(JellogAspNetCoreComponentsServerLeptonXLiteThemeModule)
  )]
  ```

- Replace `BlazorBasicThemeBundles` with `BlazorLeptonXLiteThemeBundles` in `JellogBundlingOptions`:
  ```diff
  options.StyleBundles.Configure(
    // Remove following line
  - BlazorBasicThemeBundles.Styles.Global,
    // Add following line instead
  + BlazorLeptonXLiteThemeBundles.Styles.Global,
    bundle =>
    {
        bundle.AddFiles("/blazor-global-styles.css");
        //You can remove the following line if you don't use Blazor CSS isolation for components
        bundle.AddFiles("/MyProjectName.Blazor.styles.css");
    });
  ```

- Update `_Host.cshtml` file. _(located under **Pages** folder by default.)_

  - Add following usings to Locate **App** and **BlazorLeptonXLiteThemeBundles** classes.
    ```csharp
    @using DataGap.Jellog.AspNetCore.Components.Web.LeptonXLiteTheme.Themes.LeptonXLite
    @using DataGap.Jellog.AspNetCore.Components.Server.LeptonXLiteTheme.Bundling
    ```
  - Then replace script & style bundles as following:
    ```diff
    // Remove following line
    - <jellog-style-bundle name="@BlazorBasicThemeBundles.Styles.Global" />
    // Add following line instead
    + <jellog-style-bundle name="@BlazorLeptonXLiteThemeBundles.Styles.Global" />
    ```

    ```diff
    // Remove following line
    - <jellog-script-bundle name="@BlazorBasicThemeBundles.Scripts.Global" />
    // Add following line instead
    + <jellog-script-bundle name="@BlazorLeptonXLiteThemeBundles.Scripts.Global" />
    ```

{{end}}


---

## Customization

### Toolbars
LeptonX Lite includes separeted toolbars for desktop & mobile. You can manage toolbars independently. Toolbar names can be accessible in the **LeptonXLiteToolbars** class.

- `LeptonXLiteToolbars.Main`
- `LeptonXLiteToolbars.MainMobile`

```csharp
public async Task ConfigureToolbarAsync(IToolbarConfigurationContext context)
{
    if (context.Toolbar.Name == LeptonXLiteToolbars.Main)
    {
        context.Toolbar.Items.Add(new ToolbarItem(typeof(MyDesktopComponent)));
    }

    if (context.Toolbar.Name == LeptonXLiteToolbars.MainMobile)
    {
        context.Toolbar.Items.Add(new ToolbarItem(typeof(MyMobileComponent)));
    }

    return Task.CompletedTask;
}
```

{{if UI == "BlazorServer"}}

> _You can visit the [Toolbars Documentation](https://docs.jellog.io/en/jellog/latest/UI/Blazor/Toolbars) for better understanding._

{{end}}
