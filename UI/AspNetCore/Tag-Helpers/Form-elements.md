# Form Elements

## Introduction

Jellog provides form input tag helpers to make building forms easier.

## Demo

See the [form elements demo page](https://bootstrap-taghelpers.jellog.io/Components/FormElements) to see it in action.

## jellog-input

`jellog-input` tag creates a Bootstrap form input for a given c# property. It uses [Asp.Net Core Input Tag Helper](https://docs.microsoft.com/tr-tr/aspnet/core/mvc/views/working-with-forms?view=aspnetcore-3.1#the-input-tag-helper) in background, so every data annotation attribute of `input` tag helper of Asp.Net Core is also valid for `jellog-input`.

Usage:

````xml
<jellog-input asp-for="@Model.MyModel.Name"/>
<jellog-input asp-for="@Model.MyModel.Description"/>
<jellog-input asp-for="@Model.MyModel.Password"/>
<jellog-input asp-for="@Model.MyModel.IsActive"/>
````

Model:

````csharp
    public class FormElementsModel : PageModel
    {
        public SampleModel MyModel { get; set; }

        public void OnGet()
        {
            MyModel = new SampleModel();
        }

        public class SampleModel
        {
            [Required]
            [Placeholder("Enter your name...")]
            [InputInfoText("What is your name?")]
            public string Name { get; set; }
            
            [Required]
            [FormControlSize(JellogFormControlSize.Large)]
            public string SurName { get; set; }

            [TextArea(Rows = 4)]
            public string Description { get; set; }
            
            [Required]
            [DataType(DataType.Password)]
            public string Password { get; set; }

            public bool IsActive { get; set; }
        }
    }
````

### Attributes

You can set some of the attributes on your c# property, or directly on html tag. If you are going to use this property in a [jellog-dynamic-form](Dynamic-forms.md), then you can only set these properties via property attributes.

#### Property Attributes

- `[TextArea()]`: Converts the input into a text area.

* `[Placeholder()]`: Sets placeholder for input. You can use a localization key directly.
* `[InputInfoText()]`: Sets a small info text for input. You can use a localization key directly.
* `[FormControlSize()]`: Sets size of form-control wrapper element. Available values are
  -  `JellogFormControlSize.Default`
  -  `JellogFormControlSize.Small`
  -  `JellogFormControlSize.Medium`
  -  `JellogFormControlSize.Large`
* `[DisabledInput]` :  Input is disabled.
* `[ReadOnlyInput]`: Input is read-only.

#### Tag Attributes

* `info`: Sets a small info text for input. You can use a localization key directly.
* `auto-focus`: If true, browser auto focuses on the element.
* `size`: Sets size of form-control wrapper element. Available values are
  - `JellogFormControlSize.Default`
  - `JellogFormControlSize.Small`
  - `JellogFormControlSize.Medium`
  - `JellogFormControlSize.Large`
* `disabled`: Input is disabled.
* `readonly`: Input is read-only.
* `label`: Sets the label for input.
* `display-required-symbol`: Adds the required symbol (*) to label if input is required. Default `True`.

`asp-format`, `name` and `value` attributes of [Asp.Net Core Input Tag Helper](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/working-with-forms?view=aspnetcore-3.1#the-input-tag-helper) are also valid for `jellog-input` tag helper.

### Label & Localization

You can set label of your input in different ways:

- You can use `Label` attribute and directly set the label. But it doesn't auto localize your localization key. So use it as `label="@L["{LocalizationKey}"].Value"`.
- You can set it using `[Display(name="{LocalizationKey}")]` attribute of Asp.Net Core.
- You can just let **jellog** find the localization key for the property. It will try to find "DisplayName:{PropertyName}" or "{PropertyName}" localization keys, if `label` or `[DisplayName]` attributes are not set.

## jellog-select

`jellog-select` tag creates a Bootstrap form select for a given c# property. It uses [Asp.Net Core Select Tag Helper](https://docs.microsoft.com/tr-tr/aspnet/core/mvc/views/working-with-forms?view=aspnetcore-3.1#the-select-tag-helper) in background, so every data annotation attribute of `select` tag helper of Asp.Net Core is also valid for `jellog-select`.

`jellog-select` tag needs a list of `Microsoft.AspNetCore.Mvc.Rendering.SelectListItem ` to work. It can be provided by `asp-items` attriube on the tag or `[SelectItems()]` attribute on c# property. (if you are using [jellog-dynamic-form](Dynamic-forms.md), c# attribute is the only way.)

`jellog-select` supports multiple selection.

`jellog-select` auto-creates a select list for **Enum** properties. No extra data is needed. If property is nullable, an empty key and value is added to top of the auto-generated list.

Usage:

````xml
<jellog-select asp-for="@Model.MyModel.City" asp-items="@Model.CityList"/>

<jellog-select asp-for="@Model.MyModel.AnotherCity"/>

<jellog-select asp-for="@Model.MyModel.MultipleCities" asp-items="@Model.CityList"/>

<jellog-select asp-for="@Model.MyModel.MyCarType"/>

<jellog-select asp-for="@Model.MyModel.MyNullableCarType"/>
````

Model:

````csharp
 public class FormElementsModel : PageModel
    {
        public SampleModel MyModel { get; set; }
                    
        public List<SelectListItem> CityList { get; set; }

        public void OnGet()
        {
            MyModel = new SampleModel();
            
            CityList = new List<SelectListItem>
            {
                new SelectListItem { Value = "NY", Text = "New York"},
                new SelectListItem { Value = "LDN", Text = "London"},
                new SelectListItem { Value = "IST", Text = "Istanbul"},
                new SelectListItem { Value = "MOS", Text = "Moscow"}
            };
        }

        public class SampleModel
        {
            public string City { get; set; }
            
            [SelectItems(nameof(CityList))]
            public string AnotherCity { get; set; }

            public List<string> MultipleCities { get; set; }
            
            public CarType MyCarType { get; set; }

            public CarType? MyNullableCarType { get; set; }
        }
        
        public enum CarType
        {
            Sedan,
            Hatchback,
            StationWagon,
            Coupe
        }
    }
````

### Attributes

You can set some of the attributes on your c# property, or directly on html tag. If you are going to use this property in a [jellog-dynamic-form](Dynamic-forms.md), then you can only set these properties via property attributes.

#### Property Attributes

* `[SelectItems()]`: Sets the select data. Parameter should be the name of the data list. (see example above)

- `[InputInfoText()]`: Sets a small info text for input. You can use a localization key directly.
- `[FormControlSize()]`: Sets size of form-control wrapper element. Available values are
  - `JellogFormControlSize.Default`
  - `JellogFormControlSize.Small`
  - `JellogFormControlSize.Medium`
  - `JellogFormControlSize.Large`

#### Tag Attributes

- `asp-items`: Sets the select data. This Should be a list of SelectListItem.
- `info`: Sets a small info text for input. You can use a localization key directly.
- `size`: Sets size of form-control wrapper element. Available values are
  - `JellogFormControlSize.Default`
  - `JellogFormControlSize.Small`
  - `JellogFormControlSize.Medium`
  - `JellogFormControlSize.Large`
- `label`: Sets the label for input.
- `display-required-symbol`: Adds the required symbol (*) to label if input is required. Default `True`.

### Label & Localization

You can set label of your input in different ways:

- You can use `Label` attribute and directly set the label. But it doesn't auto localize your localization key. So use it as `label="@L["{LocalizationKey}"].Value".`
- You can set it using `[Display(name="{LocalizationKey}")]` attribute of Asp.Net Core.
- You can just let **jellog** find the localization key for the property. It will try to find "DisplayName:{PropertyName}" or "{PropertyName}" localization keys.

Localizations of combobox values are set by `jellog-select` for **Enum** property. It searches for "{EnumTypeName}.{EnumPropertyName}" or "{EnumPropertyName}" localization keys. For instance, in the example above, it will use "CarType.StationWagon" or "StationWagon" keys for localization when it localizes combobox values.

## jellog-radio

`jellog-radio` tag creates a Bootstrap form radio group for a given c# property. Usage is very similar to `jellog-select` tag.

Usage:

````xml
<jellog-radio asp-for="@Model.MyModel.CityRadio" asp-items="@Model.CityList" inline="true"/>

<jellog-radio asp-for="@Model.MyModel.CityRadio2"/>
````

Model:

````csharp
 public class FormElementsModel : PageModel
    {
        public SampleModel MyModel { get; set; }

        public List<SelectListItem> CityList { get; set; } = new List<SelectListItem>
        {
            new SelectListItem { Value = "NY", Text = "New York"},
            new SelectListItem { Value = "LDN", Text = "London"},
            new SelectListItem { Value = "IST", Text = "Istanbul"},
            new SelectListItem { Value = "MOS", Text = "Moscow"}
        };
        
        public void OnGet()
        {
            MyModel = new SampleModel();
            MyModel.CityRadio = "IST";
            MyModel.CityRadio2 = "MOS";
        }

        public class SampleModel
        {
            public string CityRadio { get; set; }
            
            [SelectItems(nameof(CityList))]
            public string CityRadio2 { get; set; }
        }
    }
````

### Attributes

You can set some of the attributes on your c# property, or directly on html tag. If you are going to use this property in a [jellog-dynamic-form](Dynamic-forms.md), then you can only set these properties via property attributes.

#### Property Attributes

- `[SelectItems()]`: Sets the select data. Parameter should be the name of the data list. (see example above)

#### Tag Attributes

- `asp-items`: Sets the select data. This Should be a list of SelectListItem.
- `Inline`: If true, radio buttons will be in single line, next to each other. If false, they will be under each other.
