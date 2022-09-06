# Tabs

## Introduction

`jellog-tab` is the basic tab navigation content container derived from bootstrap tab element.

Basic usage:

````xml
<jellog-tabs>
    <jellog-tab title="Home">
             Content_Home
    </jellog-tab>
    <jellog-tab-link title="Link" href="#" />
    <jellog-tab title="profile">
            Content_Profile
    </jellog-tab>
    <jellog-tab-dropdown title="Contact" name="ContactDropdown">
        <jellog-tab title="Contact 1" parent-dropdown-name="ContactDropdown">
            Content_1_Content
        </jellog-tab>
        <jellog-tab title="Contact 2" parent-dropdown-name="ContactDropdown">
            Content_2_Content
        </jellog-tab>
    </jellog-tab-dropdown>
</jellog-tabs>
````



## Demo

See the [tabs demo page](https://bootstrap-taghelpers.jellog.io/Components/Tabs) to see it in action.

## jellog-tab Attributes

- **title**: Sets the text of the tab menu.
- **name:** Sets "id" attribute of generated elements. Default value is a Guid. Not needed unless tabs are changed or modified with Jquery.
- **active**: Sets the active tab.

Example:

````xml
<jellog-tabs name="TabId">
    <jellog-tab name="nav-home" title="Home">
        Content_Home
    </jellog-tab>   
    <jellog-tab name="nav-profile" active="true" title="profile">
        Content_Profile
    </jellog-tab>
    <jellog-tab name="nav-contact" title="Contact">
        Content_Contact
    </jellog-tab>
</jellog-tabs>
````

### Pills

Example:

````xml
<jellog-tabs tab-style="Pill">
    <jellog-tab title="Home">
         Content_Home
    </jellog-tab>
    <jellog-tab title="profile">
         Content_Profile
    </jellog-tab>
    <jellog-tab title="Contact">
         Content_Contact
    </jellog-tab>
</jellog-tabs>
````

### Vertical

**vertical-header-size**: Sets the column width of tab headers.

Example:

````xml
<jellog-tabs tab-style="PillVertical" vertical-header-size="_2" >
    <jellog-tab active="true" title="Home">
        Content_Home
    </jellog-tab>   
    <jellog-tab title="profile">
        Content_Profile
    </jellog-tab>
    <jellog-tab title="Contact">
        Content_Contact
    </jellog-tab>
</jellog-tabs>
````
