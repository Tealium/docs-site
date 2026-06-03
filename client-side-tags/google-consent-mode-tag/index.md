---
title: Google Consent Mode Tag Setup Guide
description: Learn how to set up the Google consent mode tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/google-consent-mode-tag/
---
Google consent mode communicates user consent status to Google tags, enabling them to adjust their data collection and measurement behavior according to the specified consent preferences.

## About consent modes

You can implement consent mode in two ways: basic and advanced.

For more information, see [Google Ads Help: About consent mode](https://support.google.com/google-ads/answer/10000067?hl=en)

### Basic consent mode

When you use basic consent mode, tags are completely blocked from loading until the user interacts with a consent banner. The Google Consent Mode tag is designed to always fire so that it can send consent signals to the other Google tags, but it never transmits data to Google until consent is granted.

### Advanced consent mode

When you use advanced consent mode, Google tags load and assume a default consent of denied (unless configured otherwise in Google). The Google Consent Mode tag records consent signals and each Google tag reacts to the updated consent states. While consent is denied, the Google tags use a cookieless ping to transmit consent state and anonymous user activity.

For more information, see [Google Analytics Help: Consent mode pings](https://support.google.com/analytics/answer/10000067?sjid=16066762200831072014-NC#Pings)

This approach aims to collect maximum data for analytics and ad conversions, using personally identifiable information (PII) selectively when consented.

## Tips

This section provides general information regarding tag configuration and mapping options. For details on how to integrate Google consent mode with Tealium consent register (a feature of client-side [consent integrations]() and [consent manager]()), refer to [Tealium consent register](). This is the recommended implementation approach.

To allow the Google Consent Mode tag to dynamically adapt to user consent status, we recommend the following:

* Basic consent mode:
  * Set Google Consent Mode tag to **Strictly Necessary** in consent integrations or omit the tag from consent management.
  * Map Google tags to their respective consent categories in either consent integrations or consent management.
* Advanced consent mode:
  * Set Google Consent Mode tag and Google tags to **Strictly Necessary** in consent integrations or omit the tag from consent management.
  * Map end-user consent choices to Google consent mode settings using a JavaScript extension. For details, see [consent purpose mapping]().

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Automatically read from Tealium Consent Cookie**: If set to `true`, Google consent is set based on the Tealium consent manager. See the other configuration descriptions for the exact behavior.
* **Ad Storage**: If the integration with the consent manager is enabled and partial consent is given, the `ad_storage_consent` value is set to `granted`. When full consent is given, `granted` is set.
* **Ad User Data**: If the integration with the consent manager is enabled and partial consent is given, we use this consent category to set `ad_user_data` value to `granted`. When full consent is given, `granted` is set.
* **Ad Personalization**: If the integration with the consent manager is enabled and partial consent is given, we use this consent category to set `ad_personalization` value to `granted`. When full consent is given, `granted` will be set.
* **Analytics Storage**: If the integration with the consent manager is enabled and partial consent is given, this sets `analytics_storage_consent` value to `granted`. When full consent is given, `granted` will be set.
* **Ads Data Redaction Mapping**  
When `ads_data_redaction` is `true` and `ad_storage` is `denied`, ad click identifiers sent in network requests by Google Ads and Floodlight tags are redacted.
* **URL Passthrough**: You can optionally elect to pass information through URL parameters across pages to improve measurement quality.
* **Wait For Update**: If your consent tool loads asynchronously, it might not always run before your Google tags. To account for this, specify `wait_for_update` along with a millisecond value to control how long to wait before sending data.
* **Data Layer Name**: By default, the data layer initiated and referenced by the global site tag is named `dataLayer`. Rename the data layer only if your project requires a separate name.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `tealium_consent`  | Boolean | Read from Tealium Consent Cookie. |
|  `ad_storage_consent`  | String | Ad Storage Consent. |
|  `ad_user_data`  | String | Ad User Data. |
|  `ad_personalization`  | String | Ad Personalization. |
|  `analytics_storage_consent`  | String | Analytics Storage Consent. | 
|  `ads_data_redaction`  | Boolean | Ads Data Redaction Mapping. |
|  `url_passthrough`  | Boolean | URL Passthrough. |
|  `wait_for_update`  | Number | Wait for Update. |
| `data_layer_name` | `String` | Data Layer Name. |

### Events

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `update` | Update |

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `tealium_consent` | Boolean | Read from Tealium Consent Cookie. |
|  `ad_storage_consent` | String | Ad Storage Consent. |
|  `ad_user_data` | String | Ad User Data. |
|  `ad_personalization` | String | Ad Personalization. |
|  `analytics_storage_consent` | String | Analytics Storage Consent. |
|  `ads_data_redaction` | Boolean | Ads Data Redaction Mapping. |
|  `url_passthrough` | Boolean | URL Passthrough. |
|  `wait_for_update` | Number | Wait for Update. |
|  `Custom_Parameter` | | Custom Parameter. |
|  `update` | |Update. |

## Vendor documentation

* [About Google Consent Mode](https://support.google.com/analytics/answer/9976101?hl=en)
* [Google Developers: Adjust tag behavior based on consent](https://developers.google.com/gtagjs/devguide/consent)
