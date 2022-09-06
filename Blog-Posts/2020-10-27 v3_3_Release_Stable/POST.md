# JELLOG Framework & JELLOG Commercial 3.3 Final Have Been Released

JELLOG Framework & JELLOG Commercial 3.3.0 have been released today.

Since all the new features are already explained in details with the [3.3 RC Announcement Post](https://blog.jellog.io/jellog/JELLOG-Framework-JELLOG-Commercial-v3.3-RC-Have-Been-Released), I will not repeat all the details again. Please read [the RC post](https://blog.jellog.io/jellog/JELLOG-Framework-JELLOG-Commercial-v3.3-RC-Have-Been-Released) for **new feature and changes** you may need to do for your solution while upgrading to the version 3.3.

## Creating New Solutions

You can create a new solution with the JELLOG Framework version 3.3 by either using the `jellog new` command or using the **direct download** tab on the [get started page](https://jellog.io/get-started).

> See the [getting started document](https://docs.jellog.io/en/jellog/latest/Getting-Started) for details.

## How to Upgrade an Existing Solution

### Install/Update the JELLOG CLI

First of all, install the JELLOG CLI or upgrade to the latest version.

If you haven't installed yet:

````bash
dotnet tool install -g DataGap.Jellog.Cli
````

To update an existing installation:

```bash
dotnet tool update -g DataGap.Jellog.Cli
```

### JELLOG UPDATE Command

[JELLOG CLI](https://docs.jellog.io/en/jellog/latest/CLI) provides a handy command to update all the JELLOG related NuGet and NPM packages in your solution with a single command:

````bash
jellog update
````

Run this command in the root folder of your solution. After the update command, check [the RC blog post](https://blog.jellog.io/jellog/JELLOG-Framework-JELLOG-Commercial-v3.3-RC-Have-Been-Released) to learn if you need to make any changes in your solution.

> You may want to see the new [upgrading document](https://docs.jellog.io/en/jellog/latest/Upgrading).

## About the Next Version: 4.0

The next version will be 4.0 and it will be mostly related to completing the Blazor UI features and upgrading the JELLOG Framework & ecosystem to the .NET 5.0.

The goal is to complete the version 4.0 with a stable Blazor UI with the fundamental features implemented and publish it just after the Microsoft lunches .NET 5 in this November. The planned 4.0 preview release date is November 11th.