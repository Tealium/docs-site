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

First, go to the tag marketplace and add the Criteo OneTag tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Account ID**: (Required) For multiple accounts, use a comma-separated list.
* **Generate Page View ID**: Automatically generate an page view ID for every Criteo tracking event for connector deduplication.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Tag destination       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|:----------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Account ID            | &lt;ul&gt;&lt;li&gt;Criteo account number.&lt;/li&gt;&lt;li&gt;Overrides `account`.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                                                    |
| `email`               | &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Customer email address.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `retailer_visitor_id` | &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Retailer Visitor ID&lt;/li&gt;&lt;li&gt;A unique unauthenticated ID that is consistent over multiple sessions on the same device.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                               |
| `customer_id`         | &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Customer ID&lt;/li&gt;&lt;li&gt;An identifier for an authenticated user that is consistent for all logged in sessions.&lt;/li&gt;&lt;li&gt;Criteo requires that this ID not contain personally identifiable information such as names, email addresses, unencrypted phone numbers, etc.&lt;/li&gt;&lt;li&gt;Leave empty if the customer is unknown or your site does not have unique IDs.&lt;/li&gt;&lt;li&gt;This variable is not related to e-commerce extension `_ccustid` variable.&lt;/li&gt;&lt;/ul&gt; |
| `site_type`           | &lt;ul&gt;&lt;li&gt;Site type.&lt;/li&gt;&lt;li&gt;Version of the site.&lt;/li&gt;&lt;li&gt;The value can be one of the following:  &lt;ul&gt;&lt;li&gt;`m` - The mobile version of your site&lt;/li&gt;&lt;li&gt;`t` - The tablet version of your site&lt;/li&gt;&lt;li&gt;`d` (default) - The classic version of your site. This is often the site that browsers access.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt;                                                                                                                                                  |
| `hashed_email`        | &lt;ul&gt;&lt;li&gt;Hashed email.&lt;/li&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Customer hashed email address.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                                    |
| `zip_code`            | &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Customer zip code.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                                                                      |

### E-Commerce

| Tag Destination    | Description                                                                                                                             |
|:-------------------|:----------------------------------------------------------------------------------------------------------------------------------------|
| `order_id`         | &lt;ul&gt;&lt;li&gt;Order ID&lt;/li&gt;&lt;li&gt;Unique transaction identifier.&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt;                                          |
| Product IDs        | &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Products ID&lt;/li&gt;&lt;li&gt;Unique identifier of each product in the product array.&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
| Product Prices     | &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Unit price of each product in the product array.&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt;                           |
| Product Quantities | &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Quantity of each product in the product array.&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt;                              |

### Events

To trigger Criteo events on a page, map variables to these destinations. The event triggers when the supplied value is found in the data layer.

1. Select an event from the **Events** drop-down list.
1. In the **Trigger** field, enter the value of the variable being mapped.
1. Click **&#43; Add**.
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

[Load Rules]() determine when and where to load an instance of Criteo OneTag on your site.

Create custom Load Rules to load the tag on any page where you want trigger Criteo Events. For example, if you are tracking conversion events, load this tag on the checkout page or the confirmation page.

### Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The destination variables for Criteo OneTag are built into the **Data Mappings** tab. The available destination variables are described in the following sections.

#### Passing Parameters with Events

To pass additional data with the Event destinations you mapped earlier, map variables to the corresponding parameters. If a user has filtered a product list, the filters can be included as parameters.

To pass a parameter with a mapped Criteo event:

1. Select an event from the **Events** drop-down list.
1. Select a parameter from the **Parameters** drop-down list.
1. Click **&#43; Add**.

The available parameters and filters vary depending on the selected event, as shown in the following table:

| Event                                 | Parameters                                                                                                 | Filters                                               |
|:--------------------------------------|:-----------------------------------------------------------------------------------------------------------|:------------------------------------------------------|
| `viewHome`                            | &lt;ul&gt;&lt;li&gt;Page ID&lt;/li&gt;&lt;li&gt;Custom&lt;/li&gt;&lt;/ul&gt;                                                                   | &lt;ul&gt;&lt;li&gt;None&lt;/li&gt;&lt;/ul&gt;                                |
| `viewCategory`&lt;br&gt; `viewSearchResult` | &lt;ul&gt;&lt;li&gt;Item&lt;/li&gt;&lt;li&gt;Keyword&lt;/li&gt;&lt;li&gt;Category&lt;/li&gt;&lt;li&gt;Page Number&lt;/li&gt;&lt;li&gt;Page ID&lt;/li&gt;&lt;li&gt;Custom&lt;/li&gt;&lt;/ul&gt; | &lt;ul&gt;&lt;li&gt;Name&lt;/li&gt;&lt;li&gt;Operator&lt;/li&gt;&lt;li&gt;Value&lt;/li&gt;&lt;/ul&gt; |
| `viewItem`                            | &lt;ul&gt;&lt;li&gt;Item&lt;/li&gt;&lt;li&gt;Price&lt;/li&gt;&lt;li&gt;Availability&lt;/li&gt;&lt;li&gt;Custom&lt;/li&gt;&lt;/ul&gt;                                   | &lt;ul&gt;&lt;li&gt;None&lt;/li&gt;&lt;/ul&gt;                                |
| `viewBasket`&lt;br&gt; `addToCart`          | &lt;ul&gt;&lt;li&gt;Page ID&lt;/li&gt;&lt;li&gt;Custom&lt;/li&gt;&lt;/ul&gt;                                                                   | &lt;ul&gt;&lt;li&gt;ID&lt;/li&gt;&lt;li&gt;Price&lt;/li&gt;&lt;li&gt;Quantity&lt;/li&gt;&lt;/ul&gt;   |
| `viewList`                            | &lt;ul&gt;&lt;li&gt;Item&lt;/li&gt;&lt;li&gt;Custom&lt;/li&gt;&lt;/ul&gt;                                                                      | &lt;ul&gt;&lt;li&gt;None&lt;/li&gt;&lt;/ul&gt;                                |
| `trackTransaction`                    | &lt;ul&gt;&lt;li&gt;Transaction ID&lt;/li&gt;&lt;li&gt;Custom&lt;/li&gt;&lt;/ul&gt;                                                            | &lt;ul&gt;&lt;li&gt;ID&lt;/li&gt;&lt;li&gt;Price&lt;/li&gt;&lt;li&gt;Quantity&lt;/li&gt;&lt;/ul&gt;   |

## Vendor Documentation

* [Intro to the Criteo OneTag](https://support.criteo.com/s/article?article=criteo-onetag&amp;language=en_US)
* [Criteo OneTag for Sponsored Products](https://support.criteo.com/s/article?article=360001467585-Criteo-OneTag-for-Sponsored-Products&amp;language=en_US)
* [Criteo Support Center](https://support.criteo.com/hc/en-us) (login required)
