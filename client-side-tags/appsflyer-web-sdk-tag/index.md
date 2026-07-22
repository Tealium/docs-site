---
title: AppsFlyer Web SDK Tag Setup Guide
description: This article describes how to set up the AppsFlyer Web SDK tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/appsflyer-web-sdk-tag/
---
The Web-S2S API for People-Based Attribution complements the Web SDK allowing marketers to report events occurring on their websites but outside the scope of the Web SDK.

## Tag Tips

* To get your Web Dev Key go to **AppsFlyer &gt; My Apps &gt; View brand bundles**.
* Use mappings to:
  * Dynamically override the E-Commerce extension values
  * Setup event triggers

* Supports the following E-Commerce extension values:
  * Order Subtotal (`_csubtotal`)
  * Order Currency (`_ccurrency`)

## Tag Configuration

First, go to the tag marketplace and add the AppsFlyer Web SDK tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Web Dev Key**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Tag Configuration

| Variable                    | Description |
|:----------------------------|:------------|
| Web Dev Key (`web_dev_key`) | [String]    |

### E-Commerce

| Variable                                              | Description |
|:------------------------------------------------------|:------------|
| Sub Total (`order_subtotal`) (Overrides `_csubtotal`) | [String]    |
| Currency (`order_currency`) (Overrides `_ccurrency`)  | [String]    |

### Events

| Variable       | Description      |
|:---------------|:-----------------|
| Search         | `search`         |
| AddToCart      | `addToCart`      |
| RemoveFromCart | `removeFromCart` |
| Purchase       | `purchase`       |
| Download       | `download`       |
| Signup         | `signup`         |
| Subscriptions  | `subscriptions`  |
| Custom         | `Custom`         |

### Event-specific Parameters

| Variable       | Description      |
|:---------------|:-----------------|
| Search         | `search`         |
| AddToCart      | `addToCart`      |
| RemoveFromCart | `removeFromCart` |
| Purchase       | `purchase`       |
| Download       | `download`       |
| Signup         | `signup`         |
| Subscriptions  | `subscriptions`  |
| Custom Event   | `Custom_Event`   |
