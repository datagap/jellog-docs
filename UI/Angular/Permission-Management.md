# Permission Management

A permission is a simple policy that is granted or prohibited for a particular user, role or client. You can read more about [authorization in JELLOG](../../Authorization.md) document.

You can get permission of authenticated user using `getGrantedPolicy` or `getGrantedPolicy$` method of `PermissionService`.

You can get permission as boolean value:

```js
import { PermissionService } from '@jellog/ng.core';

export class YourComponent {
  constructor(private permissionService: PermissionService) {}

  ngOnInit(): void {
    const canCreate = this.permissionService.getGrantedPolicy('JellogIdentity.Roles.Create');
  }
}
```

You may also **combine policy keys** to fine tune your selection:

```js
// this.permissionService is instance of PermissionService

const hasIdentityAndAccountPermission = this.permissionService.getGrantedPolicy(
  "Jellog.Identity && Jellog.Account"
);

const hasIdentityOrAccountPermission = this.permissionService.getGrantedPolicy(
  "Jellog.Identity || Jellog.Account"
);
```

Please consider the following **rules** when creating your permission selectors:

- Maximum 2 keys can be combined.
- `&&` operator looks for both keys.
- `||` operator looks for either key.
- Empty string `''` as key will return `true`
- Using an operator without a second key will return `false`

## Permission Directive

You can use the `PermissionDirective` to manage visibility of a DOM Element accordingly to user's permission.

```html
<div *jellogPermission="'JellogIdentity.Roles'">
  This content is only visible if the user has 'JellogIdentity.Roles' permission.
</div>
```

As shown above you can remove elements from DOM with `jellogPermission` structural directive.

## Permission Guard

You can use `PermissionGuard` if you want to control authenticated user's permission to access to the route during navigation.

* Import the PermissionGuard from @jellog/ng.core.
* Add `canActivate: [PermissionGuard]` to your route object.
* Add `requiredPolicy` to the `data` property of your route in your routing module.

```js
import { PermissionGuard } from '@jellog/ng.core';
// ...
const routes: Routes = [
  {
    path: 'path',
    component: YourComponent,
    canActivate: [PermissionGuard],
    data: {
        requiredPolicy: 'YourProjectName.YourComponent', // policy key for your component
    },
  },
];
```

## Customization

In some cases, a custom permission management may be needed. All you need to do is to replace the service with your own. Here is how to achieve this:

- First, create a service of your own. Let's call it `CustomPermissionService` and extend `PermissionService` from `@jellog/ng.core` as follows:

```js
import { ConfigStateService, PermissionService } from '@jellog/ng.core';
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class CustomPermissionService extends PermissionService {
  constructor(configStateService: ConfigStateService) {
    super(configStateService);
  }

  // This is an example to show how to override the methods
  getGrantedPolicy$(key: string) {
    return super.getGrantedPolicy$(key);
  }
}
```

- Then, in `app.module.ts`, provide this service as follows: 

```js
@NgModule({
  // ...
  providers: [
    // ...
    {
      provide: PermissionService,
      useExisting: CustomPermissionService,
    },
  ],
  // ...
})
export class AppModule {}
```

That's it. Now, when a directive/guard asks for `PermissionService` from angular, it will inject your service.
