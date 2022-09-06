# List Groups

## Introduction

`jellog-list-group` is the main container for list group content. 

Basic usage:

````xml
<jellog-list-group>
    <jellog-list-group-item>Cras justo odio</jellog-list-group-item>
    <jellog-list-group-item>Dapibus ac facilisis in</jellog-list-group-item>
    <jellog-list-group-item>Morbi leo risus</jellog-list-group-item>
    <jellog-list-group-item>Vestibulum at eros</jellog-list-group-item>
</jellog-list-group>
````



## Demo

See the [list groups demo page](https://bootstrap-taghelpers.jellog.io/Components/ListGroup) to see it in action.

## Attributes

### flush

A value indicates `jellog-list-group` items to remove some borders and rounded corners to render list group items edge-to-edge in a parent container. Should be one of the following values:

* `false` (default value)
* `true`

### active

A value indicates if an `jellog-list-group-item` to be active. Should be one of the following values:

* `false` (default value)
* `true`

### disabled

A value indicates if an `jellog-list-group-item` to be disabled. Should be one of the following values:

* `false` (default value)
* `true`

### href

A value indicates if an `jellog-list-group-item` has a link. Should be a string link value. 

### type

A value indicates an `jellog-list-group-item` style class with a stateful background and color. Should be one of the following values:

* `Default` (default value)
* `Primary`
* `Secondary`
* `Success`
* `Danger`
* `Warning`
* `Info`
* `Light`
* `Dark`
* `Link`

### Additional content

`jellog-list-group-item` can also contain additional HTML elements like spans.

Example:

````xml
<jellog-list-group>
    <jellog-list-group-item>Cras justo odio <span jellog-badge-pill="Primary">14</span></jellog-list-group-item>
    <jellog-list-group-item>Dapibus ac facilisis in <span jellog-badge-pill="Primary">2</span></jellog-list-group-item>
    <jellog-list-group-item>Morbi leo risus <span jellog-badge-pill="Primary">1</span></jellog-list-group-item>
</jellog-list-group>
````
