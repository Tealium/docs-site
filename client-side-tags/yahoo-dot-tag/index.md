---
title: Yahoo! Dot Tag Setup Guide
description: This article describes how to set up the Yahoo Dot tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/yahoo-dot-tag/
---

## Tag tips

* Use mapping to:
  * Dynamically override the standard config values
  * Dynamically override the E-Commerce extension values
  * Set values for these Standard custom event parameters:
    * Event Category (`ec`)
    * Event Action (`ea`)
    * Event Label (`el`)
    * Event Value (`ev`)
    * Goal Value (`gv`)
* If you are using the e-commerce extension, Goal Value (`gv`) will automatically be populated with the E-Commerce extension value for Order Subtotal. Map a value directly to Goal Value to override the E-Commerce extension value.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Project ID**
  * The projectId value from your Yahoo Dot code snippet.
* **Pixel ID**
  * The `pixelId` value from your Yahoo Dot code snippet.
  * You may enter multiple Pixel IDs in a comma-separated list.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Yahoo Dot

|Variable| Description|
|---| ---|
|Project ID| (projectId)|
|Pixel ID (pixelId)| [String or Array]|
|User Email| (userEmail)|
|User Hashed Email| (userHashedEmail)|

### Custom Event Parameters

|Variable| Description|
|---| ---|
|Event Category (ec)| [String or Array]|
|Event Action (ea)| [String or Array]|
|Event Label (el)| [String or Array]|
|Event Value (ev)| [String or Array]|
|Goal Value (gv) (Overrides E-Commerce Order Subtotal)| [Number]|
|Timestamp| (timestamp)|
|Advertiser ID| (advertiser\_id)|

### E-Commerce

|Variable| Description|
|---| ---|
|Sub Total| (order\_subtotal) (Overrides \_csubtotal)|
|List of Product IDs (product\_id) (Overrides \_cprod)| [Array]|
