---
title: LiveIntent Tag Setup Guide
description: This article describes how to set up the LiveIntent tag.
url: https://docs.tealium.com/client-side-tags/liveintent-tag/
---
### Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

After adding the tag, configure the below settings:

* App ID: Your unique App ID provided by LiveIntent.

### Load Rules

[Load Rules]() determine when and where to load an instance of this tag on your site.

Recommended Load Rule: **All Pages**

### Data Mappings

Mapping is the process of sending data from a [data layer variable](/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The destination variables for the LiveIntent tag are built into its **Data Mapping** tab. Available categories are:

#### Standard

|**Destination Name**| **Description**|
|---| ---|
|App ID (`app_id`)| Map to this destination to override or dynamically set the App ID|
| Content/Category/Conversion Name (`name`) |  Typically used to: &lt;ul&gt;&lt;li&gt;Pass product name for a `viewContent` event&lt;/li&gt;&lt;li&gt;Pass the category name for a `viewContent` event&lt;/li&gt;&lt;li&gt;Give the type of conversion a name for the conversion event&lt;/li&gt;&lt;/ul&gt; |
|Content ID (`contentID`)| A product ID that matches the product feed|
|Hashed User Email (`emailHash`)| The customer&#39;s email address as an MD5 hashed string|
|User Email (`email`)| The customer&#39;s email address in plain text|

#### E-Commerce

Since the LiveIntent tag is e-commerce enabled, it will automatically use the default E-Commerce Extension mappings. Manually mapping in this category is generally not needed unless:

* You want to override any extension mappings
* An e-commerce variable you want is not offered in the extension

|**Destination Name**| **Description**|
|---| ---|
| Order ID (`order_id`)| Unique identifier for this order. Use this to override the default e-commerce value `_corder`.|
| Order Total (`order_total`) | The total revenue for this order. Use this to override the default e-commerce value `_ctotal`.|
| Order Currency (`order_currency`) | Use this to override the default e-commerce value `_ccurrency`.|
| List of Product IDs (`product_id`) | The product ID for each line item. Use this to override the default e-commerce value `_cprod`.|
| List of Quantities (`product_quantity`) | Quantity of product for each line item. Use this to override the default e-commerce value `_cquan`.|
| List of Prices (`product_unit_price`) | The price of each item at point of sale. Use this to override the default e-commerce value `_cprice`.|

#### Events

Map to these destinations for triggering specific events on a page. To trigger an event:

1. Select an event from the drop-down list.  
You may choose from the predefined list or create a  event. For a  event, enter a name with which to identify it.
1. In the **Trigger** field, enter the value of the variable being mapped.
1. To map more events, click **&#43;** and repeat steps 1 and 2.
1. Click **Apply**.

The event triggers when the supplied value is found in the data layer.

|**Destination Name**| **Description**|
|---| ---|
| View Content (`content_view`) | A view of any content page which requires tracking|
| View Category (`category_view`) | A view of a category page|
| View Search Results (`search`) | A view of a search results page|
| Purchase (`purchase`) | Customer has completed an order|
| Add Product to Cart (`cart_add`) | Customer has added one or more items to the cart|
| Remove Product from Cart (`cart_remove`) | Customer has removed one or more items from the cart|
|Custom| Input a name for a custom event.|

#### Event Parameters

Map to these destinations if you want to pass additional data with the event(s) you mapped earlier.

Parameters are only used with predefined events. For more information on how to pass a parameter with a custom event, see .

To pass a parameter with a predefined event:

1. **Event**: Select a LiveIntent event from the drop-down list.
1. **Parameter**: Select a LiveIntent parameter from the drop-down list.
1. For a **Custom** parameter, enter a name with which to identify it.
1. Click **&#43; Add**.

|**Destination Name**| **Description**|
|---| ---|
|User Email (`email`)| Use to overwrite the standard configuration value on a per event basis.|
|Content/Category/Conversion Name (`name`)| Use to overwrite the standard configuration value on a per event basis.|
|Content ID (`contentId`)| Use to overwrite the standard configuration value on a per event basis.|
| Content Type (`contentType`) | The type of page being viewed. For example, `Product`, `LandingPage`, `Article`, `Hotel`, `Flight`, `Destination`.|
| Hashed User Email ( `emailHash`) | Use to overwrite the standard configuration value on a per event basis.|
| Page Number (`currentPage`) | The page number of the current page.|
| Search Term (`searchTerm`) | The term used in the search.|
|Product IDs (`itemIds`)| An array of product IDs of products shown on the page.|
|Custom| Custom parameter to be passed with a predefined event.|

#### Custom Event Data

Map to these destinations if you want to pass a custom parameter with a custom event that you mapped in the events tab.

To map a Custom Event Data variable:

1. **Event Action**: Enter the name of the Custom Event exactly as specified in the **Events** tab.
1. **Parameter**: Enter the name of the Parameter you want to send.
1. Click **&#43; Add**.

### Vendor Documentation

* [LiveConnect: Step-By-Step Implementation Guide](https://support.liveintent.com/hc/en-us/articles/115001542186-LiveConnect-Step-By-Step-Implementation-Guide-)
* [Dynamic Product Marketing: Overview](https://support.liveintent.com/hc/en-us/articles/212078166-Dynamic-Product-Marketing-Overview)
