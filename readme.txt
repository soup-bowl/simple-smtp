=== WordPress Simple SMTP ===
Contributors: soupbowl
Tags: mail,email,smtp,dispatch,sender
Requires at least: 4.9
Tested up to: 5.6
Requires PHP: 7.0
Stable tag: 1.0.2
License: MIT

Adds a simple mail configuration panel into your WordPress installation. Supports logging and config variables.

== Description ==
Adds a simple, no-fuss SMTP settings to your WordPress installation that lets you define custom settings, which is especially useful for hosts with no control over the php `mail` functionality.

The log & resend functionality currently **does not support attachments**.

## Environment and constant overriding (optional)
This plugin will prefer environmental and constant-stored values over the plugin-saved equivalent settings, making it easier to use this plugin via deployment.

These can be either stored in your systems env setup, or in wp-config.php as `define( 'SEE_BELOW', 'your_value_here' );`.

### Accepted Parameters
* `SMTP_HOST` (string) Mail server hostname.
* `SMTP_PORT` (integer) Port address (usually 25, 465 or 587).
* `SMTP_AUTH` (integer, 1 or 0) Pass below credentials to your mail server.
* `SMTP_USER` (string) The mail username for this account.
* `SMTP_PASS` (string) The password for the mailer account.
* `SMTP_FROM` (string) Enforce all emails come from this email address.
* `SMTP_FROMNAME` (string) Enforce all emails to have a certain email name.
* `SMTP_SEC` (string) Use a particular email security method (accepts 'def' (default), 'ssl' and 'tls').
* `SMTP_NOVERIFYSSL` (boolean) Disable validation of the SMTP server certificate (not recommended).
* `SMTP_LOG` (boolean) Controls the logging capability and visibility.

It is recommended to store at least `SMTP_PASS` in your wp-config.php file (with the correct file permissions set). If the openssl extension is available, the plugin will attempt to encrypt the password in the database.

== Frequently Asked Questions ==
= How do I fix SMTP errors? =
This plugin works by instructing **PHPMailer** - the mail library WordPress have chosen - to use SMTP mode, and adds in the settings you choose. 9 times out of 10, the error messages you receive are configuration errors. PHPMailer provides a good guide to help you figure out these problems.

[Troubleshooting - PHPMailer](https://github.com/PHPMailer/PHPMailer/wiki/Troubleshooting).

The one instance where an SMTP error can be caused by this plugin is if the SMTP password is stored in the database when the **secret keys** have been regenerated. You will need to re-save the password to refresh the encryption keys.

You can always get assistance from your host and/or SMTP service provider.

= One or more of the settings are greyed out =
This plugin supports being overridden by DEFINE, so please check to see that you are not setting a define for a WP Simple SMTP option. These are most commonly stored in the wp-config.php file.

= How is the SMTP password stored? = 
If openssl is available to PHP, then the password will be **encrypted** ([not hashed](https://stackoverflow.com/a/4948393)) when stored in the database. If unavailable, the SMTP password will be saved into the database as **plaintext**. The more recommended way of storing the password is to define SMTP_PASS in your wp-config.php file, which should already be locked and inaccessible from the front-end.

= Does this plugin work on WordPress Multisite? =
Yes. Each site can have unique settings, unless overriding is on. The network will use the main site settings, so network admin emails will show up in the main site log. More multisite related functionality will be added.

= Can I report an issue, or contribute to development? =
Yes! [Please see our GitHub repository here](https://github.com/soup-bowl/wp-simple-smtp) for writing issues and/or making pull requests.

== Changelog ==
= Next =
* New: Key change detection when SMTP password encryption is used, to warn user the email dispatch may fail ([#28](https://github.com/soup-bowl/wp-simple-smtp/issues/28)).
* Change: Custom HTML removed in favour of translatable HTML test email. Thanks to [Kebbet](https://github.com/kebbet) for implementation ([#26](https://github.com/soup-bowl/wp-simple-smtp/issues/26)).
* Fix: JavaScript error when viewing emails ([#24](https://github.com/soup-bowl/wp-simple-smtp/issues/24)).

= 1.0.2 =
* Fix: Quick config translations not loading, and missing i18n entities. Thanks [Kebbet](https://github.com/kebbet) ([#21](https://github.com/soup-bowl/wp-simple-smtp/issues/21)).
* Fix: Incorrect pagination if the log count was divisible by 5. Thanks [Kebbet](https://github.com/kebbet) ([#18](https://github.com/soup-bowl/wp-simple-smtp/issues/18)).

= 1.0.1 =
* Fix: Text-domain mismatch causing translations not to load in correctly. Thank you to [Kebbet](https://github.com/kebbet) for the fix ([#19](https://github.com/soup-bowl/wp-simple-smtp/issues/19)).

= 1.0.0 =
* Bumped version to 1.0.0. Application will follow [Semantic Versioning](https://semver.org/) ongoing. ([#15](https://github.com/soup-bowl/wp-simple-smtp/issues/15)).

= 0.3.6 =
* SMTPSecure is now a configurable option ([#11](https://github.com/soup-bowl/wp-simple-smtp/issues/11)).
* Log entries can now be deleted ([#13](https://github.com/soup-bowl/wp-simple-smtp/issues/13)).

= 0.3.5 =
* When openssl is available, the password stored in the database will be encrypted.
* Added a quick configuration option, to guide SMTP setup (less Googling).

= 0.3.4 =
* Confirmed working with WordPress 5.5.1.
* Added option to disable SSL verification.
* Multiple emails can be used in the test functionality.

= 0.3.3 =
* Independent log tables deprecated for CPT.

= 0.3.2 =
* Changed display format of email log.
* Limit resent emails to hourly.

= 0.3.1 =
* Table is created or deleted upon plugin state change.

= 0.3 =
* Changes to test emails.
* Log view changed depending on header.

= 0.2 =
* SMTP error logging.
* View and resend emails.
* Test email settings.

= 0.1 =
* SMTP configuration handling (overrides `mail()`).
* Optional SMTP logging (basic functionality).
