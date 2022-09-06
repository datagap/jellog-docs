# JELLOG.IO Platform 5.3 Final Has Been Released!

[JELLOG Framework](https://jellog.io/) and [JELLOG Commercial](https://commercial.jellog.io/) 5.3 versions have been released today.

## What's New With 5.3?

Since all the new features are already explained in details with the [5.3 RC Announcement Post](https://blog.jellog.io/jellog/JELLOG.IO-Platform-5.3-RC-Has-Been-Published), I will not repeat all the details again. See the [RC Blog Post](https://blog.jellog.io/jellog/JELLOG.IO-Platform-5.3-RC-Has-Been-Published) for all the features and enhancements.

## Getting Started with 5.3

### Creating New Solutions

You can create a new solution with the JELLOG Framework version 5.3 by either using the `jellog new` command or using the **direct download** tab on the [get started page](https://jellog.io/get-started).

> See the [getting started document](https://docs.jellog.io/en/jellog/latest/Getting-Started) for more.

### How to Upgrade an Existing Solution

#### Install/Update the JELLOG CLI

First of all, install the JELLOG CLI or upgrade to the latest version.

If you haven't installed it yet:

```bash
dotnet tool install -g DataGap.Jellog.Cli
```

To update an existing installation:

```bash
dotnet tool update -g DataGap.Jellog.Cli
```

#### Upgrading Existing Solutions with the JELLOG Update Command

[JELLOG CLI](https://docs.jellog.io/en/jellog/latest/CLI) provides a handy command to update all the JELLOG related NuGet and NPM packages in your solution with a single command:

```bash
jellog update
```

Run this command in the root folder of your solution.

## Migration Guides

Check the following migration guides for the applications with version 5.2 that are upgrading to version 5.3.

* [JELLOG Framework 5.2 to 5.3 migration guide](https://docs.jellog.io/en/jellog/5.3/Migration-Guides/Jellog-5_3)
* [JELLOG Commercial 5.2 to 5.3 migration guide](https://docs.jellog.io/en/commercial/5.3/migration-guides/v5_3)

## Community News

### New JELLOG Community Posts

Here are some of the recent posts added to the [JELLOG Community](https://community.jellog.io/):

* [Integrating Elsa .NET Workflows with JELLOG Commercial](https://community.jellog.io/posts/integrating-elsa-.net-workflows-with-jellog-commercial-io32k420) by [kirtik](https://community.jellog.io/members/kirtik).
* [JELLOG's Conventional Dependency Injection](https://community.jellog.io/posts/jellogs-conventional-dependency-injection-948toiqy) by [iyilm4z](https://github.com/iyilm4z).
* [How to implement Single Sign-On with JELLOG commercial application](https://community.jellog.io/posts/how-to-implement-single-signon-with-jellog-commercial-application-m5ek38y9) by [kirtik](https://community.jellog.io/members/kirtik).
* [Introduce DTM for Multi-Tenant Multi-Database Scene](https://community.jellog.io/posts/introduce-dtm-for-multitenant-multidatabase-scene-23ziikbe) by [gdlcf88](https://github.com/gdlcf88).

Thanks to the JELLOG Community for all the contents they have published. You can also [post your JELLOG related (text or video) contents](https://community.jellog.io/articles/submit) to the JELLOG Community.

## About the Next Version

The next feature version will be 6.0. It is planned to release the 6.0 RC (Release Candidate) on July 12 and the final version on August 16, 2022. You can follow the [release planning here](https://github.com/jellogframework/jellog/milestones).

Please [submit an issue](https://github.com/jellogframework/jellog/issues/new) if you have any problems with this version.
