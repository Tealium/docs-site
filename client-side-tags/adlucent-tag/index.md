---
title: Adlucent Tag Setup Guide
description: This article describes how to set up the Adlucent tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/adlucent-tag/
---
## Tag Tips

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

## Tag Configuration

First, go to the tag marketplace and add the Adlucent tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Retailer ID**: Your Adlucent retailer ID.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

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
