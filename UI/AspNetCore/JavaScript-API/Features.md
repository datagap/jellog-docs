# ASP.NET Core MVC / Razor Pages UI: JavaScript Features API

`jellog.features` API allows you to check features or get the values of the features on the client side. You can read the current value of a feature in the client side only if it is allowed by the feature definition (on the server side).

> This document only explains the JavaScript API. See the [Features](../../../Features.md) document to understand the JELLOG Features system.

## Basic Usage

````js
//Gets a value as string.
var value = jellog.features.get('ExportingToExcel');

//Check the feature is enabled
var enabled = jellog.features.isEnabled('ExportingToExcel.Enabled');
````

## All Values

`jellog.features.values` can be used to access to the all feature values.

An example value of this object is shown below:

````js
{
  Identity.TwoFactor: "Optional",
  ExportingToExcel.Enabled: "true",
  ...
}
````