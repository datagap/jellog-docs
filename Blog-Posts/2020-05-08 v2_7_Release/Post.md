# JELLOG Framework v2.7.0 Has Been Released!

The **JELLOG Framework** & and the **JELLOG Commercial** v2.7 have been released. We hadn't created blog post for   the 2.4, 2.4 and 2.6 releases, so this post will also cover **what's new** with these releases and **what we've done** in the last 2 months.

## About the Release Cycle & Development

Reminding that we had started to release a new minor feature version **in every two weeks**, generally on Thursdays. Our goal is to deliver new features as soon as possible.

We've completed & merged hundreds of issues and pull requests with **1,300+ commits** in the last 7-8 weeks, only for the JELLOG Framework repository. Daily commit counts are constantly increasing:

![github-contribution-graph](github-contribution-graph.png)

JELLOG.IO Platform is rapidly growing and we are getting more and more contributions from the community.

## What's New in the JELLOG Framework?

### Object Extending System

In the last few releases, we've mostly focused on providing ways to extend existing modules when you use them as NuGet/NPM Packages.

The Object Extending System allows module developers to create extensible modules and allows application developers to customize and extend a module easily.

For example, you can add two extension properties to the user entity of the identity module:

````csharp
ObjectExtensionManager.Instance
    .AddOrUpdate<IdentityUser>(options =>
        {
            options.AddOrUpdateProperty<string>("SocialSecurityNumber");
            options.AddOrUpdateProperty<bool>("IsSuperUser");
        }
    );
````

It is easy to define validation rules for the properties:

````csharp
ObjectExtensionManager.Instance
    .AddOrUpdateProperty<IdentityUserCreateDto, string>(
        "SocialSecurityNumber",
        options =>
        {
            options.Attributes.Add(new RequiredAttribute());
            options.Attributes.Add(
                new StringLengthAttribute(32) {
                    MinimumLength = 6
                }
            );
        });
````

You can even write custom code to validate the property. It automatically works for the objects those are parameters of an application service, controller or a page.

While extension properties of an entity are normally stored in a single JSON formatted field in the database table, you can easily configure to store a property as a table field using the EF Core mapping:

````csharp
ObjectExtensionManager.Instance
    .AddOrUpdateProperty<IdentityUser, string>(
        "SocialSecurityNumber",
        options =>
        {
            options.MapEfCore(b => b.HasMaxLength(32));
        }
    );
````

