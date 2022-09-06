# Dapper Integration

Dapper is a light-weight and simple database provider. The major benefit of using Dapper is writing T-SQL queries. It provides  some extension methods for `IDbConnection` interface.

JELLOG does not encapsulate many functions for Dapper. JELLOG Dapper library provides a `DapperRepository<TDbContext>` base class based on  JELLOG EntityFrameworkCore module, which provides the `IDbConnection` and `IDbTransaction` properties required by Dapper.

`IDbConnection` and `IDbTransaction` works well with the [JELLOG Unit-Of-Work](Unit-Of-Work.md).

## Installation

Install and configure EF Core according to [EF Core's integrated documentation](Entity-Framework-Core.md).

`DataGap.Jellog.Dapper` is the main nuget package for the Dapper integration. 

You can find it on NuGet Gallery: https://www.nuget.org/packages/DataGap.Jellog.Dapper

Install it to your project (for a layered application, to your data/infrastructure layer):

```shell
Install-Package DataGap.Jellog.Dapper
```

Then add `JellogDapperModule` module dependency (with `DependsOn` attribute) to your [module](Module-Development-Basics.md):

````C#
using DataGap.Jellog.Dapper;
using DataGap.Jellog.Modularity;

namespace MyCompany.MyProject
{
    [DependsOn(typeof(JellogDapperModule))]
    public class MyModule : JellogModule
    {
        //...
    }
}
````

## Implement Dapper Repository

The following code creates the `PersonRepository`, which requires EF Core's `DbContext` (MyAppDbContext).
You can inject `PersonDapperRepository` to your services for your database operations.

`DbConnection` and `DbTransaction` comes from the `DapperRepository` base class.

```C#
public class PersonDapperRepository : DapperRepository<MyAppDbContext>, ITransientDependency
{
    public PersonDapperRepository(IDbContextProvider<MyAppDbContext> dbContextProvider)
        : base(dbContextProvider)
    {
    }

    public virtual async Task<List<string>> GetAllPersonNames()
    {
        var dbConnection = await GetDbConnectionAsync();
        return (await dbConnection.QueryAsync<string>("select Name from People", transaction:  await GetDbTransactionAsync()))
            .ToList();
    }

    public virtual async Task<int> UpdatePersonNames(string name)
    {
        var dbConnection = await GetDbConnectionAsync();
        return await dbConnection.ExecuteAsync("update People set Name = @NewName", new { NewName = name },
             await GetDbTransactionAsync());
    }
}
```
