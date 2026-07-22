---
title: True Fit Integration Tag Setup Guide
description: This article describes how to set up the True Fit Integration Tag tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/true-fit-integration-tag/
---
This article describes how to set up the True Fit Integration tag.

## Tag tips

* For questions, send email to `support@truefit.com`.
* PDP Integration: https://techdocs.truefitcorp.com/docs/product-detail-page-integration
* Order Confirmation Integration: https://techdocs.truefitcorp.com/docs/order-confirmation-integration
* This tag requires jQuery and may not be compatible with recent jQuery versions.
* This tag may require custom callback functions or divs on the page.
* For order tracking, map values to **registered**, **userid**, and **orderid**.
* Use mappings to do the following:
  * Set up event triggers
  * Dynamically override standard config values
  * Dynamically override E-Commerce extension values

* This tag supports the following E-Commerce extension parameters:
  * Order ID
  * User ID
  * Product ID
  * List of Product IDs
  * List of Unit Price
  * List of Quantities

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Store Key**: This is your store's three-letter acronym. Contact your True Fit project manager for assistance.
* **Environment**: Set this value to `staging` for your staging/development environments and `prod` for your production environment.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Configuration

| Variable | Description |
|:---------|:------------|
| Store Key `storeKey`  | String |
| Environment `environment`  | String |

### Standard

| Variable | Description |
|:---------|:------------|
| Locale `locale`  | String |
| Product Size `size`  | [Array of strings] |
| Product currency `currency`  | [Array of strings] |
| Color ID `colorId`  | [Array of strings] |
| Sales Group `salesGroup`  | [Array of strings] |

### E-Commerce

| Variable | Description |
|:---------|:------------|
| Order ID `orderId` (Overrides `_corder`)  | String |
| User ID `userId` (Overrides `_ccustid`)  | String |
| Product ID `productId` (Overrides `_cprod`)  | [Array of strings] |
| Product Quantity `product_quantity` (Overrides `_cquan`)  | [Array of numbers] |
| Product Unit Price `product_unit_price` (Overrides `_cprice`)  | [Array of numbers] |
| Product Sku `product_sku` (Overrides `_csku`)  | [Array of strings] |

### Events
To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| Checkout (checkout) | checkout |

### Event-specific Parameters
To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| Checkout (checkout) | checkout |

    