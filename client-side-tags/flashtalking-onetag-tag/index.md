---
title: Flashtalking OneTag Tag Setup Guide
description: This article describes how to set up the Flashtalking OneTag tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/flashtalking-onetag-tag/
---
Flashtalking OneTag uses data to personalize advertising in real-time, analyze its effectiveness, and enable optimizations that drive better engagement and ROI.

## Tag tips

Use mapping to:

* Set a value for `ftXName` (Transaction Name).
* Send custom variables (U1 - U20).
* Override the standard config values.
* Override the E-Commerce extension values.
* If using the E-Commerce extension, these values will be passed automatically when populated in the data layer:
    * `ftXRef` (E-Commerce order ID)
    * `ftXValue` (E-Commerce order subtotal)
    * `ftXType` (E-Commerce order type)
    * `ftXCurrency` (E-Commerce order currency)
    * `ftXNumItems` (E-Commerce list of quantities)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Advertiser ID**: The number just after `/container/` in your code snippet.
* **Spotlight ID**: The number just after your Advertiser ID in your code snippet.
* **Spotlight Group ID**: The number just after Spotlight ID in your code snippet.

Example: `https://servedby.flashtalking.com/container/AdvertiserID;SpotlightID;SpotlightGroupID;iframe/?`

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| **Variable** | **Description** |
|:---------|:------------|
| `aid` | Advertiser ID |
| `sid` | Spotlight ID |
| `sgid` | Spotlight group ID |

### E-Commerce

| **Variable** | **Description** | **Data Type** |
|:---------|:------------|:------------|
| `order_id` | Order ID (ftXRef) (overrides `_corder`) | String |
| `order_subtotal` | Sub total (ftXValue) (overrides `_csubtotal`) | Integer |
| `order_currency` | Currency (ftXCurrency) (overrides `_ccurrency`) | String |
| `order_type` | Cart or order type (overrides `_ctype`) | String |
| `product_quantity` | List of quantities (overrides `_cquan`) | Array |
| `ft_vars.ftXName` | Transaction name | String |

### Custom

| **Variable** | **Description** |
|:---------|:------------|
| `ft_vars.U1` | Custom variable 1  |
| `ft_vars.U2` | Custom variable 2  |
| `ft_vars.U3` | Custom variable 3  |
| `ft_vars.U4` | Custom variable 4  |
| `ft_vars.U5` | Custom variable 5  |
| `ft_vars.U6` | Custom variable 6  |
| `ft_vars.U7` | Custom variable 7  |
| `ft_vars.U8` | Custom variable 8  |
| `ft_vars.U9` | Custom variable 9  |
| `ft_vars.U10` | Custom variable 10  |
| `ft_vars.U11` | Custom variable 11  |
| `ft_vars.U12` | Custom variable 12  |
| `ft_vars.U13` | Custom variable 13  |
| `ft_vars.U14` | Custom variable 14  |
| `ft_vars.U15` | Custom variable 15  |
| `ft_vars.U16` | Custom variable 16  |
| `ft_vars.U17` | Custom variable 17  |
| `ft_vars.U18` | Custom variable 18  |
| `ft_vars.U19` | Custom variable 19  |
| `ft_vars.U20` | Custom variable 20  |

    