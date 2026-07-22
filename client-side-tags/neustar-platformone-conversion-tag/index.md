---
title: Neustar PlatformOne Conversion Tag
description: This article describes how to set up the Neustar PlatformOne Conversion Tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/neustar-platformone-conversion-tag/
---
This article describes how to set up the Neustar PlatformOne Conversion Tag in your Tealium iQ Tag Management account.

Neustar® PlatformOne is an integrated marketing platform that enables advertisers to deliver precision marketing across all marketing activities. Powered by Neustar's Authoritative Identity Engine, PlatformOne provides a single, unbiased and accurate view of customers and prospects to improve conversion rates, optimize spend, and ultimately increase sales.

## Tag Tips

*   Use mapping to override the standard config values dynamically.
*   Uses the following E-Commerce variables
    *   `_corder`
    *  ` _ctotal`
    *   `_ccustid`
    *   `_cquan`
*   `product_quantity`
    *   This can be mapped as an array (overriding the E-Commerce value, as normal), and will to summed to give a total
    *   Or mapped as a number that will be assigned directly

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

*   **Tag ID**: An integer value. For example: `123456`.
*   **Type ID**: An integer value. For example:  `123456`.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/about-data-mappings/).

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
