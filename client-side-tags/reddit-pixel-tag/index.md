---
title: Reddit Pixel tag setup guide
description: Set up the Reddit Pixel tag to track post-ad interactions, measure conversions, and enable retargeting in Tealium iQ.
url: https://docs.tealium.com/client-side-tags/reddit-pixel-tag/
---
The Reddit Pixel tag tracks post-ad interactions and supports conversion measurement and retargeting. 

## Requirements

* Reddit Ads account
* Reddit Pixel ID

## Tag tips

* Use mapping to override the standard configuration values and trigger events.
* Purchase event fires when **Order ID** is set.
* To make Reddit Pixel event IDs available as server-side attributes, set **Generate Event ID** to `true` and use the latest version of the [Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/).
* We recommend using the [Reddit Conversions connector](https://docs.tealium.com/reddit-conversions-connector/) conversion ID configuration only if you are implementing both the Reddit Pixel tag and the Reddit Conversions connector. Using the conversion ID configuration prevents the same conversion event from being counted twice if it is sent across both sources. If this value is passed improperly, it impacts attribution and campaign performance.
* We recommend using advanced matching for the most accurate conversion tracking and reporting from Reddit. Pass email addresses and phone numbers as either plain values or pre-hashed with SHA256. The Reddit library applies SHA256 hashing to plain email addresses before sending.
* Map only parameters you intend to use and confirm support in Reddit documentation.
* Use event-specific parameters for fine-grained control when different events require different metadata.
* For revenue events, send both event-level `value` and `itemCount`, and product-level `quantity` and `itemPrice`. Sending only one set of fields can limit reporting or optimization in Reddit Ads.
* Keep product arrays aligned by index. Avoid mixing single values and arrays unless you intend a single-product payload.
* Use event-specific parameters to avoid accidentally applying purchase-only metadata to other events.
* The tag enforces the Reddit event-level parameter requirements. Undefined or empty values are removed and parameters not supported by Reddit for a given event are dropped from the payload.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

To add the tag, configure the following settings:

* **Pixel ID**: Your Reddit Pixel ID.
* **Send Page Visit**
    * By default, the tag automatically records a page visit event for each page on your site.
    * If you do not want to send a page visit event to the Reddit Pixel, set this option to `false`.
* **Send Default Purchase Event**: By default, the tag tracks purchase events on your site. To disable purchase events, set this option to `false`.
* **Generate Event ID**: Automatically generate an event ID for every Reddit tracking event.

### Conversions API


<blockquote>
This feature requires an active [Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/).
</blockquote>


To support the Reddit Conversions API, set **Generate Event ID** to `true`. When **Generate Event ID** is enabled, the tag generates a unique event ID for each tracked event. The tag sends the event ID as an attribute to Tealium EventStream for use in the Reddit Conversions connector, and passes it to the Reddit Pixel in the `event_id` parameter. Map this event ID attribute in the connector to synchronize the web-based tag with server-side integration.

The tag sends event IDs using generated event attributes using the following naming convention:

```nohl
reddit_pixel_event_id_{REDDIT_EVENT}_{TAG_UID}
```

For example, a purchase event from tag #32 would send the following attribute and value:

```json
{
  "reddit_pixel_event_id_Purchase_32": "028b2ade7478..."
}
```

A page view event from the same tag would send the following attribute and value:

```json
{
  "reddit_pixel_event_id_PageView_32": "084b1cda7461..."
}
```

#### Deduplication

To ensure proper event deduplication, the event ID from the Reddit Pixel tag must be included in the payload sent by the Tealium Collect tag. To do this, use the following steps:

* From the **Tag Timing** drop-down, select **Prioritized**.
* Set the **Bundle Flag** toggle to `On`.
* Use the [Load Order Manager screen](https://docs.tealium.com/load-order-manager/) to fire the Reddit Pixel tag before the Tealium Collect tag. We recommend that you fire the Tealium Collect tag last.

For information on using these event ID attributes, see [Reddit Conversions connector: Deduplication for web events](https://docs.tealium.com/reddit-conversions-connector/#deduplication-for-web-events).

## Validation

To confirm the tag is working as expected, use browser developer tools and the [Reddit Pixel Helper](https://business.reddithelp.com/s/article/Reddit-Pixel-Helper-Chrome-extension) browser extension:

* Verify that expected parameters appear for each event.
* Check that no warnings about unsupported or invalid metadata appear.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

Map parameters using the categories below. If a mapped parameter is not supported by Reddit for a given event, the tag drops it from the payload. Use [Event-specific parameters](#event-specific-parameters) to control which parameters are sent per event.

The available categories are:

### Standard

| Variable              | Data Type | Description          |
|-----------------------|-----------|----------------------|
| `pixel_id`            | String    | Pixel ID.            |
| `send_page_visit`     | Boolean   | Send page visit.     |
| `send_purchase_event` | Boolean   | Send purchase event. |
| `generate_event_id`   | Boolean   | Generate event ID.   |
| `event_id`            | String    | Event ID.            |
| `conversion_id`       | String    | Conversion ID.       |
| `transaction_id`      | String    | Transaction ID.      |

### E-commerce

| Variable        | Data Type | Description                        |
|-----------------|-----------|------------------------------------|
| `itemCount`     | Number    | Item count.                        |
| `value`         | Number    | Value.                             |
| `currency`      | String    | Currency (Overrides `_ccurrency`). |
| `transactionId` | String    | Transaction ID.                    |

### Products data

| Variable   | Type/Values | Description                            |
|:-----------|:------------|:---------------------------------------|
| `id`        | Array       | Product ID (overrides `_cprod`).         |
| `category`  | Array       | Product category (overrides `_ccat`).    |
| `name`      | Array       | Product name (overrides `_cprodname`).   |
| `quantity`  | Array       | Product quantity (overrides `_cquan`).   |
| `itemPrice` | Array       | Product item price (overrides `_cprice`).|

### Events

Enter the value of the mapped variable needed to trigger the selected event.

| Variable        | Description      |
|:----------------|:-----------------|
| `PageVisit`     | Page visit.      |
| `ViewContent`   | View content.    |
| `Search`        | Search.          |
| `AddToCart`     | Add to cart.     |
| `AddToWishlist` | Add to wish list.|
| `Purchase`      | Purchase.        |
| `Lead`          | Lead.            |
| `SignUp`        | Sign up.         |
| `Custom`        | Custom events.   |

### Event-specific parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable        | Description               |
|:----------------|:--------------------------|
| `currency`      | Currency.                 |
| `category`      | Product category.         |
| `name`          | Product name.             |
| `id`            | Product ID.               |
| `quantity`      | Product quantity.         |
| `itemPrice`     | Product item price.       |
| `content_type`  | Content type.             |
| `contents`      | Contents.                 |
| `predicted_ltv` | Predicted lifetime value. |
| `search_string` | Search string.            |
| `status`        | Status.                   |
| `itemCount`     | Item count.               |
| `value`         | Value.                    |

### Advanced matching

| Variable      | Data Type | Description       | 
|:--------------|:----------|:------------------|
| `email`       | String    | Email address.    |
| `phoneNumber` | String    | Phone number.     |
| `idfa`        | String    | IDFA.             |
| `aaid`        | String    | AAID.             | 
| `externalId`  | String    | External ID.      | 

### LDU

When the Reddit Pixel is initialized with data processing mode, every conversion event fired from the page automatically includes the following parameters:

| Variable | Data Type | Description |
|:---------|:----------|:------------|
|  `dpm`   | String    | Data processing mode. The default value is `LDU`. |
|  `dpcc`  | String    | Data processing country code in ISO 3166-1 alpha-2 country code format. |
|  `dprc`  | String    | Data processing region code in ISO 3166-2 region code format, with or without the country prefix. |
