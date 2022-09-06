# JELLOG Framework 4.x to 4.3 Migration Guide

This version comes with some changes in the startup template, mostly related to Blazor UI. This document explains the breaking changes. However, **it is suggested to [compare the startup templates manually](Upgrading-Startup-Template.md) to see all the changes** and apply to your solution.

## Common

* `app.UseVirtualFiles()` has been marked as **obsolete**. Use `app.UseStaticFiles()` instead. JELLOG will handle the virtual file system integrated to the static files middleware.

## Blazor UI

Implemented the Blazor Server Side support with this release. It required some packages and namespaces arrangements. **Existing Blazor (WebAssembly) applications should done the changes explained in this section**.

### Namespace Changes

- `JellogBlazorMessageLocalizerHelper` -> moved to DataGap.Jellog.AspNetCore.Components.Web
- `JellogRouterOptions` -> moved to DataGap.Jellog.AspNetCore.Components.Web.Theming.Routing
- `JellogToolbarOptions` and `IToolbarContributor` -> moved to DataGap.Jellog.AspNetCore.Components.Web.Theming.Toolbars
- `IJellogUtilsService` -> moved to DataGap.Jellog.AspNetCore.Components.Web
- `PageHeader` -> moved to `DataGap.Jellog.AspNetCore.Components.Web.Theming.Layout`.

In practice, if your application is broken because of the `DataGap.Jellog.AspNetCore.Components.WebAssembly.*` namespace, please try to switch to `DataGap.Jellog.AspNetCore.Components.Web.*` namespace.

Remember to change namespaces in the `_Imports.razor` files.

### Package Changes

No change on the framework packages, but **module packages are separated as Web Assembly & Server**;

* Use `DataGap.Jellog.Identity.Blazor.WebAssembly` NuGet package instead of `DataGap.Jellog.Identity.Blazor` package. Also, change `JellogIdentityBlazorModule` usage to `JellogIdentityBlazorWebAssemblyModule` in the `[DependsOn]` attribute on your module class.
* Use `DataGap.Jellog.TenantManagement.Blazor.WebAssembly` NuGet package instead of `DataGap.Jellog.TenantManagement.Blazor` package. Also, change `JellogTenantManagementBlazorModule` usage to `JellogTenantManagementBlazorWebAssemblyModule` in the `[DependsOn]` attribute on your module class.
* Use `DataGap.Jellog.PermissionManagement.Blazor.WebAssembly` NuGet package instead of `DataGap.Jellog.PermissionManagement.Blazor` package. Also, change `JellogPermissionManagementBlazorModule` usage to `JellogPermissionManagementBlazorWebAssemblyModule` in the `[DependsOn]` attribute on your module class.
* Use `DataGap.Jellog.SettingManagement.Blazor.WebAssembly` NuGet package instead of `DataGap.Jellog.SettingManagement.Blazor` package. Also, change `JellogSettingManagementBlazorModule` usage to `JellogSettingManagementBlazorWebAssemblyModule` in the `[DependsOn]` attribute on your module class.
* Use `DataGap.Jellog.FeatureManagement.Blazor.WebAssembly` NuGet package instead of `DataGap.Jellog.FeatureManagement.Blazor` package. Also, change `JellogFeatureManagementBlazorModule` usage to `JellogFeatureManagementBlazorWebAssemblyModule` in the `[DependsOn]` attribute on your module class.

### Other Changes

* `EntityAction.RequiredPermission` has been marked as **obsolete**, because of performance reasons. It is suggested to use the `Visible` property by checking the permission/policy yourself and assigning to a variable.

### Resource Reference Changes

Open `<YourProjectName>BundleContributor.cs` and replace `context.Add("main.css");` to `context.Add("main.css", true);`

Then run `jellog bundle` command in the `blazor` folder to update resource references.