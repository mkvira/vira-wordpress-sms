=== Vira SMS Login for WordPress ===
Contributors: bcloob
Tags: sms, login, woocommerce, otp, mobile
Requires at least: 6.5
Tested up to: 7.1
Stable tag: 0.4.0
Requires PHP: 7.4
License: GPLv2 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html

Passwordless WordPress login and registration with Iranian mobile numbers and one-time SMS codes. Integrates with IPPanel and works with or without WooCommerce.

== Description ==

Vira SMS Login provides passwordless WordPress login and registration using Iranian mobile numbers and one-time SMS codes. Messages are sent through your own IPPanel account and SMS pattern. When WooCommerce is active, new accounts use the customer role.

Add the login form to a page with this shortcode:

`[vira_sms_login]`

Add a login or account button, for example in a theme header, with:

`[vira_sms_account_button]`

== Features ==

* Sign in and register with an Iranian mobile number and a one-time code.
* Accept Persian and Latin digits and common Iranian phone-number formats.
* Connect to IPPanel SMS patterns and configure pattern parameters.
* Limit code requests and failed verification attempts.
* Work with or without WooCommerce.
* Display a responsive Persian-language interface.

== Installation ==

1. Upload the plugin folder to `wp-content/plugins` and activate it from the Plugins screen.
2. Open **Settings → Vira SMS Login**.
3. Enter the IPPanel service URL, access key, sender number, and pattern code.
4. Create a page and add `[vira_sms_login]` to its content.
5. Optionally configure the login-page and account-page URLs.

An IPPanel account with an active sender number and pattern is required to send messages. SMS charges and service terms are determined by your IPPanel account.

== Frequently Asked Questions ==

= Does the plugin change passwords or disable administrator login? =

No. The plugin does not modify `wp-login.php`. The SMS form is displayed through a shortcode, and redirecting public login links is optional.

= Is an email address required for registration? =

No. Registration uses a mobile number and does not ask the visitor for an email address.

= Is WooCommerce required? =

No. The plugin works without WooCommerce. New accounts use the WordPress subscriber role when WooCommerce is not active.

= What should I check if SMS messages are not delivered? =

Check the service URL, access key, sender number, pattern code, and code parameter name in the plugin settings. Your IPPanel account must be allowed to send using the configured sender number and pattern.

== Privacy ==

When a visitor requests a login code, the mobile number, one-time code, and configured pattern parameters are sent from the site to IPPanel to deliver the SMS. The IPPanel access key is stored in WordPress settings.

The mobile number is used as the WordPress username and stored in the plugin's user metadata. The one-time code is stored as a hash in a temporary WordPress record until it expires. The plugin does not send analytics or visitor tracking data to third-party services.

When the plugin is uninstalled, its settings and temporary data are removed. User accounts and mobile numbers stored on those accounts are not deleted.

== Changelog ==

= 0.4.0 =
* Add a shortcode for the login and account button.
* Improve the login and registration flow, form display, and WooCommerce account compatibility.

= 0.3.1 =
* Previous stable release.
