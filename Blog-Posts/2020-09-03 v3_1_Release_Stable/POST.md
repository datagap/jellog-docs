# JELLOG Framework 3.1 Final Has Been Released

It is exciting for us to announce that we've released the JELLOG Framework & JELLOG Commercial 3.1 today.

Since all the new features are already explained in details with the [3.1 RC Announcement Post](https://blog.jellog.io/jellog/JELLOG-Framework-v3.1-RC-Has-Been-Released), I will not repeat all the details here. Please read [the RC post](https://blog.jellog.io/jellog/JELLOG-Framework-v3.1-RC-Has-Been-Released) for **new feature and changes** you may need to do for your solution while upgrading to the version 3.1.

## Creating New Solutions

You can create a new solution with the JELLOG Framework version 3.1 by either using the `jellog new` command or using the **direct download** tab on the [get started page](https://jellog.io/get-started).

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

After the update command, check [the RC blog post](https://blog.jellog.io/jellog/JELLOG-Framework-v3.1-RC-Has-Been-Released) to learn if you need to make any changes in your solution.

> You may want to see the new [upgrading document](https://docs.jellog.io/en/jellog/latest/Upgrading).

## About the version 3.2

The planned schedule for the version 3.2 is like that;

* **September 17, 2020**: 3.2.0-rc.1 (release candidate)
* **October 1, 2020**: 3.2.0 final (stable)

You can check [the GitHub milestone](https://github.com/jellogframework/jellog/milestone/39) to see the features/issues we are working on.

## JELLOG Community & Articles

We had lunched the [JELLOG Community web site](https://community.jellog.io/) a few weeks before. The core JELLOG team and the JELLOG community have started to create content for the community.

Here, the last three articles from the JELLOG Community:

* [JELLOG Suite: How to Add the User Entity as a Navigation Property of Another Entity](https://community.jellog.io/articles/jellog-suite-how-to-add-the-user-entity-as-a-navigation-property-of-another-entity-furp75ex) by [@ebicoglu](https://github.com/ebicoglu)
* [Reuse JELLOG vNext Modules to Quickly Implement Application Features](https://community.jellog.io/articles/reuse-jellog-vnext-modules-to-quickly-implement-application-features-tdtmwd9w) by [@gdlcf88](https://github.com/gdlcf88)
* [Using DevExtreme Components With the JELLOG Framework](https://community.jellog.io/articles/using-devextreme-components-with-the-jellog-framework-zb8z7yqv) by [@cotur](https://github.com/cotur).

We are looking for your contributions; You can [submit your article](https://community.jellog.io/articles/submit)! We will promote your article to the community.