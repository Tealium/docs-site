---
title: CookieConsent v3 Loader
description: Use the CookieConsent v3 Loader extension to load and configure the open source CookieConsent consent management tool on your site.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/cookieconsent-v3-loader-extension/
---
The CookieConsent v3 Loader extension lets you implement [CookieConsent: CookieConsent v3](https://cookieconsent.orestbida.com/) through Tealium iQ instead of directly on your site, enabling better control and versioning. It loads the required JavaScript and CSS files and runs your custom configuration to render the consent banner and modal.

## Requirements

The CookieConsent v3 Loader extension requires the Manage JavaScript Code Extensions permission.

## How it works

This extension loads the CookieConsent library and initializes it using a configuration object `ccConfig`. You can define categories, services, styles, language settings, and behavior through the extension&#39;s JSON configuration.

The tool is designed to operate in opt-in or opt-out mode and supports advanced features such as disabling page interaction, customizing modal layout, and setting linked categories and cookie tables.

When the page loads, the extension:

* Loads the CookieConsent library.
* Applies your customized `ccConfig` settings.
* Displays the consent modal to users based on your preferences.

## How to configure

1. In Tealium iQ, go to **Extensions** and click **Add Extension**.
1. Click the **Privacy** tab.
1. Click **&#43; Add** next to the **CookieConsent v3 Loader** extension.
1. Enter a **Title** for the extension.
1. Under **Scope**, use the default option **DOM Ready**. It supports load conditions, which lets you control when the extension runs. The **Preloader** scope is also supported but doesn&#39;t allow load conditions.
1. (Optional) Click **Add Condition** to apply a load condition for this extension. This is useful for running the banner only in specific scenarios (for example, when a region-specific load rule is true). Ensure the conditions match your consent integration’s enforcement rules to avoid enforcement issues.
1. In the **Configuration** code, update the `ccConfig` JSON object to define your settings. This includes:
   * Category definitions such as `necessary`, `analytics`, and `marketing`.
   * Language and translation strings for consent and preferences modals.
   * Consent mode: `opt-in` or `opt-out`.
   * GUI options to control banner/modal layout and position.
   * Sections and cookie tables in the preferences modal.
   * Accessibility-related content such as labels, titles, and button text.

   For a full list of configuration options, see [CookieConsent: Configuration Reference](https://cookieconsent.orestbida.com/reference/configuration-reference.html).
