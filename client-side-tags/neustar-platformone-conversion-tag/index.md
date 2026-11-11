---
title: Neustar PlatformOne Conversion Tag
description: This article describes how to set up the Neustar PlatformOne Conversion Tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/neustar-platformone-conversion-tag/
---
This article describes how to set up the Neustar PlatformOne Conversion Tag in your Tag Management account.

Neustar® PlatformOne is an integrated marketing platform that enables advertisers to deliver precision marketing across all marketing activities. Powered by Neustar's Authoritative Identity Engine, PlatformOne provides a single, unbiased and accurate view of customers and prospects to improve conversion rates, optimize spend, and ultimately increase sales.

## Tag tips

*   Use mapping to override the standard config values dynamically.
*   Uses the following E-Commerce variables
    *   `_corder`
    *  ` _ctotal`
    *   `_ccustid`
    *   `_cquan`
*   `product_quantity`
    *   This can be mapped as an array (overriding the E-Commerce value, as normal), and will to summed to give a total
    *   Or mapped as a number that will be assigned directly

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

*   **Tag ID**: An integer value. For example: `123456`.
*   **Type ID**: An integer value. For example:  `123456`.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| Tag ID   | (`tag_id`)  |
| Type ID  | (`type`)    |

### E-Commerce

| Variable                                                     | Description                            |
|:-------------------------------------------------------------|:---------------------------------------|
| Order ID                                                     | (`order_id`) (Overrides `_corder`)     |
| Order Total                                                  | (`order_total`) (Overrides `_ctotal`)  |
| Customer ID                                                  | (`customer_id`) (Overrides `_ccustid`) |
| List of Quantities (`product_quantity`) (Overrides `_cquan`) | \[Array/Number\]                       |
| Custom Attribute 1 (`cust1`)                                 | \[Array/String\]                       |
| Custom Attribute 2 (`cust2`)                                 | \[Array/String\]                       |
