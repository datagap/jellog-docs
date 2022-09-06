# SMS Sending

The JELLOG Framework provides an abstraction to sending SMS. Having such an abstraction has some benefits;

- You can then **easily change** your SMS sender without changing your application code.
- If you want to create **reusable application modules**, you don't need to make assumption about how the SMS are sent.

## Installation

It is suggested to use the [JELLOG CLI](CLI.md) to install this package.

### Using the JELLOG CLI

Open a command line window in the folder of the project (.csproj file) and type the following command:

```bash
jellog add-package DataGap.Jellog.Sms
```

### Manual Installation

If you want to manually install;

1. Add the [DataGap.Jellog.Sms](https://www.nuget.org/packages/DataGap.Jellog.Sms) NuGet package to your project:

```
Install-Package DataGap.Jellog.Sms
```

2. Add the `JellogSmsModule` to the dependency list of your module:

```csharp
[DependsOn(
    //...other dependencies
    typeof(JellogSmsModule) //Add the new module dependency
    )]
public class YourModule : JellogModule
{
}
```

## Sending SMS

[Inject](Dependency-Injection.md) the `ISmsSender` into any service and use the `SendAsync` method to send a SMS.

**Example:**

```csharp
using System.Threading.Tasks;
using DataGap.Jellog.DependencyInjection;
using DataGap.Jellog.Sms;

namespace MyProject
{
    public class MyService : ITransientDependency
    {
        private readonly ISmsSender _smsSender;

        public MyService(ISmsSender smsSender)
        {
            _smsSender = smsSender;
        }

        public async Task DoItAsync()
        {
            await _smsSender.SendAsync(
                "+012345678901",        // target phone number
                "This is test sms..."   // message text
            );
        }
    }
}
```

The given `SendAsync` method in the example is an extension method to send an SMS with primitive parameters. In addition, you can pass an `SmsMessage` object which has the following properties:

- `PhoneNumber` (`string`): Target phone number
- `Text` (`string`): Message text
- `Properties` (`Dictionary<string, string>`): Key-value pairs to pass custom arguments

## NullSmsSender

`NullSmsSender` is a the default implementation of the `ISmsSender`. It writes SMS content to the [standard logler](Logging.md), rather than actually sending the SMS.

This class can be useful especially in development time where you generally don't want to send real SMS. **However, if you want to actually send SMS, you should implement the `ISmsSender` in your application code.**

## Implementing the ISmsSender

You can easily create your SMS sending implementation by creating a class that implements the `ISmsSender` interface, as shown below:

```csharp
using System.IO;
using System.Threading.Tasks;
using DataGap.Jellog.Sms;
using DataGap.Jellog.DependencyInjection;

namespace JellogDemo
{
    public class MyCustomSmsSender : ISmsSender, ITransientDependency
    {
        public async Task SendAsync(SmsMessage smsMessage)
        {
            // Send sms
        }
    }
}
```

## More

[JELLOG Commercial](https://commercial.jellog.io/) provides Twilio integration package to send SMS over [Twilio service](https://docs.jellog.io/en/commercial/latest/modules/twilio-sms).
