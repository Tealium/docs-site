---
title: Insider data source setup guide
description: This article describes how to use Insider as a data source to send actionable events to Tealium.
url: https://docs.tealium.com/server-side/data-sources/webhooks/setup-guides/insider/
---
## Prerequisites

* Tealium EventStream API Hub and/or Tealium AudienceStream CDP 
* Insider account


## How it works

To connect Insider with Tealium EventStream or Tealium AudienceStream, use the [Insider Webhook API](https://academy.useinsider.com/docs/webhooks-vs-apis) to send outgoing requests to the custom Insider data source endpoint in your Tealium account.

After you configure the webhook, you can receive automatic event updates for channel interactions and lead collection events.

## Insider data source

Adding the Insider data source to your Tealium Customer Data Hub profile generates a unique URL to use in your webhook configuration in following format:

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

To add the Insider data source to your Tealium Customer Data Hub profile, see [Data Sources](https://docs.tealium.com/about-data-sources/). After adding and connecting the data source, save and publish your profile.

## Insider setup

After you connect Insider to your Tealium Customer Data Hub profile, configure the webhook using the following steps:

1. Notify your Insider account manager that you want to configure the [Tealium Collect API](https://docs.tealium.com/platforms/http-api/endpoint/) to collect Insider channel events.
1. The Insider team will configure your Tealium data source within Insider.
1. In Tealium, enter the custom endpoint URL created when you added the Insider data source to your Tealium profile. For example,

```
https://collect-us-east-1.tealiumiq.com/integration/event/{account}/{profile}/{data_source_key}
```

## Events and attributes

Insider event parameters are pre-defined based on the engagement behavior or the customer behavior events. All incoming Insider event attributes are prefixed with `insider_`. For example, Insider will send the `campaign_id` attribute to Tealium and it will be converted to `insider_campaign_id` (all lowercase).

### Channel events

The following table describes common Insider event attributes and examples of what Tealium receives for certain channel-specific events. This list is not exhaustive. For a list of all Insider default events, see [Default Events](https://academy.useinsider.com/docs/default-events#mobile-app-%20events) in the Insider documentation.

| Event Attribute | Type | Example |
|---|---|---|
| `insider_event_group_id` | String | `ORDER123` |
| `insider_product_id` | String | `AGH210070 `|
| `insider_name` | String | `iPhone 11+` |
| `insider_taxonomy` | Strings | `["Electronic","Phone"]` |
| `insider_currency` | String | `USD` |
| `insider_unit_price` | Number | `990.9` |
| `insider_unit_sale_price` | Number | `890.8` |
| `insider_color` | String | `black` |
| `insider_size` | String | `one-size` |
| `insider_shipping_cost` | Number | `52.09` |
| `insider_promotion_name` | String | `Test20` |
| `insider_promotion_discount` | Number | `18.8` |
| `insider_qu `| Number | `1` |
| `insider_piu` | String | `https://test.com/producturl` |
| `insider_sid `| String |  |
| `insider_sc` | Number | `52.09` |
| `insider_vn` | String | `VoucherPromotion` |
| `insider_vd` | Number | `12.01` |
| `insider_si` | String | `one-size` |
| `insider_co` | String | `black` |
| `insider_url` | String | `https://test.com/producturl` |
| `insider_referrer` | String | `https://google.com` |
| `insider_device_type` | String | `web` |
| `insider_ip_address` | String | `192.158.1.38 `|
| `insider_campaign_id` | Number | `105901959` |
| `insider_user_agent` | String | `Mozilla/5.0 (iPad; U; CPU OS 3_2_1 like Mac OS X; en-us)` |
| `insider_url_offset_index `| Number | `0` |
| `insider_url_offset_type` | String | `html` |
| `insider_type` | String | `html` |
| `insider_reason` | String | `Unsubscribed Address` |
| `insider_deep_links` | String | `value1 `|
| `insider_dry_run` | String |  |
| `insider_image_url` | String | `https://your_image_url.jpg `|
| `insider_message` | String | `Your push content goes here `|
| `insider_title` | String | `Your push notification title goes here `|
| `insider_attr_email` | String | `test@test.com `|
| `insider_attr_phone` | String | `+14401231234` |
| `insider_hook_id` | String | `442811` |
| `insider_insider_id` | String | `a00d8092-0ba7-41f5-b07d-7ae64231dac3d` |


## Vendor documentation

* [Webhooks vs APIs ](https://academy.useinsider.com/docs/webhooks-vs-apis)
* [Webhooks for email events](https://academy.useinsider.com/docs/api-reference-email-webhooks-for-email-events)
* [Webhooks for transactional SMS](https://academy.useinsider.com/docs/webhooks-for-transactional-sms)