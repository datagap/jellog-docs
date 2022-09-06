# JELLOG.IO Platform 5.2 Final Has Been Released!

[JELLOG Framework](https://jellog.io/) and [JELLOG Commercial](https://commercial.jellog.io/) 5.2 versions have been released today.

## What's New With 5.2?

Since all the new features are already explained in details with the [5.2 RC Announcement Post](https://blog.jellog.io/jellog/JELLOG.IO-Platform-5-2-RC-Has-Been-Published), I will not repeat all the details again. See the [RC Blog Post](https://blog.jellog.io/jellog/JELLOG.IO-Platform-5-2-RC-Has-Been-Published) for all the features and enhancements.

## Creating New Solutions

You can create a new solution with the JELLOG Framework version 5.2 by either using the `jellog new` command or using the **direct download** tab on the [get started page](https://jellog.io/get-started).

> See the [getting started document](https://docs.jellog.io/en/jellog/latest/Getting-Started) for more.

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

Check [the migration guide](https://docs.jellog.io/en/jellog/5.2/Migration-Guides/Jellog-5_2) for the applications with the version 5.x upgrading to the version 5.2.

## About the Next Version

The next feature version will be 5.3. It is planned to release the 5.3 RC (Release Candidate) on May 03 and the final version on May 31, 2022. You can follow the [release planning here](https://github.com/jellogframework/jellog/milestones).

Please [submit an issue](https://github.com/jellogframework/jellog/issues/new) if you have any problem with this version.
