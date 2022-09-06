# JELLOG.IO Platform 4.4 Final Has Been Released!

[JELLOG Framework](https://jellog.io/) and [JELLOG Commercial](https://commercial.jellog.io/) 4.4 versions have been released today.

## What's New With 4.4?

Since all the new features are already explained in details with the 4.4 RC announcement posts, I will not repeat all the details again. See [the related blog post](https://blog.jellog.io/jellog/JELLOG-Platform-4-4-RC-Has-Been-Released) for all the features and enhancements.

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

## The Road Map

The next feature version will be 5.0. It is planned to release the 5.0 RC (Release Candidate) in November 2021. See the updated road maps;

* [JELLOG Framework Road Map](https://docs.jellog.io/en/jellog/latest/Road-Map)
* [JELLOG Commercial Road Map](https://docs.jellog.io/en/commercial/latest/road-map)