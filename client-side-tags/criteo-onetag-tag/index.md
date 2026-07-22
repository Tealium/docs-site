---
title: Criteo OneTag Tag Setup Guide
description: This article describes how to set up the Criteo OneTag tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/criteo-onetag-tag/
---
## Tag Tips

* Use mapping to:
  * Override the value for Account ID
  * Set values for required and optional parameters
  * Trigger events and set values for event parameters

* Supported E-Commerce extension parameters:
  * Order ID (`_corder`)
  * List of Product IDs (`_cprod`)
  * List of Quantities (`_cquan`)
  * List of Prices (`_cprice`)

## Tag Configuration

First, go to the tag marketplace and add the Criteo OneTag tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Account ID**: (Required) For multiple accounts, use a comma-separated list.
* **Generate Page View ID**: Automatically generate an page view ID for every Criteo tracking event for connector deduplication.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Tag destination       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|:----------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Account ID            | <ul><li>Criteo account number.</li><li>Overrides `account`.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                    |
| `email`               | <ul><li>String</li><li>Customer email address.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `retailer_visitor_id` | <ul><li>String</li><li>Retailer Visitor ID</li><li>A unique unauthenticated ID that is consistent over multiple sessions on the same device.</li></ul>                                                                                                                                                                                                                                                                                                               |
| `customer_id`         | <ul><li>String</li><li>Customer ID</li><li>An identifier for an authenticated user that is consistent for all logged in sessions.</li><li>Criteo requires that this ID not contain personally identifiable information such as names, email addresses, unencrypted phone numbers, etc.</li><li>Leave empty if the customer is unknown or your site does not have unique IDs.</li><li>This variable is not related to e-commerce extension `_ccustid` variable.</li></ul> |
| `site_type`           | <ul><li>Site type.</li><li>Version of the site.</li><li>The value can be one of the following:  <ul><li>`m` - The mobile version of your site</li><li>`t` - The tablet version of your site</li><li>`d` (default) - The classic version of your site. This is often the site that browsers access.</li></ul> </li></ul>                                                                                                                                                  |
| `hashed_email`        | <ul><li>Hashed email.</li><li>String</li><li>Customer hashed email address.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                    |
| `zip_code`            | <ul><li>String</li><li>Customer zip code.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                      |

### E-Commerce

| Tag Destination    | Description                                                                                                                             |
|:-------------------|:----------------------------------------------------------------------------------------------------------------------------------------|
| `order_id`         | <ul><li>Order ID</li><li>Unique transaction identifier.</li><li>Overrides `_corder`.</li></ul>                                          |
| Product IDs        | <ul><li>Array</li><li>Products ID</li><li>Unique identifier of each product in the product array.</li><li>Overrides `_cprod`.</li></ul> |
| Product Prices     | <ul><li>Array</li><li>Unit price of each product in the product array.</li><li>Overrides `_cprice`.</li></ul>                           |
| Product Quantities | <ul><li>Array</li><li>Quantity of each product in the product array.</li><li>Overrides `_cquan`.</li></ul>                              |

### Events

To trigger Criteo events on a page, map variables to these destinations. The event triggers when the supplied value is found in the data layer.

1. Select an event from the **Events** drop-down list.
1. In the **Trigger** field, enter the value of the variable being mapped.
1. Click **+ Add**.
1. To map more events, repeat steps 1, 2, and 3.

| Event Name         | Description                |
|:-------------------|:---------------------------|
| `viewHome`         | Home page viewed.          |
| `viewCategory`     | Product category viewed.   |
| `viewSearchResult` | Search results viewed.     |
| `viewItem`         | Product viewed.            |
| `viewBasket`       | Cart viewed.               |
| `viewList`         | List of products viewed.   |
| `addToCart`        | Product added to cart.     |
| `trackTransaction` | Transaction page activity. |

### Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of Criteo OneTag on your site.

Create custom Load Rules to load the tag on any page where you want trigger Criteo Events. For example, if you are tracking conversion events, load this tag on the checkout page or the confirmation page.

### Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The destination variables for Criteo OneTag are built into the **Data Mappings** tab. The available destination variables are described in the following sections.

#### Passing Parameters with Events

To pass additional data with the Event destinations you mapped earlier, map variables to the corresponding parameters. If a user has filtered a product list, the filters can be included as parameters.

To pass a parameter with a mapped Criteo event:

1. Select an event from the **Events** drop-down list.
1. Select a parameter from the **Parameters** drop-down list.
1. Click **+ Add**.

The available parameters and filters vary depending on the selected event, as shown in the following table:

| Event                                 | Parameters                                                                                                 | Filters                                               |
|:--------------------------------------|:-----------------------------------------------------------------------------------------------------------|:------------------------------------------------------|
| `viewHome`                            | <ul><li>Page ID</li><li>Custom</li></ul>                                                                   | <ul><li>None</li></ul>                                |
| `viewCategory`<br> `viewSearchResult` | <ul><li>Item</li><li>Keyword</li><li>Category</li><li>Page Number</li><li>Page ID</li><li>Custom</li></ul> | <ul><li>Name</li><li>Operator</li><li>Value</li></ul> |
| `viewItem`                            | <ul><li>Item</li><li>Price</li><li>Availability</li><li>Custom</li></ul>                                   | <ul><li>None</li></ul>                                |
| `viewBasket`<br> `addToCart`          | <ul><li>Page ID</li><li>Custom</li></ul>                                                                   | <ul><li>ID</li><li>Price</li><li>Quantity</li></ul>   |
| `viewList`                            | <ul><li>Item</li><li>Custom</li></ul>                                                                      | <ul><li>None</li></ul>                                |
| `trackTransaction`                    | <ul><li>Transaction ID</li><li>Custom</li></ul>                                                            | <ul><li>ID</li><li>Price</li><li>Quantity</li></ul>   |

## Vendor Documentation

* [Intro to the Criteo OneTag](https://support.criteo.com/s/article?article=criteo-onetag&language=en_US)
* [Criteo OneTag for Sponsored Products](https://support.criteo.com/s/article?article=360001467585-Criteo-OneTag-for-Sponsored-Products&language=en_US)
* [Criteo Support Center](https://support.criteo.com/hc/en-us) (login required)
