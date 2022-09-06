# Migration Guide for the Blazor UI from the v3.2 to the v3.3

## Startup Template Changes

* Remove `DataGap.Jellog.Account.Blazor` NuGet package from your `.Blazor.csproj` and add `DataGap.Jellog.TenantManagement.Blazor` NuGet package.
* Remove the ``typeof(JellogAccountBlazorModule)`` from the dependency list of *YourProjectBlazorModule* class and add the `typeof(JellogTenantManagementBlazorModule)`.
* Add `@using DataGap.Jellog.BlazoriseUI` and `@using DataGap.Jellog.BlazoriseUI.Components` into the `_Imports.razor` file.
* Remove the `div` with `id="blazor-error-ui"` (with its contents) from the `wwwroot/index.html ` file, since the JELLOG Framework now shows error messages as a better message box.
* Update the`AddOidcAuthentication` options in your *YourProjectBlazorModule* class as described in the issue [#5913](https://github.com/jellogframework/jellog/issues/5913).

## BlazoriseCrudPageBase to JellogCrudPageBase

Renamed `BlazoriseCrudPageBase` to `JellogCrudPageBase`. Just update the usages. It also has some changes, you may need to update method calls/usages manually.

