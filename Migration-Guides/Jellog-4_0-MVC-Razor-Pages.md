# MVC / Razor Pages UI 3.3 to 4.0 Migration Guide

## Use IBrandingProvider in the DataGap.Jellog.UI Package

This will be a breaking change for MVC UI, but very easy to fix. `IBrandingProvider` is being moved from `DataGap.Jellog.AspNetCore.Mvc.UI.Theme.Shared.Components` to `DataGap.Jellog.Ui.Branding` namespace. So, just update the namespace imports.

