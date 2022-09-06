# Navs

## Introduction

`jellog-nav` is the basic tag helper component derived from bootstrap nav element.

Basic usage:

````html
<jellog-nav nav-style="Pill" align="Center">
    <jellog-nav-item>
<a jellog-nav-link active="true" href="#">Active</a>
    </jellog-nav-item>
    <jellog-nav-item>
<a jellog-nav-link href="#">Longer nav link</a>
    </jellog-nav-item>
    <jellog-nav-item>
<a jellog-nav-link href="#">link</a>
    </jellog-nav-item>
    <jellog-nav-item>
<a jellog-nav-link disabled="true" href="#">disabled</a>
    </jellog-nav-item>
</jellog-nav>
````

## Demo

See the [navs demo page](https://bootstrap-taghelpers.jellog.io/Components/Navs) to see it in action.

## jellog-nav Attributes

- **nav-style**:  The value indicates the positioning and style of the containing items. Should be one of the following values: 
  * `Default` (default value)
  * `Vertical`
  * `Pill`
  * `PillVertical`
- **align:** The value indicates the alignment of the containing items: 
  * `Default` (default value)
  * `Start`
  * `Center`
  * `End`

### jellog-nav-bar Attributes

- **nav-style**:  The value indicates the color layout of the base navigation bar. Should be one of the following values: 
  * `Default` (default value)
  * `Dark`
  * `Light`
  * `Dark_Primary`
  * `Dark_Secondary`
  * `Dark_Success`
  * `Dark_Danger`
  * `Dark_Warning`
  * `Dark_Info`
  * `Dark_Dark`
  * `Dark_Link`
  * `Light_Primary`
  * `Light_Secondary`
  * `Light_Success`
  * `Light_Danger`
  * `Light_Warning`
  * `Light_Info`
  * `Light_Dark`
  * `Light_Link`
- **size:** The value indicates size of the base navigation bar. Should be one of the following values: 
  * `Default` (default value)
  * `Sm`
  * `Md`
  * `Lg`
  * `Xl`

### jellog-nav-item Attributes

**dropdown**: A value that sets the navigation item to be a dropdown menu if provided. Can be one of the following values: 

* `false` (default value)
* `true`

Example:

````html
<jellog-nav-bar size="Lg" navbar-style="Dark_Warning">
    <a jellog-navbar-brand href="#">Navbar</a>
    <jellog-navbar-toggle>
        <jellog-navbar-nav>
            <jellog-nav-item active="true">
                <a jellog-nav-link href="#">Home <span class="sr-only">(current)</span></a>
            </jellog-nav-item>
            <jellog-nav-item>
                <a jellog-nav-link href="#">Link</a>
            </jellog-nav-item>
            <jellog-nav-item dropdown="true">
                <jellog-dropdown>
                    <jellog-dropdown-button nav-link="true" text="Dropdown" />
                    <jellog-dropdown-menu>
                        <jellog-dropdown-header>Dropdown header</jellog-dropdown-header>
                        <jellog-dropdown-item href="#" active="true">Action</jellog-dropdown-item>
                        <jellog-dropdown-item href="#" disabled="true">Another disabled action</jellog-dropdown-item>
                        <jellog-dropdown-item href="#">Something else here</jellog-dropdown-item>
                        <jellog-dropdown-divider />
                        <jellog-dropdown-item href="#">Separated link</jellog-dropdown-item>
                    </jellog-dropdown-menu>
                </jellog-dropdown>
            </jellog-nav-item>
            <jellog-nav-item>
                <a jellog-nav-link disabled="true" href="#">Disabled</a>
            </jellog-nav-item>
        </jellog-navbar-nav>            
        <span jellog-navbar-text>
          Sample Text
        </span>
    </jellog-navbar-toggle>
</jellog-nav-bar>
````
