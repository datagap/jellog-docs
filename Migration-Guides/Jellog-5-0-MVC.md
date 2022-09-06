# JELLOG MVC / Razor Pages UI v4.x to v5.0 Migration Guide

> This document is for the JELLOG MVC / Razor Pages UI. See also [the main migration guide](Jellog-5_0.md).

## Use install-libs by default

Removed the Gulp dependency from the MVC / Razor Pages UI projects in favor of `jellog install-libs` command ([see](https://docs.jellog.io/en/jellog/5.0/UI/AspNetCore/Client-Side-Package-Management#install-libs-command)) of the JELLOG CLI. You should run this command whenever you change/upgrade your client-side package dependencies via `package.json`.

## Switched to SweetAlert2

Switched from SweetAlert to SweetAlert2. Run the `jellog install-libs` command (in the root directory of the web project) after upgrading your solution. See [#9607](https://github.com/jellogframework/jellog/pull/9607).