See the [Object Extensions document](https://docs.jellog.io/en/jellog/latest/Object-Extensions) for details about this system.

See also the [Customizing the Existing Modules](https://docs.jellog.io/en/jellog/latest/Customizing-Application-Modules-Guide) guide to learn all the possible customization options.

### Text Templating Package

[DataGap.Jellog.TextTemplating](https://www.nuget.org/packages/DataGap.Jellog.TextTemplating) is a new package introduced with the v2.7.0. Previously, [DataGap.Jellog.Emailing](https://www.nuget.org/packages/DataGap.Jellog.Emailing) package had a similar functionality but it was limited, experimental and tightly coupled to the emailing.

The new text templating package allows you to define text based templates those can be easily localized and reused. You can define layout templates and share the layout from other templates.

We are currently using it for email sending. A module needs to send an email typically defines a template. Example:

````xml
<h3>{{L "PasswordReset"}}</h3>

<p>{{L "PasswordResetInfoInEmail"}}</p>

<div>
    <a href="{{model.link}}">{{L "ResetMyPassword"}}</a>
</div>
````

This is a typical password reset email template.

* The template system is based on the open source [Scriban library](https://github.com/lunet-io/scriban). So it supports if conditions, loops and much more.
* `model` is used to pass data to the template (just like the ASP.NET Core MVC).
* `L` is a special function that localizes the given string.

It is typical to use the same layout for all emails. So, you can define a layout template. This is the standard layout template comes with the framework:

````xml
<!DOCTYPE html>
<html lang="en" xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="utf-8" />
</head>
<body>
    {{content}}
</body>
</html>
````

A layout should have a `{{content}}` area to render the child content (just like the `RenderBody()` in the MVC).

It is very easy to override a template content by the final application to customize it.

Whenever you need to render a template, use the `ITemplateRenderer` service by providing the template name and a model. See the [text templating documentation](https://docs.jellog.io/en/jellog/latest/Text-Templating) for details. We've even created a UI for the JELLOG Commercial (see the related section below).

### Subscribing to the Exceptions

JELLOG Framework's [exception handling system](https://docs.jellog.io/en/jellog/latest/Exception-Handling) automatically handles exceptions and returns an appropriate result to the client. In some cases, you may want to have a callback that is notified whenever an exception occurs. In this way, for example, you can send an email or take any action based on the exception.

Just create a class derived from the `ExceptionSubscriber` class in your application:

````csharp
public class MyExceptionSubscriber : ExceptionSubscriber
{
    public async override Task HandleAsync(ExceptionNotificationContext context)
    {
        //TODO...
    }
}
````

See the [exception handling](https://docs.jellog.io/en/jellog/latest/Exception-Handling) document for more.

### Others

There are many minor features and enhancements made to the framework in the past releases. Here, a few ones:

* Added `JellogLocalizationOptions.DefaultResourceType` to set the default resource type for the application. In this way, the localization system uses the default resource whenever the resource was not specified. The latest application startup template already configures it, but you may want to set it for your existing applications.
* Added `IsEnabled` to permission definition. In this way, you can completely disable a permission and hide the related functionality from the application. This can be a way of feature switch for some applications. See [#3486](https://github.com/jellogframework/jellog/issues/3486) for usage.
* Added Dutch and German localizations to all the localization resources defined by the framework. Thanks to the contributors.

## What's New in the JELLOG Commercial

The goal of the [JELLOG Commercial](https://commercial.jellog.io/) is to provide pre-build application functionalities, code generation tools, professional themes, advanced samples and premium support for JELLOG Framework based projects.

We are working on the JELLOG Commercial in the parallel to align with the JELLOG Framework features and provide more modules, theme options and tooling.

This section explains what's going on the JELLOG Commercial side.

### Module Entity Extension System

Module entity extension system is a higher level API that uses the object extension system (introduced above) and provides an easy way to add extension properties to existing entities. A new extension property easily automatically becomes a part of the HTTP API and the User Interface.

Example: Add a `SocialSecurityNumber` to the user entity of the identity module

````csharp
ObjectExtensionManager.Instance.Modules()
    .ConfigureIdentity(identity =>
    {
        identity.ConfigureUser(user =>
        {
            user.AddOrUpdateProperty<string>( //property type: string
                "SocialSecurityNumber", //property name
                property =>
                {
                    //validation rules
                    property.Attributes.Add(new RequiredAttribute());
                    property.Attributes.Add(
                        new StringLengthAttribute(64) {
                            MinimumLength = 4
                        }
                    );

                    //...other configurations for this property
                }
            );
        });
    });
````

With just such a configuration, the user interface will have the new property (on the table and on the create/edit forms):

![module-entity-extended-ui](module-entity-extended-ui.png)

The new property can be easily localized and validated. Currently, it supports primitive types like string, number and boolean, but we planned to add more advanced scenarios by the time (like navigation/lookup properties).

See the [Module Entity Extensions](https://docs.jellog.io/en/commercial/latest/guides/module-entity-extensions) guide to learn how to use it and configure details.

#### Other Extension Points

There are also some other pre-defined points to customize and extend the user interface of a depended module:

* You can add a new action for an entity on the data table (left side on the picture below).
* You can add new buttons (or other controls) to the page toolbar (right side on the picture below).
* You can add custom columns to a data table.

![jellog-commercial-ui-extensions](jellog-commercial-ui-extensions.png)

See the [Customizing the Modules](https://docs.jellog.io/en/commercial/latest/guides/customizing-modules) guide to learn all the possible ways to customize a depended module.

### Text Template Management Module

We are introducing a new module with the v2.7 release: [Text Template Management](https://docs.jellog.io/en/commercial/latest/modules/text-template-management). It is basically used to edit text/email templates (introduced with the JELLOG Framework 2.7) on the user interface and save changed in the database.

A screenshot from the content editing for the password reset email template:

![text-template-content-ui](text-template-content-ui.png)

This module comes pre-installed when you create a new project.

### Entity History Views

Audit logging UI module now shows all the entity changes in the application with property change details.

![audit-log-entity-changes](audit-log-entity-changes.png)

You can also check history for an entity when you click to the actions menu for the entity:

![tenant-entity-changes](tenant-entity-changes.png)

### More Samples

We are creating more advanced sample applications built with the JELLOG Commercial. Easy CRM is one of them which will be available in a few days to the commercial customers.

Here, a screenshot from the Easy CRM dashboard:

![easy-crm](easy-crm.png)

It has accounts, contacts, product groups, products, orders and so on.

### New Modules

We continue to improve existing modules and creating new modules. In addition to the new [text template management](https://docs.jellog.io/en/commercial/latest/modules/text-template-management) module introduced above;

* We've recently released a [payment module](https://commercial.jellog.io/modules/DataGap.Payment) that currently works with PayU and 2Checkout payment gateways. More gateways will be added by the time.
* We've created a simple [Twilio SMS integration](https://docs.jellog.io/en/commercial/latest/modules/twilio-sms) module to send SMS over the Twilio.
* We are working on a **chat module** that is currently being developed and will be available in the next weeks.
* We are working on the **organization unit management** system for the identity module to create hierarchical organization units (domain layer will be open source & free).

More modules, theme and tooling options are being developed for the JELLOG Commercial and the JELLOG Framework.

## JELLOG Framework vs JELLOG Commercial

We ([DataGapsoft](https://dataGapsoft.com/) - the core team behind the JELLOG.IO platform), are spending almost equal time on the JELLOG Framework and the JELLOG Commercial and we consider the JELLOG.IO platform as a whole.

[JELLOG Framework](https://jellog.io/) provides all the infrastructure and application independent framework features to make you more productive, focus on your own business code and implement software development best practices. It provides you a well defined and comfortable development experience without repeating yourself.

[JELLOG Commercial](https://commercial.jellog.io/) provides pre-built functionalities, themes and tooling to save your time if your requirements involve these functionalities in addition to the premium support for the framework and the pre-built modules.
