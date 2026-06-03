---
title: Nano Tag Setup Guide
description: This article describes how to set up the Nano tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/nano-tag/
---
Nano’s proprietary technology uses state-of-the-art machine learning to translate live intent signals, combined with next generation contextual analysis. This helps advertisers make efficient and effective decisions on their online ad spend in a post-cookie world.

## Tag tips

* Select the Pixel Type in the tag configuration to load the correct script URL.
  * **Profiling** enables tracking for home and landing pages.
  * **Conversion** loads the CPX Nano pixel for tracking on confirmation and thank you pages.
* Use mappings to override and dynamically set the Tag Configurations.
* Supports the following E-Commerce extension parameters:
  * Product ID
  * Order ID
  * Currency
  * Order Total

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Pixel ID**: Your Nano-provided Pixel ID.
* **Pixel Type**: Loads the correct script URL based on the selected Pixel Type.
  * **Profiling** enables tracking for home and landing pages.
  * **Conversion** loads the CPX Nano pixel for tracking on confirmation and thank you pages.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Configuration

| Variable | Type | Description |
|:---------|:------------|:------------|
| `pixelId`  | String | Pixel ID |
| `pixelType`  | String | Pixel Type |

### E-Commerce

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `product_id`  | Array | Product ID (Overrides `_cprod`) |
|  `order_id`   | String |  Order ID (Overrides `_corder`) |
|  `order_currency`   | String | Currency (Overrides `_ccurrency`) |
|  `order_total`  | Number | Order Total (Overrides `_ctotal`) |
