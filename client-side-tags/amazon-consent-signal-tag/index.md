---
title: Amazon Consent Signal Tag Setup Guide
description: This article describes how to set up the Amazon Consent Signal tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/amazon-consent-signal-tag/
---
## Tag tips

* [Amazon: Amazon Consent Signal (ACS) integration guide for consent management platforms](https://advertising.amazon.co.uk/help/GKJQ7E8SE9BRG73Q/)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [about-tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Automatically read from Tealium Consent Cookie**: If enabled, the tag integrates with Tealium Consent Manager, reads consent status from the Tealium Consent Cookie, and sets the following variables accordingly:
    * **Ad Storage**: Whether Amazon Ads is allowed to use ad-related storage (cookies, localStorage, similar IDs) in the browser for advertising purposes. If **Automatically read from Tealium Consent Cookie** is enabled and the visitor gives partial consent, Tealium checks the consent category you select. If the visitor has consented to this category, `amzn_ad_storage` is set to `granted`. If the visitor gives full consent, `amzn_ad_storage` is always set to `granted`. The default value is `denied`.
    * **Ad User Data**: Whether Amazon Ads is allowed to use the user’s ad-related data (identifiers, behavior) for targeting, measurement, and matching. If **Automatically read from Tealium Consent Cookie** is enabled and the visitor gives partial consent, Tealium checks the consent category you select. If the visitor has consented to this category, `amzn_user_data` is set to `granted`. If the visitor gives full consent, `amzn_user_data` is always set to `granted`. The default value is `denied`.

The following consent categories are available for the **Ad Storage** and **Ad User Data** settings:

* `Denied`: Consent is denied.
* `Granted`: Consent is granted.
* `Analytics`: Consent is given for analytics.
* `Affiliates`: Consent is given for affiliates.
* `Display Ads`: Consent is given for display ads.
* `Search`: Consent is given for search.
* `Email`: Consent is given for email.
* `Personalization`: Consent is given for personalization.
* `Social`: Consent is given for social.
* `Big Data`: Consent is given for big data.
* `Misc`: Consent is given for miscellaneous purposes.
* `Cookie Match`: Consent is given for cookie matching.
* `CDP`: Consent is given for customer data platforms.
* `Mobile`: Consent is given for mobile.
* `Engagement`: Consent is given for engagement.
* `Monitoring`: Consent is given for monitoring.
* `CRM`: Consent is given for customer relationship management.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `tealium_consent` | Boolean | Whether to read consent information from the Tealium Consent Cookie. |
| `countryCode` | String | Country code. |
| `amzn_ad_storage` | String | Ad storage consent. |
| `amzn_user_data` | String | Ad user data. |