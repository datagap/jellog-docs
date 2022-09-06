# Dropdowns

## Introduction

`jellog-dropdown` is the main container for dropdown content. 

Basic usage:

````xml
<jellog-dropdown>
    <jellog-dropdown-button text="Dropdown button" />
    <jellog-dropdown-menu>
        <jellog-dropdown-item href="#">Action</jellog-dropdown-item>
        <jellog-dropdown-item href="#">Another action</jellog-dropdown-item>
        <jellog-dropdown-item href="#">Something else here</jellog-dropdown-item>
    </jellog-dropdown-menu>
</jellog-dropdown>
````



## Demo

See the [dropdown demo page](https://bootstrap-taghelpers.jellog.io/Components/Dropdowns) to see it in action.

## Attributes

### direction

A value indicates which direction the dropdown buttons will be displayed to. Should be one of the following values:

* `Down` (default value)
* `Up`
* `Right`
* `Left`

### dropdown-style

A value indicates if an `jellog-dropdown-button` will have split icon for dropdown. Should be one of the following values:

* `Single` (default value)
* `Split`



## Menu items

`jellog-dropdown-menu` is the main container for dropdown menu items. 

Basic usage:

````xml
<jellog-dropdown>
    <jellog-dropdown-button button-type="Secondary" text="Dropdown"/>
    <jellog-dropdown-menu>
        <jellog-dropdown-header>Dropdown Header</jellog-dropdown-header>
        <jellog-dropdown-item href="#">Action</jellog-dropdown-item>
        <jellog-dropdown-item active="true" href="#">Active action</jellog-dropdown-item>
        <jellog-dropdown-item disabled="true" href="#">Disabled action</jellog-dropdown-item>
        <jellog-dropdown-divider/>
        <jellog-dropdown-item-text>Dropdown Item Text</jellog-dropdown-item-text>
        <jellog-dropdown-item href="#">Something else here</jellog-dropdown-item>
    </jellog-dropdown-menu>
</jellog-dropdown>
````

## Attributes

### align

A value indicates which direction `jellog-dropdown-menu` items will be aligned to. Should be one of the following values:

* `Left` (default value)
* `Right`

### Additional content

`jellog-dropdown-menu` can also contain additional HTML elements like headings, paragraphs, dividers or form element.

Example:

````xml
<jellog-dropdown >
    <jellog-dropdown-button button-type="Secondary" text="Dropdown With Form"/>
    <jellog-dropdown-menu>
        <form class="px-4 py-3">
            <jellog-input asp-for="EmailAddress"></jellog-input>
            <jellog-input asp-for="Password"></jellog-input>
            <jellog-input asp-for="RememberMe"></jellog-input>
            <jellog-button button-type="Primary" text="Sign In" type="submit" />
        </form>
        <jellog-dropdown-divider></jellog-dropdown-divider>
        <jellog-dropdown-item href="#">New around here? Sign up</jellog-dropdown-item>
        <jellog-dropdown-item href="#">Forgot password?</jellog-dropdown-item>
    </jellog-dropdown-menu>
</jellog-dropdown>
````
