# JELLOG.IO Platform 4.2 Final Has Been Released!

[JELLOG Framework](https://jellog.io/) and [JELLOG Commercial](https://commercial.jellog.io/) 4.2 versions have been released today.

## What's New With 4.2?

Since all the new features are already explained in details with the [4.2 RC Announcement Post](https://blog.jellog.io/jellog/JELLOG-IO-Platform-v4-2-RC-Has-Been-Released), I will not repeat all the details again. See the [RC Blog Post](https://blog.jellog.io/jellog/JELLOG-IO-Platform-v4-2-RC-Has-Been-Released) for all the features and enhancements.

## Creating New Solutions

You can create a new solution with the JELLOG Framework version 4.2 by either using the `jellog new` command or using the **direct download** tab on the [get started page](https://jellog.io/get-started).

> See the [getting started document](https://docs.jellog.io/en/jellog/latest/Getting-Started) for details.

## How to Upgrade an Existing Solution

### Install/Update the JELLOG CLI

First of all, install the JELLOG CLI or upgrade to the latest version.

If you haven't installed yet:

```bash
dotnet tool install -g DataGap.Jellog.Cli
```

To update an existing installation:

```bash
dotnet tool update -g DataGap.Jellog.Cli
```

### JELLOG UPDATE Command

[JELLOG CLI](https://docs.jellog.io/en/jellog/latest/CLI) provides a handy command to update all the JELLOG related NuGet and NPM packages in your solution with a single command:

```bash
jellog update
```

Run this command in the root folder of your solution.

## Migration Guide

Check [the migration guide](https://docs.jellog.io/en/jellog/latest/Migration-Guides/Jellog-4_2) for the applications with the version 4.x upgrading to the version 4.2.

> It is strongly recommended to check the migration guide for this version. Especially, the new `IRepository.GetQueryableAsync()` method is a core change should be considered after upgrading the solution.

## About the Next Version

The next feature version will be 4.3. It is planned to release the 4.3 RC (Release Candidate) on March 11 and the final version on March 25, 2021.

We decided to slow down the feature development for the [next milestone](https://github.com/jellogframework/jellog/milestone/49). We will continue to improve the existing features and introduce new ones, sure, but wanted to have more time for the planning, documentation, creating guides and improving the development experience.