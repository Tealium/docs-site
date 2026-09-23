---
title: Publish mobile settings
description: Publish Prism mobile profile settings to the Tealium CDN using the mobile settings publisher.
url: https://docs.tealium.com/administration/early-access/tealium-prism/publish-mobile-settings/
---

<blockquote>
The mobile settings publisher is in Early Access and only available by request. If you are interested in trying this feature, [contact support](https://docs.tealium.com/support/).
</blockquote>


## About the mobile settings publisher

The mobile settings publisher is a tool in the Tealium Tools browser extension that publishes your Prism mobile profile configuration to the Tealium CDN.

This tool is a temporary solution during the Early Access phase. When mobile settings publishing is released to GA, this tool will be retired. Your app does not need to change.

## Requirements

This feature requires the following:

* [Tealium Tools browser extension](https://docs.tealium.com/tealium-tools-browser-extension/) on Chrome or Edge, with the mobile settings publisher enabled for your account.
* Access to the Tealium account and profile you want to publish.
* A Tealium mobile profile (Early Access) with at least one module configured.
* A [Tealium API key](https://docs.tealium.com/api-keys/) with access to the [hosted data layer API](https://docs.tealium.com/about-hosted-data-layer-api/) for this account and profile.

## How it works

The tool reads the configuration of your currently open mobile profile and publishes it as a Prism settings file.

The published file is the remote tier of the SDK settings. Programmatic (enforced) settings in your app override it. For more information, see [Configuration governance](https://docs.tealium.com/about-tealium-prism/#configuration-governance).

### Environments

The tool publishes a separate file for each environment. The tool does not support custom environments. It publishes to Dev, QA, and Prod only.

| Environment | Default settings file name | URL |
| :--- | :--- | :--- |
| Dev | `mobile_settings_dev` | `https://tags.tiqcdn.com/dle/<account>/<profile>/mobile_settings_dev.json` |
| QA | `mobile_settings_qa` | `https://tags.tiqcdn.com/dle/<account>/<profile>/mobile_settings_qa.json` |
| Prod | `mobile_settings_prod` | `https://tags.tiqcdn.com/dle/<account>/<profile>/mobile_settings_prod.json` |

Set the URL of the file for each environment as the settings URL in the `TealiumConfig` of your app. For more information, see [Quick start guide](https://docs.tealium.com/quick-start/). The SDK does not derive the URL from the account, profile, or environment. The URL in your app must match the published file exactly.

### Custom settings file name

To publish under a different file name, change the **Settings file name** for an environment. For example, if your app already fetches `settings.json`, enter `settings`. The name applies to the CDN URL, the **Last published** check, the publish, and the downloaded file for that environment.

The tool removes a trailing `.json` and any character other than letters, digits, `_`, `.`, and `-`. An empty name resets to the default. To restore the default, click **Reset**. Custom names are saved in your browser for the current account and profile.

### Bundle an initial settings file with your app

Click **Download JSON** to generate the settings file, then bundle it in your app as the local settings file. A bundled file fully configures the SDK on first launch, even with limited connectivity. Remote settings override the bundled file after the SDK fetches them.

For more information about specifying a local settings file, see the [Quick start guide](https://docs.tealium.com/quick-start/).

### API key

The tool exchanges your API key for a short-lived bearer token and uses the token to publish. The tool never sends the API key itself to the hosted data layer API.

By default, the tool keeps the key for the current browser session only. If you select **Remember API key across sessions**, the tool stores the key in browser local storage. The stored key is not encrypted. Only select this option on a device that you trust. A stored key appears masked with **Change** and **Clear** actions. **Clear** removes the stored key and the cached token.

### Audit warnings

Before publishing, the tool checks the generated file for settings that the SDK accepts but ignores without logging an error. Findings appear at the top of the tool. Findings do not block a publish, but the affected setting has no effect in the app until you fix it in Tealium.

| Finding | Effect in the SDK | What to do |
| :--- | :--- | :--- |
| A list setting contains selection objects instead of plain values | The SDK drops every value. The setting behaves as if nothing is selected. | Re-save the setting in Tealium. If the finding persists, [contact support](https://docs.tealium.com/support/). |
| A barrier configuration value has the wrong type | The SDK ignores the value and uses the default. | Re-save the barrier in Tealium. |
| A barrier or transformation scope references an unknown module | The barrier gates nothing, or the transformation never runs. | Update the scope. The reference usually points to a deleted or web-only tag. |
| A barrier or transformation scope is empty | The scope matches no dispatcher and never takes effect. | Select the intended dispatchers, or remove the item. |
| A transformation uses a transformer that the SDK does not have | The transformation never runs. | Replace the extension with a type that Prism supports. |
| A module references a load rule that is not in the file | The module is blocked for every dispatch. | Check that the load rule exists and is active. |
| Consent references a dispatcher that is not a module | The consent setting gates nothing. | Update the consent configuration to reference active modules. |
| A module type is unknown to the SDK | The SDK drops the module at startup. | Remove web-only tags from the mobile profile. |

## Publish mobile settings

To publish mobile settings:

1. In Tealium, open the mobile profile you want to publish.
1. Click the Tealium Tools icon and select **Mobile Settings Publisher**. Confirm that **Account** and **Profile** match the profile you intend to publish. The tool reads them from the open session.
1. In the **Tealium API Key** box, paste your API key.
1. (Optional) To review the file before you publish it, click **Download JSON**. To keep a copy each time you publish, leave **Also download the file when publishing** selected.
1. (Optional) Change the **Settings file name** for an environment.
1. Click **Publish to Dev**, **Publish to QA**, or **Publish to Prod**. To publish the same file to all three environments, click **Publish to All Environments**.
1. If Prod is included, a confirmation dialog appears with the message "You are about to publish to PROD. This will overwrite live CDN data. Continue?" In the confirmation dialog, click **OK**.

Each publish replaces the file on the CDN immediately. There is no one-click rollback in the mobile settings section. To roll back, go to **Tag Management > Client-Side Versions**, select a previous version, and publish the mobile settings again.

The tool does not validate the file against the Prism settings schema before publishing. Before you publish to Prod, publish to Dev or QA, or download and review the file.

The tool does not publish an empty file. If the profile has no mobile configuration, the tool shows **No Mobile Configuration Found** or **Nothing to Publish** and the CDN file remains unchanged.

### Publish status

After a publish, the tool shows one of the following messages:

| Message | Meaning |
| :--- | :--- |
| **Publish Successful** | Every targeted environment was published. |
| **Publish Partially Failed** | Some environments were published and some failed. The message lists the result for each environment. |
| **Publish Failed** | Every targeted environment failed. The message lists the reason for each environment. |

The environment buttons stay active, so you can retry a failed environment directly.

## Verify a publish

Each environment shows a **Last published** time and a link to the CDN file. The time comes from the file on the CDN. **Never published** means no file exists for that settings file name.

To view the published file, click the link for the environment. The CDN caches the file for up to one hour. To bypass the cache, add a query string that you have not used before, for example `?cb=1`.

## Troubleshoot errors

| Error | Cause and resolution |
| :--- | :--- |
| **UTUI Not Found** | The tool was not opened from a Tealium mobile profile. Open a mobile profile, then open the tool. |
| **No Mobile Configuration Found** or **Nothing to Publish** | The profile has no mobile settings to publish. Configure at least one module in the mobile profile and save. |
| **API Key Required** | No API key is entered. Paste your key in the **Tealium API Key** box. |
| **User Email Missing** or **Session Error** | The tool could not read your email address, account, or profile from the current Tealium session. Reload Tealium and open the tool again. |
| **Token Exchange Failed** | The API key is invalid or expired, or your user is not authorized to generate API keys. Generate a new key in **Admin > API Keys** and try again. |
| **HTTP 400** | The hosted data layer API rejected the request. Follow the API message. If the error persists, download the file and [contact support](https://docs.tealium.com/support/). |
| **HTTP 403** | Your user does not have permission to publish to the hosted data layer for this account and profile. Contact your account admin. |
| **HTTP 404** | The hosted data layer is not enabled for this account. Contact your Tealium Account Manager. |
| **Last published: unknown** | The CDN check failed for a reason other than a missing file, for example a temporary network error. The publish is not affected. |

### The app does not pick up new settings

* The CDN caches each file for up to one hour. The SDK also keeps a cached copy and continues to use it when the CDN reports that the file has not changed.
* The SDK applies its cached settings at startup and refreshes them from the CDN in the background at the remote settings refresh interval.
* Check that the settings URL in the app matches the account, profile, environment, and settings file name that you published. A Dev or QA file exists only after you publish to that environment.

