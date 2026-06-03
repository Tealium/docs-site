---
title: ShopMessage Tag Setup Guide
description: This article describes how to set up the ShopMessage tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/shopmessage-tag/
---
## Tag Tips

* The PurchaseComplete Event fires when an Order ID is present.
* Use mapping to:
  * Dynamically override the standard config values
  * Configure event triggers
  * Send required, optional, and custom event parameters
  * Override the E-Commerce extension values
  * Use **Custom Product Variable Name** for any Product variables not listed by replacing `custom` with the variable you want to send

* Supports these E-commerce extension parameters:
  * Order ID
  * Order Total
  * Order Subtotal
  * Shipping Amount
  * Tax Amount
  * Currency
  * Customer ID
  * Customer City
  * Customer State
  * Customer Zip
  * Customer Country
  * List of Product IDs
  * List of Names
  * List of SKUs
  * List of Categories
  * List of Quantities
  * List of Prices

* Implementation Guide: &lt;https://help.shopmessage.me/en/articles/1443137-integrating-shopmessage-with-your-store&gt;

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the ShopMessage tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Account ID**: An alphanumerical value found in the src URL
* **c_id**: An alphanumerical value found after `initialize.js?c=` in the src URL
* **Facebook Login**
* **Facebook Optin**

### Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

#### Standard

| Variable                     | Description      |
|:-----------------------------|:-----------------|
| Account ID                   | (`account_id`)  |
| `c_id`                      | (`c_id`)        |
| Facebook Login (`fb_login`) | [`true`/`false`] |
| Facebook Optin (`fb_optin`) | [`true`/`false`] |

#### E-Commerce

| Variable                                                   | Description                                   |
|:-----------------------------------------------------------|:----------------------------------------------|
| Order ID                                                   | (`order_id`) (Overrides `_corder`)          |
| Order Total                                                | (`order_total`) (Overrides `_ctotal`)       |
| Order Subtotal                                             | (`order_subtotal`) (Overrides `_csubtotal`) |
| Shipping Amount                                            | (`order_shipping`) (Overrides `_cship`)         |
| Tax Amount                                                 | (`order_tax`) (Overrides `_ctax`)               |
| Currency                                                   | (`order_currency`) (Overrides `_ccurrency`)     |
| Customer ID                                                | (`customer_id`) (Overrides `_ccustid`)          |
| Customer City                                              | (`customer_city`) (Overrides `_ccity`)          |
| Customer State                                             | (`customer_state`) (Overrides `_cstate`)        |
| Customer Zip                                               | (`customer_zip`) (Overrides `_czip`)            |
| Customer Country                                           | (`customer_country`) (Overrides `_ccountry`)    |
| List of Product IDs (`product_id`) (Overrides `_cprod`)      | [Array]                                       |
| List of Names (`product_name`) (Overrides `_cprodname`)      | [Array]                                       |
| List of SKUs (`product_sku`) (Overrides `_csku`)             | [Array]                                       |
| List of Categories (`product_category`) (Overrides `_ccat`)  | [Array]                                       |
| List of Quantities (`product_quantity`) (Overrides `_cquan`) | [Array]                                       |
| List of Prices (`product_unit_price`) (Overrides `_cprice`) | [Array]                                       |

#### Event Triggers

| Variable         | Description      |
|:-----------------|:-----------------|
| `ViewProduct`      | ViewProduct      |
| `UpdateCart`       | UpdateCart       |
| `PurchaseComplete` | PurchaseComplete |

#### Event Data: ViewProduct

| Variable     | Description                                                         |
|:-------------|:--------------------------------------------------------------------|
| Title        | (`ViewProduct.title`) (Overrides E-Commerce Product Name)             |
| Price        | (`ViewProduct.price`) (Overrides E-Commerce Product Unit Price)       |
| Product ID   | (`ViewProduct.product_id`) (Overrides E-Commerce Product ID)         |
| Product Type | (`ViewProduct.product_type`) (Overrides E-Commerce Product Category) |
| Color        | (`ViewProduct.color`)                                                 |
| Style        | (`ViewProduct.style`)                                                 |
| Image        | (`ViewProduct.image`)                                                 |
| Product URL  | (`ViewProduct.product_url`)                                          |
| Tags         | (`ViewProduct.tags`)                                                  |
| Vendor       | (`ViewProduct.vendor`)                                                |

#### Event Data: UpdateCart

| Variable                                                                             | Description                                                  |
|:-------------------------------------------------------------------------------------|:-------------------------------------------------------------|
| Total Price                                                                          | (`UpdateCart.total_price`) (Overrides E-Commerce Order Total) |
| CTA URL                                                                              | (`UpdateCart.cta_url`)                                        |
| Product Title (`UpdateCart.items.title`) (Overrides E-Commerce Product Name)           | [Array]                                                      |
| Product Price (`UpdateCart.items.price`) (Overrides E-Commerce Product Unit Price)     | [Array]                                                      |
| Product Currency (`UpdateCart.items.currency`) (Overrides E-Commerce Currency)         | [Array]                                                      |
| Product ID (`UpdateCart.items.product_id`) (Overrides E-Commerce Product ID)          | [Array]                                                      |
| Variant ID (`UpdateCart.items.variant_id`)                                            | [Array]                                                      |
| Product SKU (`UpdateCart.items.sku`)                                                   | [Array]                                                      |
| Product Size (`UpdateCart.items.size`)                                                 | [Array]                                                      |
| Product Color (`UpdateCart.items.color`)                                               | [Array]                                                      |
| Product Image (`UpdateCart.items.image`)                                               | [Array]                                                      |
| Product URL (`UpdateCart.items.product_url`)                                          | [Array]                                                      |
| Product Quantity (`UpdateCart.items.quantity`) (Overrides E-Commerce Product Quantity) | [Array]                                                      |
| Product Tags (`UpdateCart.items.tags`)                                                 | [Array]                                                      |
| Custom Product Variable Name (`UpdateCart.items.custom`)                               | [Array]                                                      |

