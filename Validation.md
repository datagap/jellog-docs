# Validation

Validation system is used to validate the user input or client request for a particular controller action or service method.

JELLOG is compatible with the ASP.NET Core Model Validation system and everything written in [its documentation](https://docs.microsoft.com/en-us/aspnet/core/mvc/models/validation) is already valid for JELLOG based applications. So, this document mostly focuses on the JELLOG features rather than repeating the Microsoft documentation.

In addition, JELLOG adds the following benefits:

* Defines `IValidationEnabled` to add automatic validation to an arbitrary class. Since all the [application services](Application-Services.md) inherently implements it, they are also validated automatically.
* Automatically localize the validation errors for the data annotation attributes.
* Provides extensible services to validate a method call or an object state.
* Provides [FluentValidation](https://fluentvalidation.net/) integration.

## Validating DTOs

This section briefly introduces the validation system. For details, see the [ASP.NET Core validation documentation](https://docs.microsoft.com/en-us/aspnet/core/mvc/models/validation).

### Data Annotation Attributes

Using data annotations is a simple way to implement the formal validation for a [DTO](Data-Transfer-Objects.md) in a declarative way. Example:

````csharp
public class CreateBookDto
{
    [Required]
    [StringLength(100)]
    public string Name { get; set; }

    [Required]
    [StringLength(1000)]
    public string Description { get; set; }

    [Range(0, 999.99)]
    public decimal Price { get; set; }
}
````

When you use this class as a parameter to an [application service](Application-Services.md) or a controller, it is automatically validated and a localized validation exception is thrown ([and handled](Exception-Handling.md) by the JELLOG framework).

### IValidatableObject

`IValidatableObject` can be implemented by a DTO to perform custom validation logic. `CreateBookDto`  in the following example implements this interface and checks if the `Name` is equals to the `Description` and returns a validation error in this case.

````csharp
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;

namespace Acme.BookStore
{
    public class CreateBookDto : IValidatableObject
    {
        [Required]
        [StringLength(100)]
        public string Name { get; set; }

        [Required]
        [StringLength(1000)]
        public string Description { get; set; }

        [Range(0, 999.99)]
        public decimal Price { get; set; }

        public IEnumerable<ValidationResult> Validate(
            ValidationContext validationContext)
        {
            if (Name == Description)
            {
                yield return new ValidationResult(
                    "Name and Description can not be the same!",
                    new[] { "Name", "Description" }
                );
            }
        }
    }
}
````

#### Resolving a Service

If you need to resolve a service from the [dependency injection system](Dependency-Injection.md), you can use the `ValidationContext` object. Example:

````csharp
var myService = validationContext.GetRequiredService<IMyService>();
````

> While resolving services in the `Validate` method allows any possibility, it is not a good practice to implement your domain validation logic in DTOs. Keep DTOs simple. Their purpose is to transfer data (DTO: Data Transfer Object).

## Validation Infrastructure

This section explains a few additional services provided by the JELLOG framework.

### IValidationEnabled Interface

`IValidationEnabled` is an empty marker interface that can be implemented by any class (registered to and resolved from the [DI](Dependency-Injection.md)) to let the JELLOG framework perform the validation system for the methods of the class. Example:

````csharp
using System.Threading.Tasks;
using DataGap.Jellog.DependencyInjection;
using DataGap.Jellog.Validation;

namespace Acme.BookStore
{
    public class MyService : ITransientDependency, IValidationEnabled
    {
        public virtual async Task DoItAsync(MyInput input)
        {
            //...
        }
    }
}
````

> JELLOG framework uses the [dynamic proxying / interception](Dynamic-Proxying-Interceptors.md) system to perform the validation. In order to make it working, your method should be **virtual** or your service should be injected and used over an **interface** (like `IMyService`).

#### Enabling/Disabling Validation

You can use the `[DisableValidation]` to disable it for methods, classs and properties.

````csharp
[DisableValidation]
public Void MyMethod()
{
}

[DisableValidation]
public class InputClass
{
    public string MyProperty { get; set; }
}

public class InputClass
{
    [DisableValidation]
    public string MyProperty { get; set; }
}
````

### JellogValidationException

Once JELLOG determines a validation error, it throws an exception of type `JellogValidationException`. Your application code can throw `JellogValidationException`, but most of the times it is not needed.

* `ValidationErrors` property of the `JellogValidationException` contains the validation error list.
* Log level of the `JellogValidationException` is set to `Warning`. It logs all the validation errors to the [logging system](Logging.md).
* `JellogValidationException` is automatically caught by the JELLOG framework and converted to a usable error into with HTTP 400 status code. See the [exception handling](Exception-Handling.md) document for more.

## Advanced Topics

### IObjectValidator

In addition to the automatic validation, you may want to manually validate an object. In this case, [inject](Dependency-Injection.md) and use the `IObjectValidator` service:

* `ValidateAsync` method validates the given object based on the validation rules and throws an `JellogValidationException` if it is not in a valid state.
* `GetErrorsAsync` doesn't throw an exception, but only returns the validation errors.

`IObjectValidator` is implemented by the `ObjectValidator` by default. `ObjectValidator` is extensible; you can implement `IObjectValidationContributor` interface to contribute a custom logic. Example:

````csharp
public class MyObjectValidationContributor
    : IObjectValidationContributor, ITransientDependency
{
    public Task AddErrorsAsync(ObjectValidationContext context)
    {
        //Get the validating object
        var obj = context.ValidatingObject;

        //Add the validation errors if available
        context.Errors.Add(...);
        return Task.CompletedTask;
    }
}
````

* Remember to register your class to the [DI](Dependency-Injection.md) (implementing `ITransientDependency` does it just like in this example)
* JELLOG will automatically discover your class and use on any type of object validation (including automatic method call validation).

### IMethodInvocationValidator

`IMethodInvocationValidator` is used to validate a method call. It internally uses the `IObjectValidator` to validate objects passes to the method call. You normally don't need to this service since it is automatically used by the framework, but you may want to reuse or replace it on your application in rare cases.

## FluentValidation Integration

DataGap.Jellog.FluentValidation package integrates the FluentValidation library to the validation system (by implementing the `IObjectValidationContributor`). See the [FluentValidation Integration document](FluentValidation.md) for more.
