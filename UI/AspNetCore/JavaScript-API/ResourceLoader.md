# ASP.NET Core MVC / Razor Pages UI: JavaScript Resource Loader API

`jellog.ResourceLoader` is a service that can load a JavaScript or CSS file on demand. It guarantees to load the file only once even if you request multiple times.

## Loading Script Files

`jellog.ResourceLoader.loadScript(...)` function **loads** a JavaScript file from the server and **executes** it.

**Example: Load a JavaScript file**

````js
jellog.ResourceLoader.loadScript('/Pages/my-script.js');
````

### Parameters

`loadScript` function can get three parameters;

* `url` (required, `string`): The URL of the script file to be loaded.
* `loadCallback` (optional, `function`): A callback function that is called once the script is loaded & executed. In this callback you can safely use the code in the script file. This callback is called even if the file was loaded before.
* `failCallback` (optional, `function`): A callback function that is called if loading the script fails.

**Example: Provide the `loadCallback` argument**

````js
jellog.ResourceLoader.loadScript('/Pages/my-script.js', function() {
  console.log('successfully loaded :)');
});
````

## Loading Style Files

`jellog.ResourceLoader.loadStyle(...)` function adds a `link` element to the `head` of the document for the given URL, so the CSS file is automatically loaded by the browser.

**Example: Load a CSS file**

````js
jellog.ResourceLoader.loadStyle('/Pages/my-styles.css');
````

