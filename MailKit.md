# MailKit Integration

[MailKit](http://www.mimekit.net/) is a cross-platform, popular open source mail client library for .net. JELLOG Framework provides an integration package to use the MailKit as the [email sender](Emailing.md).

## Installation

It is suggested to use the [JELLOG CLI](CLI.md) to install this package. Open a command line window in the folder of the project (.csproj file) and type the following command:

````bash
jellog add-package DataGap.Jellog.MailKit
````

If you haven't done it yet, you first need to install the JELLOG CLI. For other installation options, see [the package description page](https://jellog.io/package-detail/DataGap.Jellog.MailKit).

## Sending Emails

### IEmailSender

[Inject](Dependency-Injection.md) the standard `IEmailSender` into any service and use the `SendAsync` method to send emails. See the [email sending document](Emailing.md) for details.

> `IEmailSender` is the suggested way to send emails even if you use MailKit, since it makes your code provider independent.

### IMailKitSmtpEmailSender

MailKit package also exposes the `IMailKitSmtpEmailSender` service that extends the `IEmailSender` by adding the `BuildClientAsync()` method. This method can be used to obtain a `MailKit.Net.Smtp.SmtpClient` object that can be used to perform MailKit specific operations.

## Configuration

MailKit integration package uses the same settings defined by the email sending system. So, refer to the [email sending document](Emailing.md) for the settings.

In addition to the standard settings, this package defines `JellogMailKitOptions` as a simple [options](Options.md) class. This class defines only one options:

* **SecureSocketOption**: Used to set one of the `SecureSocketOptions`. Default: `null` (uses the defaults).

**Example: Use *SecureSocketOptions.SslOnConnect***

````csharp
Configure<JellogMailKitOptions>(options =>
{
    options.SecureSocketOption = SecureSocketOptions.SslOnConnect;
});
````

Refer to the [MailKit documentation](http://www.mimekit.net/) to learn more about this option.

## See Also

* [Email sending](Emailing.md)