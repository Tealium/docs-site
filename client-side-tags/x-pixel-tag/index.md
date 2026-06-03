---
title: X Pixel Tag Setup Guide
description: This article describes how to set up the X Pixel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/x-pixel-tag/
---
The X Pixel helps you measure your return on investment by tracking the actions users take after viewing or engaging with your ads on X. X conversion tracking lets you attribute conversions beyond last link clicked, to include actions driven by all types of ad engagements, such as link clicks, posts, likes, and impressions.

## Tag tips

* Use mappings to:
  * Set up event triggers.
  * Map event-specific parameters to Event Code IDs.
  * Dynamically override standard config values.
  * Dynamically override E-Commerce extension values.
* Supports the following E-Commerce extension parameters:
  * Order ID
  * Order Total
  * Currency
  * List of Product IDs
  * List of Names
  * List of Categories
  * List of Quantities

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Pixel ID**: Also referred to as your X Pixel ID. You can find it in your X Pixel code snippet. For example, `pid` in the following snippet: `twq(&#39;config&#39;,&#39;pid&#39;);`.
* **Generate Event ID**: Automatically generate an event ID for every X tracking event.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The **Events** category is used to configure an event to trigger the pixel. The **Event-specific Parameters** category can be used to map other variables when the trigger event occurs.

### Configure an event to trigger the pixel

Use the following steps to configure an event to trigger the pixel:

1. Click **Data Mappings**.
1. Select a variable to trigger the pixel, then click **&#43; Select Destination**.
1. For **Category**, select **Events**. 
1. In the **Mapped variable equals** field, enter the value of the variable to trigger the pixel.
1. From your X Ads account, copy the Event ID for the event and paste it into the **Event Code ID** field.  
For example, `tw-o6ou1-o9l96`.
1. Click **&#43; Add**.
1. To map additional variables when the event occurs, follow these steps:  
    1. Select a variable, then click **&#43; Select Destination**.  
    1. For **Category**, select **Event-specific Parameters**.  
    1. Select the parameter to map the variable to.  
    1. Enter the Event ID from your X Ads account in the **Event Code ID** field.  
    1. Click **&#43; Add**.
1. Click **Finish**.
1. Save and publish.

### Standard Parameters

| Variable | Data Type | Description |
|---|---|---|
| `pixel_code` | String | X Pixel ID |
| `email_address` | String | Email address |
| `phone_number` | String | Phone number |
| `external_id` | String | External ID |
| `search_string` | String | Text that was searched for on your website |
| `description` | String | A string description for additional info |
| `twclid` | String | X click ID that can be included with any request |
| `status`  | String |Status of a sign up or subscription |

### E-Commerce

| Variable | Data Type | Description |
|---|---|---|
| `value` | Number | The total value of the conversion event. For example the monetary value of the transaction in case of a purchase. Maps to `_ctotal`. |
| `currency` | String | Currency denoted using the ISO 4217 code. For example, USD, JPY, or EUR. Maps to `_ccurrency`. |
| `conversion_id` | String | Unique identifier for a given purchase or order. Maps to `_corder`. |
| `content_type` | Array | Category of the product purchased. Maps to `_ccat`. |
| `content_id` | Array | For product catalog users, pass the product SKU. For all other use cases, pass Global Trade Item Number (GTIN), if available, otherwise pass the product SKU. Maps to `_csku`. |
| `content_name` | Array | Name of a product or service. Maps to `_cprodname`. |
| `content_price` | Array | Price of a product or service. Maps to `_cprice`. |
| `num_items` | Array | Number of products purchased. Maps to `_cquan`. |
| `content_group_id` | String | ID associated with a group of product variants. |

### Event-specific Parameters

For more information on mapping variables, see [Manage data mappings]().


| Variable             | Description                                 |
|----------------------|---------------------------------------------|
| `pixel_code`         | X Pixel ID                            |
| `email_address`      | Email address                               |
| `phone_number`       | Phone number                                |
| `external_id`        | External ID                                 |
| `search_string`      | Text that was searched for on your website  |
| `description`        | A string description for additional info    |
| `twclid`             | X click ID that can be included with any request |
| `order_total`        | Order total (Overrides `_ctotal`)           |
| `order_currency`     | Currency (Overrides `_ccurrency`)           |
| `order_id`           | Order ID (Overrides `_corder`)              |
| `product_category`   | List of categories (Overrides `_ccat`)      |
| `product_skus`       | List of SKUs (Overrides `_csku`)            |
| `product_names`      | List of names (Overrides `_cprodname`)      |
| `product_unit_price` | List of prices (Overrides `_cprice`)        |
| `product_quantity`   | List of quantities (Overrides `_cquan`)     |
| `content_group_id`   | ID associated with a group of product variants |
| `custom_parameter`   | Custom parameter                            |

