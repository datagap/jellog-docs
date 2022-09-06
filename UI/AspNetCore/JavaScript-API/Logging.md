# ASP.NET Core MVC / Razor Pages UI: JavaScript Logging API

`jellog.log` API is used to write simple logs in the client side.

> The logs are written to console, using the `console.log`, by default.

> This document is for simple client side logging. See the [Logging](../../../Logging.md) document for server side logging system.

## Basic Usage

Use one of the `jellog.log.xxx(...)` methods based on the severity of your log message.

````js
jellog.log.debug("Some debug log here..."); //Logging a simple debug message
jellog.log.info({ name: "john", age: 42 }); //Logging an object as an information log
jellog.log.warn("A warning message"); //Logging a warning message
jellog.log.error('An error happens...'); //Error message
jellog.log.fatal('Network connection has gone away!'); //Fatal error
````

## Log Levels

There are 5 levels for a log message:

* DEBUG = 1
* INFO = 2
* WARN = 3
* ERROR = 4
* FATAL = 5

These are defined in the `jellog.log.levels` object (like `jellog.log.levels.WARN`).

### Changing the Current Log Level

You can control the log level as shown below:

````js
jellog.log.level = jellog.log.levels.WARN;
````

Default log level is `DEBUG`.

### Logging with Specifying the Level

Instead of calling `jellog.log.info(...)` function, you can use the `jellog.log.log` by specifying the log level as a parameter:

````js
jellog.log.log("log message...", jellog.log.levels.INFO);
````

