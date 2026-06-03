---
title: Upsellit Tag
description: This article describes how to set up the Upsellit tag.
url: https://docs.tealium.com/client-side-tags/upsellit-tag/
---
## Tag Tips

* The Launch JavaScript code runs by default on every page.
* The Confirmation Pixel fires when an Order ID is set.
* Supports the E-Commerce extension for:  
  * Order ID  
  * Subtotal
* Use mapping to:  
  * Override the standard config value for Launch File.
  * Override the E-Commerce extension values.  
  * Set values for Site ID and Product ID.  
  * Override the value for Position (default is `1`).

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Launch File**:  
The Launch JavaScript code provided by Upsellit. This value appears before `.jsp`.
* **Site ID**:  
The Site ID for the Confirmation Pixel. For example: `1234`.
* **Product ID**:  
The Product ID for the Confirmation Pixel. For example: `12`.

 The Launch File for the Upsellit tag can be retrieved directly from your Upsellit account dashboard. You can access it by logging into your Upsellit account and navigating to the **Integration** or **Implementation** section. Download or copy the provided JavaScript library URL and associated account details, such as the Account ID and Site ID. For further assistance, contact your Upsellit account representative. 

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `launchfile` | Launch File |
| `position` | Position |
| `USI_orderID` |Order ID (Overrides `_corder`) |
| `USI_orderAmt` |Order Amount (Overrides `_csubtotal`) |
| `USI_currency` | Order Currency (Overrides `_ccurrency`) |

