---
title: Viant Universal Pixel Tag Setup Guide
description: This article describes how to set up the Viant Universal Pixel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/viant-universal-pixel-tag/
---
## About

The Viant Universal Pixel tag sends client-side conversion and engagement events from your site to Adelphic DSP by Viant for measurement, optimization, and attribution.

Use this tag to track standard funnel events (such as Page View, Add to Cart, Initiate Checkout, Purchase, Lead) and pass rich transaction details, customer identifiers, and product data to Viant.

Built-in support for Universal Pixel ID (UPID), customer IDs, revenue, currency, and custom parameters helps improve campaign performance, reporting accuracy, and troubleshooting across Viant’s advertising platform.

## Tag tips
*   Use mappings to:
    *   Dynamically override the standard config values
    *   Dynamically override E-Commerce extension values
*   Supports the E-Commerce extension for:  
    * Currency (`_ccur`)  
    * Product Category (`_ccat`)  
    * Revenue / Sub Total (`_csubtotal`)  
    * Transaction ID (`_corder`)

## Tag configuration

Navigate to the tag marketplace to add a new tag. For more information, see .

When adding the tag, configure the following settings:

* **Universal Pixel ID**: Unique ID for the pixel used for tracking. Provided by Adelphic DSP by Viant.
* **User ID**: Base64 encoded internal customer ID of advertiser. Used for attribution algorithms and audit troubleshooting.
* **Disable Automapping**: Disable automatic mapping of E-Commerce extension variables to event data.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Tag Configuration

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `upid` | `String` | Universal Pixel ID |
| `cuid` | `String` | User ID |
| `disable_automapping` | `String` | Disable Automapping |


### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `upid` | `String` | Universal Pixel ID |
| `cuid` | `String` | User ID |
| `cur` | `String` | Currency |
| `cust` | `String` | Customer Type |
| `itms` | `String` | Product Category |
| `url` | `String` | Page URL |
| `ref` | `String` | Referrer URL |
| `val` | `String` | Revenue |
| `tn` | `String` | Transaction ID |
| `p1` | `String` | Custom Parameter 1 |
| `p2` | `String` | Custom Parameter 2 |
| `p3` | `String` | Custom Parameter 3 |
| `p4` | `String` | Custom Parameter 4 |
| `p5` | `String` | Custom Parameter 5 |
| `p6` | `String` | Custom Parameter 6 |
| `p7` | `String` | Custom Parameter 7 |
| `p8` | `String` | Custom Parameter 8 |
| `p9` | `String` | Custom Parameter 9 |
| `p10` | `String` | Custom Parameter 10 |


### E-Commerce

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `cur` | `String` | Currency (Overrides `_ccur`) |
| `itms` | `0` | Product Category |
| `val` | `String` | Revenue (Overrides `_csubtotal`) |
| `tn` | `String` | Transaction `ID` (Overrides `_corder`) |


### Event-specific Parameters
To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Event | Description |
|:------|:------------|
| `cuid` | User ID |
| `url` | Page URL |
| `cur` | Currency |
| `cust` | Customer Type |
| `itms` | Product Category |
| `ref` | Referrer URL |
| `val` | Revenue |
| `tn` | Transaction ID |
| `p1` | Custom Parameter 1 |
| `p2` | Custom Parameter 2 |
| `p3` | Custom Parameter 3 |
| `p4` | Custom Parameter 4 |
| `p5` | Custom Parameter 5 |
| `p6` | Custom Parameter 6 |
| `p7` | Custom Parameter 7 |
| `p8` | Custom Parameter 8 |
| `p9` | Custom Parameter 9 |
| `p10` | Custom Parameter 10 |

    