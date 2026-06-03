---
title: BloomReach Tag Setup Guide
description: This article describes how to set up the BloomReach tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/bloomreach-tag/
---
## Tag Configuration

First, go to the tag marketplace and add the BloomReach tag to your profile (See [Add a tag]()).

After adding the tag, configure the below settings:

* Account ID: Your BloomReach account ID.
* View ID: This BloomReach-provided ID is only required if you have multiple sites with unique product catalog characteristics using the same account ID.
* Domain Key: This BloomReach-provided ID is only required for a site with multiple language versions.
* Track TMS: Toggle tracking of Tealium as your Tag Management System (TMS). Only toggle to `Yes` when migrating your BloomReach implementation from another platform to Tealium, and you&#39;re still loading BloomReach on both platforms. The default is `No`. This allows BloomReach to distinguish the tracking calls from each platform.
* Clear `br_data` on Page View: Toggle whether to clear out the `br_data` object with each page view, or to allow persisted values to remain. This is often set to `Yes` for Single-page or AJAX applications. The default is `No`.

## Load Rules

[Load Rules]() determine when and where to load an instance of this tag on your site.

Recommended Load Rule: **All Pages**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The destination variables for the BloomReach tag are built into its **Data Mapping** tab. Available categories are:

### Standard/Global

| **Destination Name** | **Description**                                                                                                           |
|:---------------------|:--------------------------------------------------------------------------------------------------------------------------|
| Account ID           | Overrides your configured **Account ID**.                                                                                 |
| View ID              | Overrides your configured **View ID**.                                                                                    |
| Domain Key           | Overrides your configured **Domain Key**.                                                                                 |
| Title                | Overrides the Page Title with the title of the current page.                                                              |
| Currency             | Overrides the currency code for transactions.                                                                             |
| User ID              | Overrides the E-Commerce extension&#39;s `_ccustid` value.                                                                    |
| Track TMS Flag       | Overrides your configured Track TMS setting. The value must be the string `yes` to toggle on.                    |
| Clear br_data Flag   | Overrides your configured Clear `br_data` on Page View setting. The value must be the string `yes` to toggle on. |
| Event Group          | Map to override the default event group. Only override this after consulting with your BloomReach representative.         |
| Event Type           | Map to override the default event type. Only override this after consulting with your BloomReach representative.          |

### Page Type (`ptype`)

| **Destination Name** | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|:---------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ptype                | (Required for all page views) BloomReach has 7 page type classifications: `homepage`, `product`, `category`, `search`, `content`, `thematic`, and `other`. Set the `ptype` dynamically by entering the mapped variable&#39;s value and selecting the appropriate `ptype` from the dropdown.&lt;br&gt;&lt;br&gt;If your page type doesn&#39;t correspond to one of the supported BloomReach page types, then use `other`. Only set a custom ptype after consulting with your BloomReach representative. |

### Category Page

