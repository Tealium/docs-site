---
title: Exactag Tag Setup Guide
description: This article describes how to set up the Exactag tag in your Tealium iQ Tag Management account..
url: https://docs.tealium.com/client-side-tags/exactag-tag/
---

## Tag Tips

* Supports the E-Commerce extension for:
  * Order ID
  * Order Subtotal
  * Order Total
  * Order Coupon Code
  * Customer ID
  * Product ID
  * Product Name
  * Product Category
  * Product Quantity
  * Product Unit Price

* Conversion data automatically added when Order ID is present. Conversion data can be manually triggered by setting the **Is Conversion Flag** to `true`
* Additional data points can be added through the **UI Add Custom Destination** option

### Tag Configuration

First, go to the tag marketplace and add the Exactag tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Campaign Code**  
Your brand-specific Campaign Code

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable           | Description       |
|:-------------------|:------------------|
| Campaign Code      | (`campaign`)      |
| Referrer URL       | (`referrer`)      |
| Host Domain        | (`host`)          |
| Site Path          | (`site`)          |
| Search Parameters  | (`search`)        |
| Site Group         | (`sitegroup`)     |
| Cross Device ID    | (`crossid`)       |
| Subid              | (`subid`)         |
| Is Conversion Flag | (`is_conversion`) |

### E-Commerce

| Variable                                                   | Description                                |
|:-----------------------------------------------------------|:-------------------------------------------|
| Level Value                                                | (`level`)                                    |
| Customer Gender                                            | (`customer_gender`)                         |
| Customer Type                                              | (`customer_type`)                           |
| Order ID                                                   | (`order_id`) (Overrides `_corder`)           |
| Revenue/Order Total                                        | (`order_total`) (Overrides `_ctotal`)        |
| Total Price/Sub Total                                      | (`order_subtotal`) (Overrides `_csubtotal`)  |
| Promo Code                                                 | (`order_coupon_code`) (Overrides `_cpromo`) |
| Cart or Order Type                                         | (`order_type`) (Overrides `_ctype`)          |
| Customer ID                                                | (`customer_id`) (Overrides `_ccustid`)       |
| List of Product IDs (`product_id`) (Overrides `_cprod`)      | [Array]                                    |
| List of Names (`product_name`) (Overrides `_cprodname`)      | [Array]                                    |
| List of Categories (`product_category`) (Overrides `_ccat`)  | [Array]                                    |
| List of Quantities (`product_quantity`) (Overrides `_cquan`) | [Array]                                    |
| List of Prices (`product_unit_price`) (Overrides `_cprice`) | [Array]                                    |
