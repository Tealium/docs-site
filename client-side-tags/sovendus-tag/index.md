---
title: Sovendus Tag Setup Guide
description: This article describes how to set up the Sovendus tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/sovendus-tag/
---
## Tag tips

* Supports these E-commerce extension parameters:
  * Order ID (`_corder`)
  * Order Subtotal `_csubtotal`)
  * Currency (`_ccurrency`)
  * Promo Code (`_cpromo`)
  * Customer Zip (`_czip`)

### Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Traffic Source Number**
  * Enables Sovendus to allocate your shop in their system.

* **Traffic Medium Number**
  * If you are using several traffic media enter the active traffic medium here.

* **Iframe Container ID**
  * Determines at which position on the page the generated iframe should be implemented.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Iframe Configurations

| Variable                                                  | Description             |
|:----------------------------------------------------------|:------------------------|
| Traffic Source Number                                     | (`trafficSourceNumber`) |
| Traffic Medium Number                                     | (`trafficMediumNumber`) |
| Iframe Container ID                                       | (`iframeContainerId`)   |
| Session ID                                                | (`sessionId`)           |
| Timestamp                                                 | (`timestamp`)           |
| Order ID (`orderId`) (Overrides `_corder`)                | [String]                |
| Order Value (`orderValue`) (Overrides `_csubtotal`)       | [String]                |
| Order Currency (`orderCurrency`) (Overrides `_ccurrency`) | [String]                |
| Used Coupon Code (`usedCouponCode`) (Overrides `_cpromo`) | [String]                |

### Consumer Data

| Variable                                                 | Description            |
|:---------------------------------------------------------|:-----------------------|
| Consumer Salutation                                      | (`consumerSalutation`) |
| Consumer First Name                                      | (`consumerFirstName`)  |
| Consumer Last Name                                       | (`consumerLastName`)   |
| Consumer Email                                           | (`consumerEmail`)      |
| Consumer Zipcode (`consumerZipcode`) (Overrides `_czip`) | [String]               |