| **Destination Name** | **Description**                                                                                                                                                                                                                                                     |
|:---------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Category ID          | The unique category ID as referred to in your BloomReach database/catalog. The category ID needs to match the `crumb_id` in the feed. This is often a numeric ID or unique crumb path.&lt;br&gt;&lt;br&gt;If you are passing a crumb path, do not delimit the individual crumb values. |
| Category Name        | The breadcrumb of the page. Each crumb must be delimited by a pipe (&amp;#124;).                                                                                                                                                                                        |

### Conversion Page

| **Destination Name** | **Description**                                                                                                 |
|:---------------------|:----------------------------------------------------------------------------------------------------------------|
| Order ID             | The order or transaction ID for the conversion.                                                                 |
| Order Total          | The total price of the order, including taxes and shipping.                                                     |
| List of Product IDs  | An array of product IDs.                                                                                        |
| List of Names        | An array of product names.                                                                                      |
| List of SKUs         | An array of product SKUs.                                                                                       |
| List of Categories   | An array of product categories.                                                                                 |
| List of Prices       | An array of product prices.                                                                                     |
| List of Quantities   | An array of the number of each product in the order.                                                            |
| Is Conversion Flag   | Set this to `1` on a conversion or thank you page. This is automatically set to `1` when Order ID is populated. |

### Product Page

| **Destination Name** | **Description**            |
|:---------------------|:---------------------------|
| List of Product IDs  | An array of product IDs.   |
| List of Names        | An array of product names. |
| List of SKUs         | An array of product SKUs.  |

### Search Page

| **Destination Name** | **Description**                                    |
|:---------------------|:---------------------------------------------------|
| Search Term          | The value of the search query describing the page. |

### Virtual Page View

| **Destination Name**   | **Description**                                                                                                                                                                          |
|:-----------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Original Referring URL | When firing Virtual Page View events, this is the originally loaded page&#39;s URL. This is automatically captured when a Virtual Page View is fired, but can be overridden by mapping here. |

### Events

Map to these destinations for triggering specific events on a page. To trigger an event:

1. Select an event from the dropdown list. You may choose from the predefined list or create a Custom event. For a Custom event, enter a name with which to identify it. Please consult with your BloomReach representative before configuring any custom parameters or events.
1. In the **Trigger** field, enter the value of the variable being mapped.
1. To map more events, click the **&#43;** button and repeat steps 1 and 2.
1. Click **Apply**.

The event triggers when the supplied value is found in the data layer.

| **Destination Name** | **Description**                                                                                                                                                                                        |
|:---------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Add To Cart          | Trigger when a visitor adds an item to their cart. Default event group: `cart`. Default event type: `click-add`.                                                                                       |
| Content Page View    | Trigger when a visitor opens a non-product page dedicated to another page (for example, Recipe, Blog, or Article Pages).                                                                               |
| Content Search       | Trigger when a visitor performs a search.                                                                                                                                                              |
| QuickView            | Trigger when a visitor opens a quick view to display more details about a product. This usually occurs on a listing or category page. Default event group: `product`. Default event type: `quickview`. |
| Search Suggest       | Trigger when a visitor enters a search term and clicks submit, or an auto-suggest term pops up and the visitor clicks on it. Default event group: `suggest`. Default event types: `submit`, `click`.   |
| Virtual Page View    | Trigger when the current page is updated in a way that would be best tracked as a new page view. This is common with AJAX sites and single-page apps.                                                  |
| Widget Add-to-Cart   | Trigger when a visitor adds an item to their cart from a recommendation.                                                                                                                               |
| Widget Click         | Trigger when a visitor clicks an item from a recommendation.                                                                                                                                           |
| Widget View          | Trigger when a visitor views an item from a recommendation.                                                                                                                                            |
| Custom               | Trigger a custom event. Please consult with your BloomReach representative before configuring this.                                                                                                    |

### Event Parameters

This lets you map to a parameter for a specific event.

| **Destination Name**       | **Description**                                                                     |
|:---------------------------|:------------------------------------------------------------------------------------|
| Product ID (`prod_id`)     | The ID of the product for an Add to Cart or Quick View event.                       |
| Product Name (`prod_name`) | The name of the product for a Quick View event.                                     |
| Product SKU (`sku`)        | The SKU of the product for an Add to Cart or Quick View event.                      |
| Search Query (`q`)         | The search term entered by the visitor for a Search Suggest event.                  |
| Display Query (`aq`)       | The auto-suggested search term displayed to the visitor for a Search Suggest event. |

If you pass a Display Query parameter for a Search Suggest event, then the event type will be set to `click` automatically. Otherwise, the event type will be `submit`.

#### Segment Parameter

You can add a custom segment parameter with the `br_data.SEGMENT_NAME` destination name, where `SEGMENT_NAME` represents the segment name.

For example: `br_data.customer_tier = &#34;vip&#34;`

### Vendor Documentation

* [BloomReach JavaScript Tracking Pixel Reference](https://help.bloomreach.com/display/BRINT/JavaScript&#43;tracking&#43;pixel&#43;reference)
