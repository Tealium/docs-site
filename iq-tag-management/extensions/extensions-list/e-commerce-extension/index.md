---
title: E-commerce Extension
description: The E-commerce extension defines a standard set of e-commerce variables such as Order Total and Product IDs that get automatically mapped them to vendor tags that support them.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/e-commerce-extension/
---
## Prerequisites

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

Older versions (4.37 and below) may impact execution, causing the extension to run twice.

## How it works

The E-Commerce extension is a global mapping for your e-commerce data layer variables. The tag integrations that expect e-commerce data reference these mappings automatically so that you don&#39;t have to map them manually in each tag.

The E-Commerce extension adds special variables to the data layer with names that are prefixed with `_c` to distinguish them from other variables. For example, when you map a variable to Order ID, that value will be stored in the data layer as `_corder`. These special e-commerce variables are referenced in the tag template code of vendor tags that expect this data.

## Using the extension

Before you begin, familiarize yourself with [how extensions work]().

Once the extension is added, map your data layer variables to their corresponding e-commerce variables by selecting them from the drop-down list. You may leave the mappings blank for unused variables.

The following example shows the mappings between data layer variables and e-commerce variables.

![](/images/iq-tag-management/e-commerce-extension-configuration-variables-naming-best-practices.png)

Hovering over each variable entry displays a tool tip to help you choose the correct variable.

The extension separates the E-commerce variables into two categories: order values and product values. The order values contain information about the order and customer. The product values contain information about the products in the order and are organized as lists.

### Order data

This table lists the e-commerce variables associated with order-level data.

The Order ID variable is a required mapping.

| **Order Value**    | **Description**                                                                                                                                                     | **Output variable** |
|:-------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------|
| Order ID           | Select the variable that contains the unique ID that identifies the customer&#39;s order. In order for the E-Commerce Extension to work, you must have order ID mapped. | `_corder`           |
| Order Total        | Select the variable that contains the total revenue value of the order.                                                                                             | `_ctotal`           |
| Sub Total          | Select the variable that contains the subtotal value of the order. This is the order total less the shipping and tax amounts.                                       | `_csubtotal`        |
| Shipping Amount    | Select the variable that contains the shipping amount for the order.                                                                                                | `_cship`            |
| Tax Amount         | Select the variable that contains the tax amount of the order.                                                                                                      | `_ctax`             |
| Store              | Select the variable that identifies the channel, site, or store in which the order occurs.                                                                          | `_cstore`           |
| Currency           | Select the variable that identifies the currency which the revenue is in.                                                                                           | `_ccurrency`        |
| Promo Code         | Select the variable that contains the voucher, promotion, or coupon code.                                                                                           | `_cpromo`           |
| Cart or Order Type | Select the variable that contains the cart, order, or customer type.                                                                                                | `_ctype`            |
| Customer ID        | Select the variable that contains the customer ID.                                                                                                                  | `_ccustid`          |
| Customer City      | Select the variable that identifies the customer&#39;s city, as identified by the customer&#39;s address.                                                                   | `_ccity`            |
| Customer State     | Select the variable that identifies the customer&#39;s state or province, as identified by the customer&#39;s address.                                                      | `_cstate`           |
| Customer Zip       | Select the variable that identifies the customer&#39;s zip code, as identified by the customer&#39;s address.                                                               | `_czip`             |
| Customer Country   | Select the variable that identifies the customer&#39;s country, as identified by the customer&#39;s address. The output variable is `_ccountry`.                            | `_ccountry`         |

The **Calculate Order Total ( `_ctotal`)** radio button lets you specify if the E-commerce extension computes the order total. For the majority of situations, the Order Total is calculated prior to data reaching the E-Commerce extension, so the default is set to **No**. If you want the E-commerce extension to calculate the order total for you, select **Yes**.

### Product data

This table lists the product-level e-commerce variables. Product variables are array so that they can hold multiple values.

| **Product Value**    | **Description**                                                                  | **Output variable** |
|:---------------------|:---------------------------------------------------------------------------------|:--------------------|
| List of Product IDs  | Select the variable that contains the product ID.                                | `_cprod`            |
| List of Names        | Select the variable that contains the name of the product.                       | `_cprodname`        |
| List of SKUs         | Select the variable that contains the product SKU.                               | `_csku`             |
| List of Brands       | Select the variable that contains the producs brand.                             | `_cbrand`           |
| List of Categories   | Select the variable that contains the product&#39;s primary category.                | `_ccat`             |
| List of Categories 2 | Select the variable that contains the product&#39;s secondary category.              | `_ccat2`            |
| List of Quantities   | Select the variable that contains the quantity of each product that was ordered. | `_cquan`            |
| List of Prices       | Select the variable that contains the product price.                             | `_cprice`           |
| List of Discounts    | Select the variable that contains product discount amounts.                      | `_cpdisc`           |

The **List Variable Type** droplist identifies the format in which the lists of product values is sent. The options are:

* **Array:** (Default) For example, `[&#34;product 1&#34;,&#34;product 2&#34;, &#34;product 3&#34;]`
* **String**: For example, `&#34;product 1, product 2, product 3&#34;`

To learn more about strings and arrays, see the [Strings vs. Arrays]() article.

The **Prices are in** radio button identifies the format in which product prices are displayed to the E-commerce extension. The options are:

* **Unit Price**: (Default) The price of the item, regardless of the quantity.
* **Line Price**: The price of the item multiplied by its quantity. If this option is selected, the E-commerce extension automatically converts it to **Unit Price**.

### Overriding E-commerce variables

When you set up the E-Ccommerce extension, the values you select in the extension are automatically sent to all tags that use E-commerce data. If you want to send the value of another variable instead of the E-commerce extension&#39;s variable, you do so by mapping the value you want to send in the mapped variables section for a tag&#39;s configuration. The **Mapping Toolbox** indicates which destinations override E-commerce mappings.

The following is an example of the **Mapping Toolbox** from the Google Universal Analytics tag:

![](/images/iq-tag-management/mappingtoolboxexample.png)

#### Adding E-commerce variable bundles

If you have not added the E-commerce extension and are adding [variable bundles](), the following bundles are automatically added and configure the E-commerce extension for you:

* E-commerce Variables bundle
* Demandware bundle (version 18.1 and earlier)
* Hybris bundle
* Magento bundle

If you added and configured the E-commerce extension before adding these bundles, adding a bundle does not overwrite or replace the existing E-commerce extension or its settings.
