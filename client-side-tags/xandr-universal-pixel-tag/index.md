---
title: Xandr Universal Pixel Tag Setup Guide
description: This article describes how to set up the Xandr Universal Pixel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/xandr-universal-pixel-tag/
---
## Tag tips

* You may enter multiple Pixel IDs in a comma-separated list.
* Purchase tracking occurs automatically when an order ID is populated. To disable automatic Purchase tracking, toggle the `automatic_purchase_tracking` destination through mappings.
* PageView tracking occurs automatically. To disable automatic PageView tracking, toggle the `automatic_pageview_tracking` destination through mappings.
* By default the PageView event executes without additional data. If you want to pass data with the PageView event, you must map the variables you want in the Event-specific Parameters tab of the mapping toolbox.
* Supports these E-Commerce extension parameters:
  * Order ID (`_corder`)
  * List of Product IDs (`_cprod`)
  * List of Product Names (`_cprodname`)
  * List of Product Categories (`_ccat`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Pixel ID**
  * Enter your Xandr Universal Pixel ID.
  * You may enter multiple IDs in a comma-separated list.
* **Ad Storage Consent**: Set the default consent for Ad Storage. Dynamically update this value by mapping the `ad_storage` parameter in the **Data Mappings** section.
* **Automatically read from Tealium Consent Cookie**: If set to true, consent is set based on the [Tealium consent manager](). 

## Consent mode

There are two options to implement consent mode for this tag:

* Use [client-side consent management]() and automatically read the Tealium consent cookie.
* Add a [JavaScript Code extension]() to map consent choices and category mappings from your consent management platform (CMP) to this tag.

As visitors make their consent choices, the tag will choose the appropriate approach for first and third-party cookies:

* **Granted**: Both first-party and third-party cookies can be read and written.
* **Denied**: First-party cookies are neither read nor written, and third-party cookies are read-only for fraud and spam purposes, not for advertising.

### Client-side consent management

To implement consent mode for this tag using client-side consent management, set **Automatically read from Tealium Consent Cookie** to `true` in the tag configuration.

### JavaScript Code extension

To map end-user consent choices to Xandr consent mode settings, use the JavaScript Code extension. Configure the extension as follows:

* Set **Scope** to **After Load Rules (default)** 
* Set **Occurrence** to **Run Always**
* Enter the JavaScript code for your CMP. You can customize the following code template for your CMP by replacing `CUSTOM_LOGIC` with the logic for your vendor:

```js
b.consent_decision = (tealiumConsentRegister &amp;&amp; tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = CUSTOM_LOGIC ? &#39;granted&#39; : &#39;denied&#39;;
```

For example, the following code is for OneTrust:

```js
// After Load Rules - Run Always
b.consent_decision = (tealiumConsentRegister &amp;&amp; tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = b.consent_decision.indexOf(&#39;C0004&#39;) !== -1  ? &#39;granted&#39; : &#39;denied&#39;;
```

If you use these exact variable names, no additional mapping is required. The latest version of the tag uses these variables by default. Overwrite these variables by mapping the `ad_storage` parameter to attributes for your specific case.  

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Tag Configurations

| Variable                  | Type            | Description                         |
|---------------------------|-----------------|-------------------------------------|
| `pixel_id`                | String          | Universal pixel ID.                 |
| `auto_pageview_tracking`  | Boolean, String | Toggle automatic pageview tracking. |
| `auto_purchase_tracking`  | Boolean, String | Toggle automatic purchase tracking. |
| `base_url`                | String          | Base URL.                           |

### E-Commerce

| Variable      | Type   | Description                                   |
|---------------|--------|-----------------------------------------------|
| `item_type`   | Array  | List of item categories. (Overrides `_ccat`). |
| `item_id`     | Array  | List of item IDs. (Overrides `_cprod`).       |
| `item_name`   | Array  | List of item names. (Overrides `_cprodname`). |

### Events

| Variable           | Description       |
|--------------------|-------------------|
| `AddPaymentInfo`   | Add payment info. |
| `AddToCart`        | Add to cart.      |
| `InitiateCheckout` | Initiate checkout.|
| `ItemView`         | Item view.        |
| `LandingPage`      | Landing page.     |
| `Lead`             | Lead.             |
| `PageView`         | Page view.        |
| `Purchase`         | Purchase.         |
| `Custom`           | Custom event.     |

### Event-specific Parameters

| Variable            | Description         |
|---------------------|---------------------|
| `item_type`         | Item type.          |
| `item_id`           | Item ID.            |
| `item_name`         | Item name.          |
| `Custom_Parameter`  | Custom parameter.   |
| `AddPaymentInfo`    | Add payment info.   |
| `AddToCart`         | Add to cart.        |
| `InitiateCheckout`  | Initiate checkout.  |
| `ItemView`          | Item view.          |
| `LandingPage`       | Landing page.       |
| `Lead`              | Lead.               |
| `Purchase`          | Purchase.           |
| `Custom_Event`      | Custom event.       |
