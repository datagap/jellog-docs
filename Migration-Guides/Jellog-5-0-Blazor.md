# JELLOG Blazor UI v4.x to v5.0 Migration Guide

> This document is for the Blazor UI. See also [the main migration guide](Jellog-5_0.md).

## Upgrading to the latest Blazorise

JELLOG 5.0 uses the latest version of the [Blazorise](https://blazorise.com/) library. Please upgrade the Blazorise NuGet packages in your solution.

## Bootstrap 5

JELLOG 5.0 now works with Bootstrap 5. For details, please refer to the official [migration guide](https://getbootstrap.com/docs/5.0/migration/) provided by Bootstrap.

Replace `Blazorise.Bootstrap` with `Blazorise.Bootstrap5` package.

Replace `AddBootstrapProviders()` with `AddBootstrap5Providers()`.

## Update Bundle

Use `jellog bundle` command to update bundles if you are using Blazor WebAssembly.
