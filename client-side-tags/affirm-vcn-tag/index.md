---
title: Affirm Virtual Card Integration (VCN Integration) Tag Setup Guide
description: This article describes how to set up the Affirm Virtual Card Integration (VCN Integration) tag.
url: https://docs.tealium.com/client-side-tags/affirm-vcn-tag/
---
## Tag Tips

*   All dollar values should be in string format with a decimal and two digits after the decimal.
*   Use mapping to:
    *   Override the standard config values.
    *   Override the E-Commerce extension values.
*   Supports the following E-Commerce extension parameters:
    *   Store
    *   Customer City
    *   Customer State
    *   Customer ZIP
    *   Customer Country
    *   List of Product Names
    *   List of SKUs
    *   List of Prices
    *   List of Quantities
    *   Tax Amount
    *   Shipping Amount
    *   Order Total
    *   Order ID
*  Destinations with "Overrides E-Commerce extension" in the description do not require mapping if you have the E-Commerce extension enabled and configured for those parameters.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Environment**: The environment for this tag to use at Affirm.
* **Sandbox API Key**: (Required for Sandbox environment) Available in your Sandbox Affirm Dashboard.
* **Production API Key**:(Required for Production environment) Available in your Production Affirm Dashboard.
* **Success Callback Function Name**: (Required) The name of your checkout success callback function.
* **Error Callback Function Name**: (Required) The name of your checkout error callback function.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `environment` | String | Environment |

### Checkout Data

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `checkout_data.merchant.name` | String | Merchant name |
| `checkout_data.billing.name.first` | String | Billing first name |
| `checkout_data.billing.name.last` | String | Billing last name |
| `checkout_data.billing.name.full` | String | Billing full name |
| `checkout_data.billing.address.line1` | String | Billing address line 1 |
| `checkout_data.billing.address.line2` | String | Billing address line 2 |
| `checkout_data.billing.address.city` | String | Billing address city |
| `checkout_data.billing.address.state` | String | Billing address state |
| `checkout_data.billing.address.zipcode` | String | Billing address ZIP code |
| `checkout_data.billing.address.country` | String | Billing address country |
| `checkout_data.billing.phone_number` | String | Billing phone number |
| `checkout_data.billing.email` | String | Billing email |
| `checkout_data.shipping.name.first` | String | Shipping first name |
| `checkout_data.shipping.name.last` | String | Shipping last name |
| `checkout_data.shipping.name.full` | String | Shipping full name |
| `checkout_data.shipping.address.line1` | String | Shipping address line 1 |
| `checkout_data.shipping.address.line2` | String | Shipping address line 2 |
| `checkout_data.shipping.address.city` | String | Shipping address city |
| `checkout_data.shipping.address.state` | String | Shipping address state |
| `checkout_data.shipping.address.zipcode` (Overrides E-Commerce extension) | String | Shipping address ZIP code |
| `checkout_data.shipping.address.country` | String | Shipping address country |
| `checkout_data.shipping.phone_number` | String | Shipping phone number |
| `checkout_data.shipping.email` | String | Shipping email |
| `checkout_data.items.display_name` | Array of Strings | List of item display names |
| `checkout_data.items.sku` | Array of Strings | List of item SKUs |
| `checkout_data.items.unit_price` | Array of Strings | List of item unit prices |
| `checkout_data.items.qty` | Array of Strings | List of item quantities |
| `checkout_data.items.item_image_url` | Array of Strings | List of item image URLs |
| `checkout_data.items.item_url` | Array of Strings | List of item URLs |
| `checkout_data.items.categories` | Array of Arrays | List of item categories |
| `checkout_data.discounts` | Object | Discounts |
| `checkout_data.tax_amount` | String | Tax amount |
| `checkout_data.shipping_amount` | String | Shipping amount |
| `checkout_data.total` | String | Order total |
| `checkout_data.metadata.custom` | String | Order metadata |
| `checkout_data.order_id` | String | Order ID |