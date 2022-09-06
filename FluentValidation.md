# FluentValidation Integration

JELLOG [Validation](Validation.md) infrastructure is extensible. [DataGap.Jellog.FluentValidation](https://www.nuget.org/packages/DataGap.Jellog.FluentValidation) NuGet package extends the validation system to work with the [FluentValidation](https://fluentvalidation.net/) library.

## Installation

It is suggested to use the [JELLOG CLI](CLI.md) to install this package.

### Using the JELLOG CLI

Open a command line window in the folder of the project (.csproj file) and type the following command:

````bash
jellog add-package DataGap.Jellog.FluentValidation
````

### Manual Installation

If you want to manually install;

1. Add the [DataGap.Jellog.FluentValidation](https://www.nuget.org/packages/DataGap.Jellog.FluentValidation) NuGet package to your project:

   ````
   Install-Package DataGap.Jellog.FluentValidation
   ````

2.  Add the `JellogFluentValidationModule` to the dependency list of your module:

````csharp
[DependsOn(
    //...other dependencies
    typeof(JellogFluentValidationModule) //Add the FluentValidation module
    )]
public class YourModule : JellogModule
{
}
````

## Using the FluentValidation

Follow [the FluentValidation documentation](https://fluentvalidation.net/) to create validator classes.  Example:

````csharp
public class CreateUpdateBookDtoValidator : AbstractValidator<CreateUpdateBookDto>
{
    public CreateUpdateBookDtoValidator()
    {
        RuleFor(x => x.Name).Length(3, 10);
        RuleFor(x => x.Price).ExclusiveBetween(0.0f, 999.0f);
    }
}
````

JELLOG will automatically find this class and associate with the `CreateUpdateBookDto` on object validation.

## See Also

* [Validation System](Validation.md)