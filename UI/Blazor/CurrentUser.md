# Blazor UI: Current User

`ICurrentUser` service is used to obtain information about the currently authenticated user. Inject the `ICurrentUser` into any component/page and use its properties and methods.

**Example: Show username & email on a page**

````csharp
@page "/"
@using DataGap.Jellog.Users
@inject ICurrentUser CurrentUser
@if (CurrentUser.IsAuthenticated)
{
    <p>Welcome @CurrentUser.UserName</p>
}
````

> If you (directly or indirectly) derived your component from the `JellogComponentBase`, you can directly use the base `CurrentUser` property.

`ICurrentUser` provides `Id`, `Name`, `SurName`, `Email`, `Roles` and some other properties.

> See the [Server Side Current User](../../CurrentUser) service for more information.

