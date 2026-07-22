---
title: Adjust Mobile Remote Command Tag Setup Guide
description: This article describes how to set up the Adjust Mobile Remote Command tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/adjust-mobile-remote-command-tag/
---
Adjust is the industry leader in mobile measurement and fraud prevention. By making marketing simpler, smarter and more secure, we empower data-driven marketers to succeed.

## Tag Tips

* Use mappings to override standard config values.
* This is a remote command companion tag for the native mobile app SDK.

## Tag Configuration

First, go to the tag marketplace and add the Adjust Mobile Remote Command tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Adjust API Token**
  * Adjust API tokens are assigned per user and can be used with any of your Adjust dashboard accounts and for any Adjust integrated app.
  * [Find your Adjust API token](https://help.adjust.com/en/article/developer-guides#how-to-find-your-adjust-api-token).

* **Auto Initialize**
  * Automatically send the Initialize command.

* **Sandbox**
  * Set to true if you or someone else is testing your app.

* **Log Leve**
  * Increase or decrease the amount of logs that you see during testing.

* **Delay Start**
  * Delaying the start of the Adjust SDK allows your app some time to obtain session parameters, such as unique identifiers, to be sent on install.
  * The maximum delay start time of the Adjust SDK is 10 seconds.

* **Allow iAd iOS Framework**
  * This framework is needed so that SDK can automatically handle attribution for ASA campaigns you might be running.

* **Allow Ad Services Framework**
  * For devices running iOS 14.3 or higher, this framework allows the SDK to automatically handle attribution for ASA campaigns.
  * It is required when leveraging the Apple Ads Attribution API.

* **Allow iOS Advertising Identifier**
  * Certain services (such as Google Analytics) require you to coordinate device and client IDs to prevent duplicate reporting.

* **App Secret ID**
  * Used for SDK Signature Feature.

* **App Secret Info 1**
  * Used for SDK Signature Feature.

* **App Secret Info 2**
  * Used for SDK Signature Feature.

* **App Secret Info 3**
  * Used for SDK Signature Feature.

* **App Secret Info 4**
  * Used for SDK Signature Feature.

* **Event Buffering**
  * If your app makes heavy use of event tracking, you might want to delay some HTTP requests to send them in one batch every minute.

* **Background Tracking**
  * The default behaviour of the Adjust SDK is to pause sending HTTP requests while the app is in the background.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Commands

| Remote Command              |
|:----------------------------|
| `launch`                    |
| `track_deeplink`            |
| `purchase`                  |
| `event`                     |
| `contact`                   |
| `ad_revenue`                |
| `subscribe`                 |
| `received_push_token`       |
| `add_session_parameters`    |
| `remove_session_parameters` |
| `reset_session_parameters`  |
| `consent_revoked`           |
| `consent_granted`           |
| `set_enabled`               |
| `offline`                   |

### Standard

| Variable                                                     | Type      |
|:-------------------------------------------------------------|:----------|
| API Token (`api_token`)                                      | [String]  |
| Auto Initialize (`auto_initialize`)                          | [Boolean] |
| Sandbox (`sandbox`)                                          | [Boolean] |
| Log Level (`settings.log_level`)                             | [String]  |
| Delay Start (`settings.delay_start`)                         | [Float]   |
| Allow IAD (`settings.allow_iad)                              | [Boolean] |
| Allow Ad Services (`settings.allow_ad_services`)             | [Boolean] |
| Allow IDFA (`settings.allow_idfa`)                           | [Boolean] |
| App Secret (`settings.app_secret`)                           | [String]  |
| App Secret Info 1 (`settings.app_secret_info_1`)             | [String]  |
| App Secret Info 2 (`settings.app_secret_info_2`)             | [String]  |
| App Secret Info 3 (`settings.app_secret_info_3`)             | [String]  |
| App Secret Info 4 (`settings.app_secret_info_4`)             | [String]  |
| Event Buffering Enabled (`settings.event_buffering_enabled`) | [Boolean] |
| Send In Background (`settings.send_in_background`)           | [Boolean] |

### Event Tracking

| Variable                                          | Type                                        |
|:--------------------------------------------------|:--------------------------------------------|
| Event Token                                       | (`event_token`)                             |
| Order ID                                          | (`order_id`) (Overrides `_corder`)          |
| Order Total (`order_total`) (Overrides `_ctotal`) | [Float]                                     |
| Currency                                          | (`order_currency`) (Overrides `_ccurrency`) |
| Conversion Value                                  | (`conversion_value`)                        |
| Sales Region                                      | (`sales_region`)                            |
| SKU (`sku`)                                       | [String]                                    |
| Purchase Token (`purchase_token`)                 | [String]                                    |
| Signature (`signature`)                           | [String]                                    |

### Ad Revenue Tracking

| Name              | Parameter             |
|:------------------|:----------------------|
| Ad Revenue Source | (`ad_revenue_source`) |

### Subscriptions

| Variable                           | Type              |
|:-----------------------------------|:------------------|
| App Store Receipt Data (`receipt`) | [JSON]            |
| Purchase Timestamp                 | (`purchase_time`) |

### Callback/Partner Parameters

| Variable                       | Parameter                          |
|:-------------------------------|:-----------------------------------|
| Callback Id                    | (`callback_id`)                    |
| Remove Session Callback Params | (`remove_session_callback_params`) |
| Reset Session Callback Params  | (`reset_session_callback_params`)  |
| Remove Session Partner Params  | (`remove_session_partner_params`)  |
| Reset Session Partner Params   | (`reset_session_partner_params`)   |

### Deeplinking

| Variable      | Description           |
|:--------------|:----------------------|
| Deep Link Url | (`deeplink_open_url`) |

### Messaging

| Variable   | Description    |
|:-----------|:---------------|
| Push Token | (`push_token`) |

### Consent Measurement

| Variable            | Description             |
|:--------------------|:------------------------|
| Consent Granted     | (`measurement_consent`) |
| Enabled (`enabled`) | [Boolean]               |
