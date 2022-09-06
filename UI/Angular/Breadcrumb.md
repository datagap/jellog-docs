## Breadcrumb Component

JELLOG provides a component that listens to the angular router's `NavigationEnd`
event and creates inputs for `BreadcrumbItemsComponent`. This component is used in
JELLOG components with [`PageComponent`](./Page-Component.md).

## Breadcrumb Items Component

`BreadcrumbItemsComponent` is used to display breadcrumb items. It can be useful
when you want to display breadcrumb items in a different way than the default.

### Usage

Example of overriding the default template of `PageComponent`:

```html
<jellog-page title="Title">
  <jellog-page-breadcrumb-container>
    <jellog-breadcrumb-items [items]="breadCrumbItems"></jellog-breadcrumb-items>
  </jellog-page-breadcrumb-container>
</jellog-page>
```

```js
import { Component } from "@angular/core";
import { JELLOG } from "@jellog/ng.core";

@Component({
  /* component metadata */
})
export class YourComponent {
  breadCrumbItems: JELLOG.Route[] = [
    {
      name: "Item 1",
    },
    {
      name: "Item 2",
      path: "/path",
    },
  ];
}
```

### Inputs

- items: Partial<JELLOG.Route>[] : Array of JELLOG.Route objects. The source code of JELLOG.Route can be found in [github](https://github.com/jellogframework/jellog/blob/dev/npm/ng-packs/packages/core/src/lib/models/common.ts#L69).

## See Also

- [Page Component](./Page-Component.md)
