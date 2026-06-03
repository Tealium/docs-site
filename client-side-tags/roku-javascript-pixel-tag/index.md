---
title: Roku JavaScript Pixel Tag Setup Guide
description: This article describes how to set up the Roku JavaScript Pixel tag.
url: https://docs.tealium.com/client-side-tags/roku-javascript-pixel-tag/
---
## Tag tips

* Use mappings to override standard parameters.
* Supported E-Commerce extension parameters.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see .

When adding the tag, configure the following settings:

* **Ad Account ID**: Your Roku ad account ID. 
* **Generate Event ID**: Automatically generate an event ID for every Roku tracking event. Used for deduplication when implementing the Roku Events API connector. The default value is `true`. For more information, see [Roku Events API connector](). 
* **Auto PageView Tracking**: Automatically track page views. The default value is `true`.
* **Auto Purchase Tracking**: If `order_id` or `_corder` are present, automatically trigger a purchase event. The default value is `true`.

### Roku Events API

 This feature requires an active [Tealium Collect tag](). 

To support the Roku Events API, set **Generate Event ID** to `true`.  When **Generate Event ID** is enabled, this tag generates a unique event ID for each event tracked and sends it as an attribute to Tealium EventStream for use in the Roku Events API connector and passes it to the Roku JavaScript Pixel in the `event_id` parameter. This event ID attribute may be mapped in the connector to synchronize the web-based tag with server-side integration. 

The tag sends event IDs using generated event attributes using the following naming convention:

```nohl
roku_event_id_{EVENT_NAME}_{TAG_UID}
```

For example, a purchase event from tag #32 would send the following attribute and value:

```json
{
  &#34;roku_event_id_purchase_32&#34;: &#34;028b2ade7478...&#34;
}
```

A page view event from the same tag would send the following attribute and value:

```json
{
  &#34;roku_event_id_page_view_32&#34;: &#34;084b1cda7461...&#34;
}
```

#### Deduplication

To ensure proper event deduplication, the event ID from the Roku Events API connector Pixel tag must be included in the payload sent by the Tealium Collect tag. To do this, use the following steps:

* From the **Tag Timing** drop-down, select **Prioritized**.
* Set the **Bundle Flag** toggle to `On`.
* Use **Load Order Manager** to fire the Roku JavaScript Pixel tag before the Tealium Collect tag. We recommend that you fire the Tealium Collect tag last. For more information, see [Load Order Manager]().

For information on using these event ID attributes, see [Roku: Events API connector]() and [Roku: Conversions API](https://help.ads.roku.com/en/articles/8880744-conversions-api).


## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Tag configuration

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `account_id` | String | Account ID. |
| `generate_event_id` | Boolean | Generate event ID. |
| `auto_page_view` | Boolean | Auto page view. |
| `auto_purchase_event` | Boolean | Auto purchase event. |

### User

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `user_data.is_hashed` | Boolean | Is hashed. |
| `user_data.em` | String | Email. |
| `user_data.ph` | String | Phone number. |
| `user_data.ge` | String | Gender. |
| `user_data.db` | String | Date of birth. |
| `user_data.ln` | String | Last name. |
| `user_data.fn` | String | First name. |
| `user_data.ct` | String | City. |
| `user_data.st` | String | State. |
| `user_data.zp` | String | Zip. |
| `user_data.country` | String | Country. |
| `user_data.external_id` | String | External ID. |
| `user_data.subscription_id` | String | Subscription ID. |
| `user_data.ga_session_id` | String | Google Analytics session ID. |
| `user_data.ga_client_id` | String | Google Analytics client ID. |
| `user_data.ga_gclid` | String | Google Analytics click ID. |
| `user_data.ga_measurement_ids` | Array | Google Analytics measurement IDs. |
| `user_data.us_privacy` | String | US privacy string. |

### E-Commerce

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `order_id` | String | Order ID (Overrides `_corder`). |
| `order_subtotal` | String | Sub total (Overrides `_csubtotal`). |
| `order_currency` | String | Currency (Overrides `_ccurrency`). |
| `delivery_category` | String | Delivery category. |
| `product_delivery_category` | Array | List of product delivery categories. |
| `product_id` | Array | List of product IDs (Overrides `_cprod`). |
| `product_quantity` | Array | List of product quantities (Overrides `_cquan`). |
| `product_unit_price` | Array | List of product prices (Overrides `_cprice`). |

### Standard tracking parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `event_id` | String | Event ID.|
| `content_category` | String or Array | Content category. |
| `content_name` | String or Array | Content name. |
| `content_ids` | Array | Content IDs. |
| `content_type` | String | Content type. |
| `predicted_ltv` | String | Predicted lifetime value. |
| `search_string` | String | Search string. |
| `num_items` | Number | Number of items. |
| `status` | String | Status. |
| `event_source` | String | Event source. |
| `event_source_URL` | String | Event source URL. |
| `referrer_URL` | String | Referrer URL. |
| `opt_out` | String | LDU opt out. |

### Event-specific parameters

To map events, see [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Event | Description |
|:------|:------------|
| `event_id` | Event ID. |
| `content_category` | Content category. |
| `content_name` | Content name. |
| `content_ids` | Content IDs (Overrides `_cprod`). |
| `content_type` | Content type. |
| `predicted_ltv` | Predicted lifetime value. |
| `search_string` | Search string. |
| `num_items` | Number of items. |
| `status` | Status. |
| `event_source` | Event source. |
| `event_source_URL` | Event source URL. |
| `referrer_URL` | Referrer URL. |
| `opt_out` | LDU opt out. |
| `order_id` | Order ID. |
| `order_subtotal` | Sub total. |
| `order_currency` | Currency. |
| `delivery_category` | Delivery category. |
| `product_delivery_category` | List of product delivery categories. |
| `product_id` | List of product IDs. |
| `product_quantity` | List of product quantities. |
| `product_unit_price` | List of product prices. |

    