#### Event Data: PurchaseComplete

| Variable                                                                                   | Description                                                                      |
|:-------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------|
| Order ID                                                                                   | (`PurchaseComplete.order_id`) (Overrides E-Commerce Order ID)                     |
| Checkout Token                                                                             | (`PurchaseComplete.checkout_token`)                                               |
| Created at                                                                                 | (`PurchaseComplete.created_at`)                                                   |
| Order Status URL                                                                           | (`PurchaseComplete.order_status_url`)                                            |
| Currency                                                                                   | (`PurchaseComplete.currency`) (Overrides E-Commerce Currency)                      |
| Total Price                                                                                | (`PurchaseComplete.total_price`) (Overrides E-Commerce Order Total)               |
| Subtotal Price                                                                             | (`PurchaseComplete.subtotal_price`) (Overrides E-Commerce Order Subtotal)         |
| Total Tax                                                                                  | (`PurchaseComplete.total_tax`) (Overrides E-Commerce Tax Amount)                  |
| Shipping Price                                                                             | (`PurchaseComplete.shipping_price`) (Overrides E-Commerce Shipping Amount)        |
| Platform                                                                                   | (`PurchaseComplete.platform`)                                                      |
| Address 1                                                                                  | (`PurchaseComplete.shipping_address.address1`)                                    |
| Address 2                                                                                  | (`PurchaseComplete.shipping_address.address2`)                                    |
| First Name                                                                                 | (`PurchaseComplete.shipping_address.first_name`)                                 |
| Last Name                                                                                  | (`PurchaseComplete.shipping_address.last_name`)                                  |
| Full Name                                                                                  | (`PurchaseComplete.shipping_address.full_name`)                                  |
| City                                                                                       | (`PurchaseComplete.shipping_address.city`) (Overrides E-Commerce Customer City)   |
| State                                                                                      | (`PurchaseComplete.shipping_address.state`) (Overrides E-Commerce Customer State) |
| Zip Code                                                                                   | (`PurchaseComplete.shipping_address.zip`) (Overrides E-Commerce Customer Zip)     |
| Phone Number                                                                               | (`PurchaseComplete.shipping_address.phone`)                                       |
| Product Title (`PurchaseComplete.items.title`) (Overrides E-Commerce Product Name)           | [Array]                                                                          |
| Product Price (`PurchaseComplete.items.price`) (Overrides E-Commerce Product Unit Price)     | [Array]                                                                          |
| Product ID (`PurchaseComplete.items.product_id`) (Overrides E-Commerce Product ID)          | [Array]                                                                          |
| Variant ID (`PurchaseComplete.items.variant_id`)                                            | [Array]                                                                          |
| Product SKU (`PurchaseComplete.items.sku`) (Overrides E-Comemrce Product SKU)                | [Array]                                                                          |
| Product Size (`PurchaseComplete.items.size`)                                                 | [Array]                                                                          |
| Product Color (`PurchaseComplete.items.color`)                                               | [Array]                                                                          |
| Product Image (`PurchaseComplete.items.image`)                                               | [Array]                                                                          |
| Product URL (`PurchaseComplete.items.product_url`)                                          | [Array]                                                                          |
| Product Quantity (`PurchaseComplete.items.quantity`) (Overrides E-Commerce Product Quantity) | [Array]                                                                          |
| Product Tags (`PurchaseComplete.items.tags`)                                                 | [Array]                                                                          |
| Custom Product Variable Name (`PurchaseComplete.items.custom`)                               | [Array]                                                                          |
| Customer Email                                                                             | (`PurchaseComplete.customer_properties.email`)                                    |
| Customer ID                                                                                | (`PurchaseComplete.customer_properties.id`) (Overrides E-Commerce Customer ID)    |
| Customer First Name                                                                        | (`PurchaseComplete.customer_properties.first_name`)                              |
| Customer Last Name                                                                         | (`PurchaseComplete.customer_properties.last_name`)                               |

#### Visitor Parameters

| Variable        | Description                                               |
|:----------------|:----------------------------------------------------------|
| Customer ID     | (`visitor.customer_id`) (Overrides E-Commerce Customer ID) |
| Address 1       | (`visitor.address1`)                                        |
| Address 2       | (`visitor.address2`)                                        |
| First Name      | (`visitor.first_name`)                                     |
| Last Name       | (`visitor.last_name`)                                      |
| Full Name       | (`visitor.full_name`)                                      |
| Gender          | (`visitor.gender`)                                          |
| Language        | (`visitor.language`)                                        |
| City            | (`visitor.city`) (Overrides E-Commerce Customer City)       |
| State           | (`visitor.state`) (Overrides E-Commerce Customer State)     |
| Zip Code        | (`visitor.zip`) (Overrides E-Commerce Customer Zip)         |
| Phone Number    | (`visitor.phone`)                                           |
| Profile Picture | (`visitor.profile_pic`)                                    |
