# Preview Releases

The preview versions are released **~4 weeks before** releasing a major or feature version of the JELLOG Framework. They are released for developers to try and provide feedback to have more stable versions.

Versioning of a preview release is like that:

* 3.1.0-rc.1
* 4.0.0-rc.1

More than one preview releases (like 3.1.0-rc.2 and 3.1.0-rc.3) might be published until the stable version (like 3.1.0).

## Using the Preview Versions

### New Solutions

To create a project for testing the preview version, you can select the "**preview**" option on the [download page](https://jellog.io/get-started) or use the "**--preview**" parameter with the [JELLOG CLI](CLI.md) new command:

````bash
jellog new Acme.BookStore --preview
````

This command will create a new project using the latest preview NuGet packages, NPM packages and the solution template. Whenever the stable version is released, you can switch to the stable version for your solution using the `jellog switch-to-stable` command in the root folder of your solution.

### Existing Solutions

If you already have a solution and want to use/test the latest preview version, use the following [JELLOG CLI](CLI.md) command in the root folder of your solution.

````bash
jellog switch-to-preview
````

You can return back to the latest stable using the `jellog switch-to-stable ` command later.

````bash
jellog switch-to-stable
````

## Providing Feedback

You can open an issue on the [GitHub repository](https://github.com/jellogframework/jellog/issues/new), if you find a bug or want to provide any kind of feedback.
