---
title: Zaius Tag Setup Guide
description: This article describes how to set up Zaius in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/zaius-tag/
---
Zaius empowers marketers to understand and act on customer behavioral data.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* Tracker ID: Your Zaius-supplied Tracker ID.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

## Data mappings

Mapping is the process of sending data from a [data layer variable](/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The destination variables for the Zaius tag are built into its **Data Mapping** tab. Available categories are:

### Standard

|**Destination Name**| **Description**|
|---| ---|
|Tracker ID| Map to this destination to override or dynamically set the Tracker ID.|

### E-Commerce

Since the Zaius tag is e-commerce enabled, it will automatically use the default E-Commerce Extension mappings. Manually mapping in this category is generally not needed unless:

* You want to override any extension mappings.
* an e-commerce variable you want is not offered in the extension.

|**Destination Name**| **Description**|
|---| ---|
|First Name (first\_name)| Customer&#39;s first name on the order.|
|Last Name (last\_name)| Customer&#39;s last name on the order.|
|Phone (phone)| Phone number associated with the order.|
|Shipping Address (order\_ship\_address)| Shipping address for the order in the following format: street1, street2, city, state, zip, country.|
|Billing Address (order\_bill\_address)| Billing address for the order in the following format: street1, street2, city, state, zip, country.|
|Order ID (order\_id)| Unique identifier for this order. Use this to override the default e-commerce value `_corder`.|
|Order Total (order\_total)| The total revenue for this order. Use this to override the default e-commerce value `_ctotal`.|
|Order Sub Total (order\_subtotal)| The subtotal for the order. Use this to override the default e-commerce value `_csubtotal`.|
|Order Discount (order\_discount)| The order level discount applied to the order.|
|Order Shipping Amount (order\_shipping)| Shipping applied to the order. Use this to override the default e-commerce value `_cship`.|
|Order Tax Amount (order\_tax)| The tax applied to the order. Use this to override the default e-commerce value `_ctax`.|
|Promo Code (order\_coupon\_code)| The coupon code used for the order. Use this to override the default e-commerce value `_cpromo`.|
|Custom Order Data Item (order\_custom)| A custom data point applied to the order.|
|List of IDs (product\_name)| The product identifier for each line item. Use this to override the default e-commerce value `_cprod`.|
|List of Names (product\_name)| Use this to override the default e-commerce value `_cprodname`.|
|List of SKUs (product\_sku)| The product SKU for each line item. Use this to override the default e-commerce value `_csku`.|
|List of Brands (product\_brand)| The product brand for each line item. Use this to override the default e-commerce value `_cbrand`.|
|List of Categories (product\_category)| The product category for each line item. Use this to override the default e-commerce value `_ccat`.|
|List of Quantities (product\_quantity)| Quantity of product for each line item. Use this to override the default e-commerce value `_cquan`.|
|List of Prices (product\_unit\_price)| The price of each item at point of sale. Use this to override the default e-commerce value `_cprice`.|
|List of Discounts (product\_discount)| The discount amount applied each line item. Use this to override the default e-commerce value `_cpdisc`.|
|List of UPCs (product\_upc)| The product UPC for each line item.|
|List of Subtotals (product\_subtotal)| The subtotal for each line item.|
|List of Custom Product Info (custom\_product\_info)| A custom product data point for each line item.|

### Events

Map to these destinations for triggering specific events on a page. To trigger an event:

1. Select an event from the dropdown list. You may choose from the predefined list or create a &#39;Custom&#39; event. For a &#39;Custom&#39; event, enter a name with which to identify it.
1. In the **Trigger** field, enter the value of the variable being mapped.
1. To map more events, click the **&#43;** button and repeat steps #1 and #2.
1. Click **Apply**.

The event triggers when the supplied value is found in the data layer.

|**Destination Name**| **Description**|
|---| ---|
|Detail View (detail)| Visitor views an item detail page.|
|Add to Cart (add\_to\_cart)| Visitor adds an item to the cart.|
|Remove From Cart (remove\_from\_cart)| Visitor removes an item to the cart.|
|Purchase (purchase)| Visitor successfully completes the last step in the checkout process.|
|Return (return)| Visitor successfully completes a return on a previous order.|
|Refund (refund)| Visitor successfully completes a refund for a previous order.|
|Cancel (cancel)| Visitor successfully completes a cancelation on a previous order.|
|Identify (identify)| Add event association with visitor.|
|Anonymize (anonymize)| Remove event association with visitor.|
|Pageview (pageview)| Visitor views any page on your site.|

### Event Parameters

Map to these destinations if you want to pass additional data with the event(s) you mapped earlier.

Note: Parameters are only used with pre-defined events. See Custom Event Data to learn how to pass a parameter with a custom event.

To pass a parameter with a pre-defined event:

1. Event: Select a Zaius event from the drop-down list.
1. Parameter: Select a Zaius Parameter from the dropdown list.
1. For a Custom parameter, enter a name with which to identify it.
1. Click **&#43;Add**.

|**Destination Name**| **Description**|
|---| ---|
|Customer ID (customer\_id)| The identifier of the customer associated with this event.|
|Email (email)| The email address of the customer associated with this event.|
|Category (category)| The category associated with this event. This can either be a flat category (Laptops) or hierarchical category using &amp;gt; as delimiters (Electronics &amp;gt; Computers &amp;gt; Laptops).|
|Search Term (search\_term)| Search term for on-site search.|
|Paginate Result Count (paginate\_result\_count)| Number of results in a search pagination.|
|Paginate Page Number (paginate\_page\_number)| Page depth of search pagination.|
|Filter Field (filter\_field)| Field name for search or navigation filter.|
|Filter Value (filter\_value)| Field value for search or navigation filter.|
|Sort Direction (sort\_direction)| Sort direction of results from search or navigation filter.|
|Sort Field (sort\_field)| Sort field for results from search or navigation filter.|
|Carousel Page Number (carousel\_page\_number)| Page depth of carousel scroll.|
|Page (page)| The path of the URL requested.|
|Custom| Custom parameter to be passed with a predefined event.|

### Custom Event Data

Map to these destinations if you want to pass a custom parameter with a custom Event that you mapped in the Events tab.

To map a Custom Event Data variable:

1. Event Action: Enter the name of the Custom Event exactly as specified in the Events tab.
1. Parameter: Enter the name of the parameter you want to send.
1. Click **&#43;Add**.

## Vendor documentation

* [JavaScript Reference](https://developers.zaius.com/reference)
