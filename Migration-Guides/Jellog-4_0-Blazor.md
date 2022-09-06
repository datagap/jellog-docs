# Blazor UI 3.3 to 4.0 Migration Guide

## Startup Template Changes

These changes are required to manually applied in your own solution. It would be easier if you create a new solution based on 4.0 with the same name of your current solution then compare the files.

### Csproj File / Dependencies

* Add `<BlazorWebAssemblyLoadAllGlobalizationData>true</BlazorWebAssemblyLoadAllGlobalizationData>` to the `PropertyGroup` section of your project (`.csproj`) file.
* Update the `Blazorise.*` packages to the latest version (to the latest RC for the JELLOG 4.0 preview).

### wwwroot/index.html

There are some changes made in the index.html file;

* Removed JQuery & Bootstrap JavaScript dependencies
* Replaced Bootstrap and FontAwesome imports with local files instead of CDN usages.
* Re-arranged some JELLOG CSS file locations.
* Introduced the `jellog bundle` CLI command to manage global Style/Script file imports.

Follow the steps below to apply the changes;

1. Add the bundle contributor class into your project (it will be slightly different based on your solution namespaces):

````csharp
using DataGap.Jellog.Bundling;

namespace MyCompanyName.MyProjectName.Blazor
{
    public class MyProjectNameBundleContributor : IBundleContributor
    {
        public void AddScripts(BundleContext context)
        {
        }

        public void AddStyles(BundleContext context)
        {
            context.Add("main.css");
        }
    }
}
````

If you are using another global style/script files, add them here.

2. Remove all the `<link...>` elements and replace with the following comment tags:

````html
<!--JELLOG:Styles-->
<!--/JELLOG:Styles-->
````

3. Remove all the `<script...>` elements and replace with the following comment tags:

````html
<!--JELLOG:Scripts-->
<!--/JELLOG:Scripts-->
````

4. Execute the following command in a terminal in the root folder of the Blazor project (`.csproj`) file (ensure that you're using the JELLOG CLI version 4.0):

````bash
jellog bundle
````

This will fill in the `Styles` and `Scripts` tags based on the dependencies.

5. You can clean the `blazor-error-ui` related sections from your `main.css` file since they are not needed anymore.

### The Root Element

This change is optional but recommended.

* Change `<app>...</app>` to `<div id="ApplicationContainer">...</div>` in the `wwwroot/index.html`.
* Change `builder.RootComponents.Add<App>("app");` to `builder.RootComponents.Add<App>("#ApplicationContainer");` in the *YourProjectBlazorModule.cs*.

## JellogCrudPageBase Changes

If you've derived your pages from the `JellogCrudPageBase` class, then you may need to apply the following changes;

- `OpenEditModalAsync` method gets `EntityDto` instead of id (`Guid`) parameter. Pass `context` instead of `context.Id`.
- `DeleteEntityAsync` method doesn't display confirmation dialog anymore. You can use the new `EntityActions` component in Data Grids to show confirmation messages. You can also inject `IUiMessageService` to your page or component and call the `ConfirmAsync` explicitly.
- Added `GetListInput` as a base property that is used to filter while getting the entities from the server.

## Others

- Refactored namespaces for some Blazor components ([#6015](https://github.com/jellogframework/jellog/issues/6015)).
- Removed Async Suffix from IUiMessageService methods ([#6123](https://github.com/jellogframework/jellog/pull/6123)).