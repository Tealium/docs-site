---
title: Namogoo Tag Setup Guide
description: This article describes how to set up the Namogoo tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/namogoo-tag/
---
Namogoo enhances the online customer experience by blocking unauthorized ads that intrude into web sessions, ensuring a focused and distraction-free browsing journey.

## Tag tips

* Use mapping to override the standard config values dynamically.
* Supports these E-Commerce extension parameters:
    * Cart Total
    * Order Total After Discount
    * Coupon Code
    * Num Of Items
    * Currency

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Client ID**: The Namogoo сlient (account) ID

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
| `client_Id`  | String | Client ID. |
| `cartTotal`  | Number | Cart total (overrides `_csubtotal`). |
| `orderTotalBeforeDiscount`  | Number | Order total before discount. |
| `orderTotalAfterDiscount`  | Number | Order total after discount (overrides `_ctotal`). |
| `couponCode`  | String | Coupon code (overrides `_cpromo`). |
| `numOfItems`  | Number | Number Of items (overrides `_cquan`). |
| `currency`  | String | Currency (overrides `_ccurrency`). |

### Events
To map events, see [Create an Event Mapping]().

| Variable | Description |
|:---------|:------------|
|  `addCartData` | Add cart data. |
|  `addOrderData` | Add order data. |

### Event-specific Parameters
To map events, see [Create an Event Mapping]().

| Variable | Description |
|:---------|:------------|
| `addCartData` | Add cart data. |
| `addOrderData` | Add order data. |
    