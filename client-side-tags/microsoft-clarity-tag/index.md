---
title: Microsoft Clarity Tag Setup Guide
description: This article describes how to set up the Microsoft Clarity tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/microsoft-clarity-tag/
---
Microsoft Clarity is a free-to-use analytics product built to help website managers improve their website experiences by better understanding site visitor behavior.

## Tag Tips
*   Use mapping to dynamically override the project ID value
*   For more information, see [Bing: Microsoft Clarity is now Generally Available](https://blogs.bing.com/webmaster/october-2020/Microsoft-Clarity-is-now-Generally-Available)

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Project ID**: The Clarity project ID. You can find your project ID from your Clarity project URL. For example, `https://clarity.microsoft.com/projects/view/PROJECT_ID/`.
* **Ad Storage Consent**: Set the default consent for Ad Storage. Dynamically update this value by mapping the `ad_storage` parameter in the **Data Mappings** section.
* **Automatically read from Tealium Consent Cookie**: If set to true, consent is set based on the [Tealium consent manager](https://docs.tealium.com/about-consent-management/). 

## Consent mode

There are two options to implement consent mode for this tag:

* Use [client-side consent management](https://docs.tealium.com/about-consent-management/) and automatically read the Tealium Consent cookie.
* Add a [JavaScript Code extension](https://docs.tealium.com/javascript-code-extension/) to map consent choices and category mappings from your consent management platform (CMP) to this tag.

As visitors make their consent choices, the tag will choose the appropriate approach for first and third-party cookies:

* **Granted**: Both first-party and third-party cookies can be read and written.
* **Denied**: First-party cookies are neither read nor written, and third-party cookies are read-only for fraud and spam purposes, not for advertising.

### Client-side consent management

To implement consent mode for this tag using client-side consent management, set **Automatically read from Tealium Consent Cookie** to `true` in the tag configuration.

### JavaScript Code extension

To map end-user consent choices to Microsoft consent mode settings, use the JavaScript Code extension. Configure the extension as follows:

* Set **Scope** to **After Load Rules (default)** 
* Set **Occurrence** to **Run Always**
* Enter the JavaScript code for your CMP. You can customize the following code template for your CMP by replacing `CUSTOM_LOGIC` with the logic for your vendor.
```js
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = CUSTOM_LOGIC ? 'granted' : 'denied';
```

For example, the following code is for OneTrust.
```js
// After Load Rules - Run Always
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = b.consent_decision.indexOf('C0004') !== -1  ? 'granted' : 'denied';
```

If you use these exact variable names, no additional mapping is required. The latest version of the tag uses these variables by default. Overwrite these variables by mapping the `ad_storage` parameter to attributes for your specific case.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `project_id` | The Clarity project ID. You can find your project ID from your Clarity project URL. For example, `https://clarity.microsoft.com/projects/view/PROJECT_ID/`. |


### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Event | Description |
|:------|:------------|
| `enable_consent` | Enable consent |
| `disable_consent` | Disable consent |

    