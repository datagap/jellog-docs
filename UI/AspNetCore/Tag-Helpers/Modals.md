# Modals

> This document explains the details of the `jellog-modal` Tag Helper, which simplifies to build the HTML markup for a modal dialog. Read [that documentation](../Modals.md) to learn how to work with modals.

## Introduction

`jellog-modal` is a main element to create a modal.

Basic usage:

````xml
<jellog-button button-type="Primary" data-toggle="modal" data-target="#myModal">Launch modal</jellog-button>

<jellog-modal centered="true" scrollable="true" size="Large" id="myModal">
   <jellog-modal-header title="Modal title"></jellog-modal-header>
   <jellog-modal-body>
       Woohoo, you're reading this text in a modal!
   </jellog-modal-body>
   <jellog-modal-footer buttons="Close"></jellog-modal-footer>
</jellog-modal>
````

## Demo

See the [modals demo page](https://bootstrap-taghelpers.jellog.io/Components/Modals) to see it in action.

## Attributes

### centered

A value indicates the positioning of the modal. Should be one of the following values:

* `false` (default value)
* `true`

### Scrollable

A value indicates the scrolling of the modal. Should be one of the following values:

* `false` (default value)
* `true`

### size

A value indicates the size of the modal. Should be one of the following values:

* `Default` (default value)
* `Small`
* `Large`
* `ExtraLarge`

### static

A value indicates if the modal will be static. Should be one of the following values:

* `false` (default value)
* `true`

### Additional content

`jellog-modal-footer` can have multiple buttons with alignment option.

Add `@using DataGap.Jellog.AspNetCore.Mvc.UI.Bootstrap.TagHelpers.Modal` to your page.

Example:

````xml
<jellog-button button-type="Primary" data-toggle="modal" data-target="#myModal">Launch modal</jellog-button>

<jellog-modal centered="true" size="Large" id="myModal" static="true">
    <jellog-modal-header title="Modal title"></jellog-modal-header>
    <jellog-modal-body>
        Woohoo, you're reading this text in a modal!
    </jellog-modal-body>
    <jellog-modal-footer buttons="@(JellogModalButtons.Save|JellogModalButtons.Close)" button-alignment="Between"></jellog-modal-footer>
</jellog-modal>
````

### button-alignment

A value indicates the positioning of your modal footer buttons. Should be one of the following values: 

* `Default` (default value)
* `Start`
* `Center`
* `Around`
* `Between`
* `End`
