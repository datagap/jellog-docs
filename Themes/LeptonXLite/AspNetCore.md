# LeptonX Lite MVC UI
LeptonX Lite has implementation for the JELLOG Framework Razor Pages. It's a simplified variation of the [LeptonX Theme](https://x.leptontheme.com/).

>   If you are looking for a professional, enterprise ready theme, you can check the [LeptonX Theme](https://x.leptontheme.com/), which is a part of [JELLOG Commercial](https://commercial.jellog.io/).

> See the [Theming document](https://docs.jellog.io/en/jellog/latest/UI/AspNetCore/Theming) to learn about themes.

## Installation

- Add **DataGap.Jellog.AspNetCore.Mvc.UI.Theme.LeptonXLite** package to your **Web** application.

```bash
dotnet add package DataGap.Jellog.AspNetCore.Mvc.UI.Theme.LeptonXLite --prerelease
```

- Remove **DataGap.Jellog.AspNetCore.Mvc.UI.Theme.Basic** reference from the project since it's not necessary after switching to LeptonX Lite.

- Make sure the old theme is removed and LeptonX is added in your Module class.

```diff
[DependsOn(
     // Remove BasicTheme module from DependsOn attribute
-    typeof(JellogAspNetCoreMvcUiBasicThemeModule),
     
     // Add LeptonX Lite module to DependsOn attribute
+    typeof(JellogAspNetCoreMvcUiLeptonXLiteThemeModule),
)]
```

- Replace `BasicThemeBundles` with `LeptonXLiteThemeBundles` in JellogBundlingOptions

```diff
Configure<JellogBundlingOptions>(options =>
{
    options.StyleBundles.Configure(
        // Remove following line
-       BasicThemeBundles.Styles.Global,
        // Add following line instead
+       LeptonXLiteThemeBundles.Styles.Global
        bundle =>
        {
            bundle.AddFiles("/global-styles.css");
        }
    );
});
```

---

## Customization

### Toolbars
LeptonX Lite includes separeted toolbars for desktop & mobile. You can manage toolbars independently. Toolbar names can be accessible in the **LeptonXLiteToolbars** class.

- `LeptonXLiteToolbars.Main`
- `LeptonXLiteToolbars.MainMobile`

```csharp
public class MyProjectNameMainToolbarContributor : IToolbarContributor
{
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
    }
}
```
