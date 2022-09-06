# Breadcrumbs

## Introduction

`jellog-breadcrumb` is the main container for breadcrumb items. 

Basic usage:

````html
<jellog-breadcrumb>
    <jellog-breadcrumb-item href="#" title="Home" />
    <jellog-breadcrumb-item href="#" title="Library"/>
    <jellog-breadcrumb-item title="Page"/>
</jellog-breadcrumb>
````

## Demo

See the [breadcrumbs demo page](https://bootstrap-taghelpers.jellog.io/Components/Breadcrumbs) to see it in action.

## jellog-breadcrumb-item Attributes

- **title**: Sets the text of the breadcrumb item.
- **active**: Sets the active breadcrumb item. Last item is active by default, if no other item is active.
- **href**: A value indicates if an `jellog-breadcrumb-item` has a link. Should be a string link value. 
