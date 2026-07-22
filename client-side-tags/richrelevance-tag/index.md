---
title: RichRelevance Tag Setup Guide
description: This article describes how to set up the RichRelevance tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/richrelevance-tag/
---
RichRelevance powers personalized shopping experiences for the world’s largest and most innovative retail brands, including Wal-Mart, Sears, Overstock.com and others.

## Tag Tips

* Supports these e-commerce extension values:
  * Order ID
  * List of Product IDs
  * List of Product Names
  * List of Brands
  * List of Categories (Category ID)
  * List of Categories 2 (Category Name)
  * List of Quantities
  * List of Prices

* Use mapping to override the following:
  * Override the standard configuration values
  * Override the e-commerce extension values
  * Define placement lists
  * Block Items by ID

* The **Page Type** is automatically set to **Purchase Complete Page** (`purchase`) when an **Order ID** (`order_id`) is set.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **API Key**: Your RichRelevance API Key.
* **Page Type**: The **Home Page** (`home`) is typically any generic page that does not have a specific product or product category associated to it. Use data mappings to override this selection. The **Page Type** will automatically be set to **Purchase Complete Page** (`purchase`) when an **Order ID** is set.
* **Test Domains**: A comma-separated list of domain names for pre-production sites, for example, `dev.mydomain.com` or `qa.mydomain.com`. Calls to RichRelevance from these domains will go to `integration.richrelevance.com` instead of `recs.richrelevance.com`.
* **Force Dev Mode**: Forces the recommendation engine to ignore the current user's behavior. For use only in Dev and QA environments.
* **Force Display**: Overrides the **Display recommendations onsite** configuration. Use **Force Display** in a development environment to see recommendations when the customer-facing site is not ready for recommendation display. For use only in Dev and QA environments.
* **Use Dummy Data**: A method for using random products from the product cache to provide recommendations for a merchant. If the product cache is empty, a static recommendation set (not from the merchant's catalog) is used.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable                                 | Description            |
|:-----------------------------------------|:-----------------------|
| API Key (`api_key`)                      | [String]               |
| Page Type (`page_type`)                  | [String]               |
| Test Domains (`test_domains`)            | (comma-separated list) |
| List of Placements (`placements`)        | [Array]                |
| Session ID (`user_session_id`)           | [String]               |
| User ID (`user_id`)                      | [String]               |
| Channel API Key (`channel`)              | [String]               |
| Search Terms (`search_terms`)            | [String]               |
| Order ID (`order_id`)                    | [String]               |
| List of Product IDs ( `product_id` )     | [Array]                |
| List of Product Names ( `product_name` ) | [Array]                |
| List of Prices ( `price` )               | [Array]                |
| List of Quantitites ( `qty` )            | [Array]                |
| List of SKUs ( `product_sku` )           | [Array]                |
| Category ID (`category_id`)              | [String]               |
| Category Name (`category_name`)          | [String]               |
| Brand (`brand`)                          | [String]               |
| Force Dev Mode (`forceDevMode`)          | [Boolean]              |
| Force Display Mode (`forceDisplayMode`)  | [Boolean]              |
| Use Dummy Data (`useDummyData`)          | [Boolean]              |
| Block Item ID (`blockItemId`)            | [Array]                |
| Registry ID (`registry_id`)              | [String]               |

### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

| Variable                               | Description     |
|:---------------------------------------|:----------------|
| Home Page (`home`)                     | `home`          |
| Search Page (`search`)                 | `search`        |
| Item Page (`item`)                     | `item`          |
| Category Page (`category`)             | `category`      |
| Personal Page (`personal`)             | `personal`      |
| Brand Page (`brand`)                   | `brand`         |
| Add to Cart Page (`addtocart`)         | `addtocart`     |
| Cart Page (`cart`)                     | `cart`          |
| Purchase Complete Page (`purchase`)    | `purchase`      |
| Error Page (`error`)                   | `error`         |
| Add to Registry Page (`addtoregistry`) | `addtoregistry` |
| Generic Page (`generic`)               | `generic`       |
| Wish List Page (`wishlist`)            | `wishlist`      |

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

| Variable                               | Description     |
|:---------------------------------------|:----------------|
| Home Page (`home`)                     | `home`          |
| Search Page (`search`)                 | `search`        |
| Item Page (`item`)                     | `item`          |
| Category Page (`category`)             | `category`      |
| Personal Page (`personal`)             | `personal`      |
| Brand Page (`brand`)                   | `brand`         |
| Add to Cart Page (`addtocart`)         | `addtocart`     |
| Cart Page (`cart`)                     | `cart`          |
| Purchase Complete Page (`purchase`)    | `purchase`      |
| Error Page (`error`)                   | `error`         |
| Add to Registry Page (`addtoregistry`) | `addtoregistry` |
| Generic Page (`generic`)               | `generic`       |
| Wish List Page (`wishlist`)            | `wishlist`      |
