---
title: Sovendus Tag Setup Guide
description: This article describes how to set up the Sovendus tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/sovendus-tag/
---
## Tag Tips

* Supports these E-commerce extension parameters:
  * Order ID (`_corder`)
  * Order Subtotal `_csubtotal`)
  * Currency (`_ccurrency`)
  * Promo Code (`_cpromo`)
  * Customer Zip (`_czip`)

### Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Sovendus tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Traffic Source Number**
  * Enables Sovendus to allocate your shop in their system.

* **Traffic Medium Number**
  * If you are using several traffic media enter the active traffic medium here.

* **Iframe Container ID**
  * Determines at which position on the page the generated iframe should be implemented.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

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
