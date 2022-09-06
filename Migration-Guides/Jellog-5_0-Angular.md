# Angular UI v4.x to v5.0 Migration Guide

> This document is for the Angular UI. See also [the main migration guide](Jellog-5_0.md).

## Overall

See the overall list of breaking changes:

- Bootstrap 5 implementation [#10067](https://github.com/jellogframework/jellog/issues/10067)
- Remove NGXS dependency & states [#9952](https://github.com/jellogframework/jellog/issues/9952)
- Install @angular/localize package to startup templates [#10099](https://github.com/jellogframework/jellog/issues/10099)
- Create new secondary entrypoints and move the related proxies to there [#10060](https://github.com/jellogframework/jellog/issues/10060)
- Move SettingTabsService to @jellog/ng.setting-management/config package from @jellog/ng.core [#10061](https://github.com/jellogframework/jellog/issues/10061)
- Make the @jellog/ng.account dependent on @jellog/ng.identity [#10059](https://github.com/jellogframework/jellog/issues/10059)
- Set default jellog-modal size medium [#10118](https://github.com/jellogframework/jellog/issues/10118)
- Update all dependency versions to the latest [#9806](https://github.com/jellogframework/jellog/issues/9806)
- Chart.js big include with CommonJS warning [#7472](https://github.com/jellogframework/jellog/issues/7472)

## Angular v12

The new JELLOG Angular UI is based on Angular v12. We started to compile Angular UI packages with the Ivy compilation. Therefore, **new packages only work with Angular v12**. If you are still on the older version of Angular v12, you have to update to Angular v12. The update is usually very easy. See [Angular Update Guide](https://update.angular.io/?l=2&v=11.0-12.0) for further information.

> **JELLOG Angular UI is not yet compatible with Angular v13 due to some issues.**

## Bootstrap 5

JELLOG 5.0 now works with Bootstrap 5. For details, please refer to the official [migration guide](https://getbootstrap.com/docs/5.0/migration/) provided by Bootstrap.

We have updated dependencies of the `ThemeShared` package, therefore when you update `@jellog/ng.theme.shared`, it will install the necessary dependencies. 

### RTL

Bootstrap 5 provides its own CSS file for RTL(right-to-left) languages. Therefore, we have removed `bootstrap-rtl.min.css` from `@jellog/ng.theme.shared`.

In angular.json, make the following change:

Replace 

`"node_modules/@jellog/ng.theme.shared/styles/bootstrap-rtl.min.css"` with 

`"node_modules/bootstrap/dist/css/bootstrap.rtl.min.css"`

```js
{
  // ...
    "styles": [{
      "input": "node_modules/bootstrap/dist/css/bootstrap.rtl.min.css",
      "inject": false,
      "bundleName": "bootstrap-rtl.min"
    }]
}
```

That's it for open source templates.

### Commercial

Starting from version 5.0, Lepton styles get bundled with Bootstrap. That's why you don't need to provide `bootstrap` styles in `angular.json` anymore.

Remove the following two objects from the `styles` array in `angular.json`

```js
{
  // ...
    "styles": [{
      "input": "node_modules/@jellog/ng.theme.shared/styles/bootstrap-rtl.min.css",
      "inject": false,
      "bundleName": "bootstrap-rtl.min"
    },
    {
      "input": "node_modules/bootstrap/dist/css/bootstrap.min.css",
      "inject": true,
      "bundleName": "bootstrap-ltr.min"
    }]
}
```

After you have implemented the necessary changes explained by Bootstrap, it should be good to go.

## NGXS has been removed

We aim to make the JELLOG Framework free of any state-management solutions. JELLOG developers should be able to use the JELLOG Framework with any library/framework of their choice. So, we decided to remove NGXS from JELLOG packages.

If you'd like to use NGXS after upgrading to v5.0, you have to install the NGXS to your project. The package can be installed with the following command:

```bash
npm install @ngxs/store

# or

yarn add @ngxs/store
```

NGXS states and actions, some namespaces have been removed. See [this issue](https://github.com/jellogframework/jellog/issues/9952) for the details.

If you don't want to use the NGXS, you should remove all NGXS related imports, injections, etc., from your project.

## @angular/localize package

[`@angular/localize`](https://angular.io/api/localize) dependency has been removed from `@jellog/ng.core` package. The package must be installed in your app. Run the following command to install:

```bash
npm install @angular/localize@12

# or

yarn add @angular/localize@12
```

> JELLOG Angular UI packages are not dependent on the `@angular/localize` package. However, some packages (like `@ng-bootstrap/ng-bootstrap`) depend on the package. Thus, this package needs to be installed in your project.

## Proxy endpoints

New endpoints named proxy have been created, related proxies have moved.
For example; before v5.0, `IdentityUserService` could be imported from `@jellog/ng.identity`. As of v5.0, the service can be imported from `@jellog/ng.identity/proxy`. See an example:

```ts
import { IdentityUserService } from '@jellog/ng.identity/proxy';

@Component({})
export class YourComponent {
  constructor(private identityUserService: IdentityUserService) {}
}
```

Following proxies have been affected:

- `@jellog/ng.account` to `@jellog/ng.account.core/proxy`
- `@jellog/ng.feature-management` to `@jellog/ng.feature-management/proxy`
- `@jellog/ng.identity` to `@jellog/ng.identity/proxy`
- `@jellog/ng.permission-management` to `@jellog/ng.permission-management/proxy`
- `@jellog/ng.tenant-management` to `@jellog/ng.tenant-management/proxy`
- **ProfileService** is deleted from `@jellog/ng.core`. Instead, you can import it from `@jellog/ng.identity/proxy`

## SettingTabsService

**SettingTabsService** has moved from `@jellog/ng.core` to `@jellog/ng.setting-management/config`.

## ChartComponent

[`ChartComponent`](../UI/Angular/Chart-Component.md) has moved from `@jellog/ng.theme.shared` to `@jellog/ng.components/chart.js`. To use the component, you need to import the `ChartModule` to your module as follows:

```ts
import { ChartModule } from '@jellog/ng.components/chart.js';

@NgModule({
  imports: [
    ChartModule,
    // ...
  ],
  // ...
})
export class YourFeatureModule {}
```
