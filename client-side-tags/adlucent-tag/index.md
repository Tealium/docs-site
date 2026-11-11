---
title: Adlucent Tag Setup Guide
description: This article describes how to set up the Adlucent tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/adlucent-tag/
---
## Tag tips

* Use the E-Commerce extension to set the following parameters:
  * Order ID
  * Customer ID
  * List of SKUs
  * List of Quantities
  * List of Prices
  * List of Categories

* Use mapping to:
  * Dynamically override the standard config values
  * Dynamically override the E-Commerce extension values
  * Set a value for Customer Type

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Retailer ID**: Your Adlucent retailer ID.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable                        | Description      |
|:--------------------------------|:-----------------|
| Retailer ID                     | (`retailer`)     |
| Customer ID                     | (`customerID`)   |
| Customer Type                   | (`customerType`) |
| Order ID                        | (`orderKey`)     |
| List of SKUs (`sku`)            | [Array]          |
| List of Quantities (`qty`)      | [Array]          |
| List of Prices (`price`)        | [Array]          |
| List of Categories (`category`) | [Array]          |
