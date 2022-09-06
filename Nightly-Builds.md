# Nightly Builds

All framework & module packages are deployed to MyGet every night in weekdays. So, you can install the latest dev-brach builds to try out functionality prior to release.

## Install & Uninstall Nightly Preview Packages

The latest version of nightly preview packages can be installed by the running below command in the root folder of the application:

```bash
jellog switch-to-nightly 
```

> Note that this command doesn't create a project with nightly preview packages. Instead, it switches package versions of a project with the nightly preview packages.

After this command, a new NuGet feed will be added to the `NuGet.Config` file of your project. Then, you can get the latest code of JELLOG Framework without waiting for the next release.

> You can check the [jellog-nightly gallery](https://www.myget.org/gallery/jellog-nightly) to see the all nightly preview packages.

If you're using the JELLOG Framework nightly preview packages, you can switch back to stable version using this command:

```bash
jellog switch-to-stable
```

JELLOG nightly NuGet feed is [https://www.myget.org/F/jellog-nightly/api/v3/index.json](https://www.myget.org/F/jellog-nightly/api/v3/index.json).

See the [JELLOG CLI documentation](./CLI.md) for more information.
