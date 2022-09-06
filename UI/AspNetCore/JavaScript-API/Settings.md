# ASP.NET Core MVC / Razor Pages UI: JavaScript Setting API

Localization API allows you to get the values of the settings on the client side. You can read the current value of a setting in the client side only if it is allowed by the setting definition (on the server side).

> This document only explains the JavaScript API. See the [settings document](../../../Settings.md) to understand the JELLOG setting system.

## Basic Usage

````js
//Gets a value as string.
var language = jellog.setting.get('Jellog.Localization.DefaultLanguage');

//Gets an integer value.
var requiredLength = jellog.setting.getInt('Jellog.Identity.Password.RequiredLength');

//Gets a boolean value.
var requireDigit = jellog.setting.getBoolean('Jellog.Identity.Password.RequireDigit');
````

## All Values

`jellog.setting.values` can be used to obtain all the setting values as an object where the object properties are setting names and property values are the setting values.

An example value of this object is shown below:

````js
{
  Jellog.Localization.DefaultLanguage: "en",
  Jellog.Timing.TimeZone: "UTC",
  ...
}
````

