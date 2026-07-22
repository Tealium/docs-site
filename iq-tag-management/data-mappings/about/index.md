---
title: About data mappings
description: This article describes how to configure tag data mappings to send data from your data layer to a vendor.
url: https://docs.tealium.com/iq-tag-management/data-mappings/about/
---
A data mapping is a connection between a data layer variable and a vendor tag. Data mappings determine the data a tag receives and the type of event tracking it performs.

For example, a tag might collect the page name in a parameter named `pName`, but your data layer might store this value in a variable named `page_name`. To send the value of `page_name` to `pName`, you create a data mapping. After the mapping is configured, the value of `page_name` will always be passed to the vendor parameter `pName` when that tag is triggered.

![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-page-name-to-pname.png)

Data mappings are managed from the tag configuration. The list of supported vendor parameters is organized by category and available on the **Data Mappings** screen. First, you select the data layer variable to map, then choose the vendor parameter it maps to.

![](https://docs.tealium.com/images/iq-tag-management/data-mappings-select-destination.png)

## Variable mapping

There are two types of data mappings: variable mappings and custom value mappings. A variable mapping is the most common type since it allows values from your data layer to be passed to a vendor parameter.

## Event mapping

An event mapping is a variable mapping that associates your event names to the vendor's event names. For example, an e-commerce tag might run specific tracking functions for each of the primary shopping actions, such as searching for products, viewing product details, adding a product to the cart, checking out, and completing a purchase.

The vendor tag might offer the following tracked events for an e-commerce site:

* `viewItem`
* `viewSearchResult`
* `addToCart`
* `viewCart`
* `completeTransaction`

Similarly, your data layer might track these same events using `tealium_event` and the following values:

* `product_view`
* `search`
* `cart_add`
* `cart_view`
* `purchase`

An event mapping associates the values of your event variable ( `tealium_event` ) to the vendor's event names and triggers the corresponding tag function. Learn more about [mapping events](https://docs.tealium.com/manage-data-mappings/).

#### Example: Variable mapping

A tag vendor has a parameter for currency code, named `curr` , to be set to the three-character code matching the currency of a transaction. If the tag is loaded on pages that support multiple currencies, you would likely have a data layer variable called `site_currency` or `currency_code` that is set to the appropriate value for the current visitor. The expected values might be `USD`, `CAD`, `GBP`, `EUR`, `JPY`, and so on. The variable mapping would look like this:

![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-datamapping-variables.png)

## Custom value mapping

A custom value mapping is a convenient method for assigning a value directly in a mapping without using an extension or a data layer variable. The custom value is plain-text or the return value of a snippet of JavaScript code.

### Example: Custom value with plain text

A tag vendor has a parameter for currency code, named `curr` , but the tag is only deployed to a single geographic region where the currency is always the same (such as `CAD`). In this case, a data layer variable is not necessary because the value is constant throughout the site. The expected currency code, `CAD`, can be set directly as a custom value mapping, as follows:

![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-datamapping-customvalue.png)

### Example: Custom value with JavaScript code

The custom value can also be returned from JavaScript code. This option can be used to pass a JavaScript number, boolean, or array value to a vendor parameter. You can use advanced statements or even an inline function.

For example, the following line of JavaScript sets the mapping to `GB` if the `hostname` contains `co.uk`, otherwise it is set to `USD`:

```
location.hostname.indexOf("co.uk") > -1 ? "GBP" : "USD"
```

![](https://docs.tealium.com/images/iq-tag-management/iq-data-mappings-custom-value-jscode.jpg)

To reference a data layer variable such as `page_name`, use the `b` object. For example, `b['page_name']`. [Learn more about the b object](https://docs.tealium.com/platforms/javascript/the-b-object/).

## Mapping precedence

When two or more variables are mapped to the same destination, such as `page_name > pageName` and `Document Title > pageName`, the last mapping takes precedence. Data mappings can be reordered to account for this precedence.

![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-two-variabvles-mapped-to-same-destination.png)

In this example, if both `page_name` and `Document Title` are populated, the destination variable `pageName` will receive the value from `Document Title`. If the variables are populated, the last mapping takes precedence.

Learn more about [reordering data mappings](https://docs.tealium.com/manage-data-mappings/).


<blockquote>
If a variable does not have a value, the mapping is not applied.
</blockquote>

