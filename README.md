# Vira SMS Login for WordPress

Passwordless WordPress login and registration with Iranian mobile numbers and one-time SMS codes. The plugin integrates with IPPanel and works with or without WooCommerce.

| | |
| --- | --- |
| Version | 0.4.0 |
| WordPress | 6.5 or later |
| PHP | 7.4 or later |
| License | GPL-2.0-or-later |
| Repository | [mkvira/vira-wordpress-sms](https://github.com/mkvira/vira-wordpress-sms) |

## Features

- Sign in and register with an Iranian mobile number and a one-time code.
- Accept Persian and Latin digits, common number separators, and Iranian country-code prefixes.
- Send codes through an IPPanel SMS pattern with configurable parameters.
- Limit code requests and verification attempts.
- Provide shortcodes for the login form and account link.
- Use the WooCommerce customer role when WooCommerce is active; otherwise use the WordPress subscriber role.
- Keep the front-end form responsive and in Persian.

## Requirements

- WordPress 6.5 or later.
- PHP 7.4 or later.
- An IPPanel account with an active sender number and SMS pattern to send real messages.
- WooCommerce is optional.

## Installation

1. Copy or install this plugin in `wp-content/plugins/vira-wordpress-sms`.
2. Activate **Vira SMS Login** from **Plugins** in the WordPress dashboard.
3. Open **Settings → Vira SMS Login** and enter the IPPanel service URL, access key, sender number, and pattern code.
4. Create a page and add the login form shortcode:

   ```text
   [vira_sms_login]
   ```

5. Optionally set the login-page and account-page URLs in the plugin settings.

To add a login or account link to a theme header, use:

```text
[vira_sms_account_button]
```

The button links to the configured login page for visitors and the configured account page for signed-in users. When no account page is configured, it uses the WooCommerce account page if available, or the user's profile page.

## Sign-in flow

1. The visitor enters an Iranian mobile number. The plugin normalizes Persian and Latin digits, spaces, hyphens, `+98`, and `0098` to a consistent number.
2. The plugin sends a one-time code through the configured IPPanel pattern. The form masks the destination number and provides a resend countdown.
3. Existing users sign in after entering the correct code. New users provide a first and last name before their account is created and signed in.

The mobile number without its leading zero is used as the WordPress username. The form does not ask for an email address or password. New accounts receive a random password that is not shown to the user; sign-in is handled by SMS.

The plugin does not replace or disable `wp-login.php`, so administrators retain the standard WordPress login. Public login links and WooCommerce account-page redirects can optionally point to the SMS login page through the plugin settings.

## Settings

The settings page includes:

- IPPanel service URL, access key, and sender number.
- SMS pattern code, code parameter name, and additional `key=value` pattern parameters.
- Code length, expiration time, and resend interval.
- Post-login redirect, login-page URL, account-page URL, and optional form font.

Additional pattern parameter values are sent to IPPanel as configured. Do not include secrets in public issue reports or code examples.

## SMS request

The plugin sends a JSON `POST` request to `{service URL}/api/send`:

```http
POST {service URL}/api/send
Authorization: {IPPanel access key}
Content-Type: application/json
```

```json
{
  "sending_type": "pattern",
  "from_number": "+983000505",
  "code": "{pattern code}",
  "recipients": ["+989123456789"],
  "params": { "code": "12345" }
}
```

Phone numbers are sent in international format. The plugin displays service error messages returned by IPPanel.

## Privacy and security

- The mobile number is used as the account username and stored in the plugin's `vira_sms_mobile` user metadata.
- The one-time code and configured pattern parameters are sent from the WordPress site to IPPanel to deliver the SMS. The IPPanel access key is stored in WordPress settings.
- One-time codes are stored as hashes and expire. Each code can be used once; failed attempts and resend frequency are limited.
- The registration step requires a verified mobile number in the same session and expires after 15 minutes.
- The plugin does not send analytics or visitor tracking data to third parties.
- Uninstalling removes the plugin's settings and temporary data. It does not delete WordPress accounts or mobile numbers saved on those accounts.

## Testing

Run the plugin checks from the WordPress installation root:

```bash
wp eval-file wp-content/plugins/vira-wordpress-sms/tests/test-plugin.php
```

The checks cover number normalization, settings, one-time codes, account behavior, shortcode output, and IPPanel request and response handling. HTTP requests are intercepted during the checks, so no SMS is sent. Temporary settings and codes are restored or removed after the run.

## Project layout

```text
vira-wordpress-sms/
├── admin/                 Plugin settings page
├── assets/                Front-end CSS and JavaScript
├── includes/              Plugin logic, account flow, and IPPanel gateway
├── languages/             Translation files
├── tests/                 WordPress integration checks
├── LICENSE
├── README.md
├── readme.txt             WordPress.org plugin directory readme
└── vira-wordpress-sms.php Main plugin file
```

## License

This project is licensed under the GPL-2.0-or-later license. See [LICENSE](LICENSE).
