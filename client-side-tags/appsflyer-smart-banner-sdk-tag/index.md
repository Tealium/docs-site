---
title: AppsFlyer Smart Banner SDK Tag Setup Guide
description: This article describes how to set up the AppsFlyer Smart Banner SDK tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/appsflyer-smart-banner-sdk-tag/
---
## Tag tips

* Use AppsFlyer Web SDK or AppsFlyer Smart Banner SDK, but not both.
* To get your Web Dev Key, In AppsFlyer, go to the **My Apps** tab and click **View brand bundles**.
* To get Your Banner Key, In AppsFlyer, go to **Engagement & Deep Linking > Smart Banners**.
* Use mappings to:
  * Dynamically override the E-Commerce extension values
  * Setup event triggers
* Supports the following E-Commerce extension values:
  * Order Subtotal (`_csubtotal`)
  * Order Currency (`_ccurrency`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Web Dev Key**
* **Your Banner Key**

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Tag Configuration

| Variable | Data Type | Description |
|:---------|:------------|:------------|
|  `web_dev_key`  | String | Web developer key |
|  `your_banner_key`  | String | Your banner key |

### E-Commerce

| Variable | Data Type | Description |
|:---------|:------------|:------------|
|  `order_subtotal` (Overrides `_csubtotal`)  | String | Subtotal |
|  `order_currency` (Overrides `_ccurrency`)  | String | Currency |

### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
|   `search` |Search|
|   `addToCart` | Add to cart|
|   `removeFromCart` | Remove from cart|
|   `purchase` | Purchase|
|  `download` | Download|
|  `signup` | Signup|
|   `subscriptions` | Subscriptions|
|  `Custom` | Custom|

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
|   `search` |Search|
|   `addToCart` | Add to cart|
|   `removeFromCart` | Remove from cart|
|   `purchase` | Purchase|
|  `download` | Download|
|  `signup` | Signup|
|   `subscriptions` | Subscriptions|
|  `Custom` | Custom|

    