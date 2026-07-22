---
title: Naver Tag Setup Guide
description: This article describes how to set up the Naver tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/naver-tag/
---
## Tag Tips

* Use mapping to override the standard config values dynamically.
* Uses the following E-Commerce variables
  * `_ctotal`
* **Page Type** has the following options
  * None - 0
  * Checkout - 1
  * Sign-up - 2
  * Shopping Cart - 3
  * Book / Register - 4
  * Other - 5

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Account ID**: The Naver account ID.
* **Page Type**: This parameter is deprecated.
* **Sub Domain**: Set this parameter only if Naver specifies it.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `account_id` | Account ID. |
| `page_type` | Page type. |
| `subdomain` | Sub domain. |

### E-Commerce

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `order_total` | `Number` | Order total (Overrides `_ctotal`). |
| `type` | `String` | The type of the conversion event. |
| `id` | `String` | Conversion ID or customer's action ID. |
| `value` | `String` | Total price without shipping fees of all products and services in the order. |
| `item_id` | `Array` | Item ID (Overrides `_cprod`). |
| `name` | `Array` | Item name (Overrides `_cprodname`). |
| `category` | `Array` | Item category (Overrides `_ccat`). |
| `quantity` | `Array` | Item quantity (Overrides `_cquan`). |
| `payAmount` | `Array` | Total amount paid for the specific item. This is not a unit price. |
| `option` | `Array` | Item product options, such as color or size (for example: `color:red, size:240`). |

### Event Triggers

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Event | Description |
|:------|:------------|
| `purchase` | Purchase completed. |
| `begin_checkout` | Begin checkout. |
| `sign_up` | Sign up. |
| `add_to_cart` | Add to cart. |
| `schedule` | Booking completed. |
| `save_store` | Add/Save store. |
| `add_to_wishlist` | Add/Save to wish list. |
| `inquiry` | Inquiry/Contact us. |
| `call` | Phone call. |
| `lead` | Lead generated. |
| `view_product` | View product detail. |
| `view_content` | View content. |
| `search` | Search. |
| `share` | Share. |
| `clip_coupon` | Issue coupon. |
| `view_item_list` | View list. |
| `about_us` | View about us page. |
| `staff` | View service staff. |
| `location` | View business location/get directions. |
| `promotion` | Register for event/promotion. |
| `add_contact_method` | Add communication channel. |
| `opt_in_marketing` | Receive marketing communications. |
| `subscribe` | Subscribe. |
| `review` | Write review. |

### Event Specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Event | Description |
|:------|:------------|
| `order_total` | Order total (Overrides `_ctotal`). |
| `type` | The type of the conversion event. |
| `id` | Conversion ID or customer's action ID. |
| `value` | Total amount of multiple products or services. |
| `item_id` | Item ID (Overrides `_cprod`). |
| `name` | Item name (Overrides `_cprodname`). |
| `category` | Item category (Overrides `_ccat`). |
| `quantity` | Item quantity (Overrides `_cquan`). |
| `payAmount` | Total amount paid for the specific item. This is not a unit price. |
| `option` | Item product options, such as color or size (for example: `color:red, size:240`). |
| `purchase` | Purchase completed. |
| `begin_checkout` | Begin checkout. |
| `sign_up` | Sign up. |
| `add_to_cart` | Add to cart. |
| `schedule` | Booking completed. |
| `save_store` | Add/Save store. |
| `add_to_wishlist` | Add/Save to wish list. |
| `inquiry` | Inquiry/Contact us. |
| `call` | Phone call. |
| `lead` | Lead generated. |
| `view_product` | View product detail. |
| `view_content` | View content. |
| `search` | Search. |
| `share` | Share. |
| `clip_coupon` | Issue coupon. |
| `view_item_list` | View list. |
| `about_us` | View about us page. |
| `staff` | View service staff. |
| `location` | View business location/get directions. |
| `promotion` | Register for event/promotion. |
| `add_contact_method` | Add communication channel. |
| `opt_in_marketing` | Receive marketing communications. |
| `subscribe` | Subscribe. |
| `review` | Write review. |