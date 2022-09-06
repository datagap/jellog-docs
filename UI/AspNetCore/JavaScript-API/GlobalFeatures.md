# ASP.NET Core MVC / Razor Pages UI: JavaScript Global Features API

`jellog.globalFeatures` API allows you to get the enabled features of the [Global Features](../../../Global-Features.md) in the client side.

> This document only explains the JavaScript API. See the [Global Features](../../../Global-Features.md) document to understand the JELLOG Global Features system.

## Usage

````js
//Gets all enabled global features.
> jellog.globalFeatures.enabledFeatures

[ 'Shopping.Payment', 'Ecommerce.Subscription' ]


//Check the global feature is enabled
> jellog.globalFeatures.isEnabled('Ecommerce.Subscription')

true

> jellog.globalFeatures.isEnabled('My.Subscription')

false
````
