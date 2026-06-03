---
title: Snap Pixel Tag Setup Guide
description: This article describes how to set up the Snap Pixel tag.
url: https://docs.tealium.com/client-side-tags/snap-pixel-tag/
---
The Snap Pixel helps advertisers measure the cross-device impact of campaigns. Advertisers will be able to see how many Snapchatters take action on their websites after seeing their ad.

## Tag tips

* Purchase tracking fires automatically when the Order ID is set. To disable automatic purchase tracking, set the destination `auto_purchase_tracking` to `false` with mappings.
* Automatic page view tracking is enabled by default. To disable automatic page view tracking, set `auto_page_tracking` to `false` with mappings.
* Supports the following E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Sub Total (`_csubtotal`)
  * Currency (`_ccurrency`)
  * Customer ID (`_ccustid`)
  * List of Product IDs (`_cprod`)
  * List of Categories (`_ccat`)
  * List of Quantities (`_cquan`)
  * List of Prices (`_cprice`)
* User Email and Phone Number are converted to SHA256 within the Snap Pixel SDK before being passed to Snap&#39;s server.
* To make Snap Pixel Event IDs available as server-side attributes, set **Generate Event ID** to `true` and use the latest version of the Tealium Collect tag.
* The event ID attribute names are in the format `snap_event_id_&lt;Event Name&gt;_&lt;Tag UID&gt;` (for example: `snap_event_id_PageView_512`).

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Pixel ID**: Found in your Snapchat Ads Manager.
* **Generate Event ID**: Automatically generate an Event ID for every Snap tracking event.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Tag Configurations

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `pixel_id`  | String | Pixel ID  |
|  `auto_page_tracking`  | Boolean | Automatic page tracking |
|  `auto_purchase_tracking`  | Boolean | Automatic purchase tracking |
|  `generate_event_id`  | Boolean | Generate event IDs |

### Standard Parameters

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `currency`  | String | Currency | 
|  `description`  | String | Description |
| `item_category` | String | Item category |
| `item_ids` | Array | Item IDs |
| `number_items` | Integer | Number of items |
| `payment_info_available` | Boolean | Payment infofmation available. |
| `price` | Array | Price |
|  `search_string`  | String | Search |
|  `sign_up_method`  | String | Signup method (for example, Facebook, Email, X). |
|  `success` | Boolean | Success |
|  `transaction_id`  | String | Transaction ID |

### E-Commerce

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `order_id` (Overrides `_corder`)  | String | Order ID |
|  `order_subtotal` (Overrides `_csubtotal`)  | String | Subtotal |
|  `order_currency` (Overrides `_ccurrency`)  | String | Currency |
|  `customer_id` (Overrides `_ccustid`)  | String | Customer ID |
|  `product_id` (Overrides `_cprod`)  | Array | List of product IDs |
|  `product_category` (Overrides `_ccat`)  | Array | List of categories |
|  `product_unit_price` (Overrides `_cprice`)  | Array | List of prices |
|  `product_quantity` (Overrides `_cquan`)  | Array | List of 1uantities |

### User Parameters

To allow Snap to match the visitor, we recommend that you include an email or phone number parameter.

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `user_email`  | String | Email address of currently signed in user. |
|  `user_hashed_email`  | String | SHA256 hash of lowercase and whitespace-removed email address. |
|  `user_hashed_phone_number`  | String | SHA256 hash of lowercase and whitespace-removed phone number. |
|  `user_phone_number`  | String | Only digits with country code, area code, and number. No other formatting characters. For example, `12125551212`.|

### Events

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `ACHIEVEMENT_UNLOCKED` | Tack unlocked achievements. |
| `ADD_BILLING` | Track payment information configuration status. |
| `ADD_CART` | Track additions to cart. Required for dynamic ads, and you must include `item_ids` or `item_category` event-specific parameters. |
| `ADD_TO_WISHLIST` | Track additions to wish list.|
| `AD_CLICK` | Track advertisement clicks. |
| `AD_VIEW` | Track advertisement views. |
| `COMPLETE_TUTORIAL` | Track tutorial completions. |
| `INVITE` | Track invitations. |
| `LIST_VIEW` | Track viewing of lists. |
| `LOGIN` | Track logins. |
| `OPEN_APP` | Track opening of application. |
| `PAGE_VIEW` | Track page views. Required for dynamic ads, and you must include `item_ids` or `item_category` event-specific parameters. |
| `PURCHASE` | Track purchases. Required for dynamic ads, and you must include `item_ids` or `item_category` event-specific parameters. |
| `RATE` | Track rates. |
| `RESERVE` | Track reservations. |
| `SAVE` | Track add to wish list events of specific items. |
| `SEARCH` | Track search events. |
| `SHARE` | Track shares. |
| `SIGN_UP` | Track sign up methods (for example, Facebook, Email, X). |
| `SPENT_CREDITS` | Track credits spent. |
| `START_CHECKOUT` | Track checkout events. |
| `START_TRIAL` | Track trial subscriptions started. |
| `SUBSCRIBE` | Track subscriptions. |
| `VIEW_CONTENT` | Track content viewing events. Required for dynamic ads, and you must include `item_ids` or `item_category` event-specific parameters. |
| `CUSTOM_EVENT_1` | CUSTOM_EVENT_1 |
| `CUSTOM_EVENT_2` | CUSTOM_EVENT_2 |
| `CUSTOM_EVENT_3` | CUSTOM_EVENT_3 |
| `CUSTOM_EVENT_4` | CUSTOM_EVENT_4 |
| `CUSTOM_EVENT_5` | CUSTOM_EVENT_5 |
| `Custom` | Custom |

To run dynamic ads, you will need to upload a product catalog or feed, and then connect your Snapchat Pixel. For more information about dynamic ads, see [Snapchat Ads: Dynamic Ads](https://businesshelp.snapchat.com/s/article/pixel-dynamic-best?language=en_US).

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Type | Description |
|:---------|:------------|:------------|
| `currency`| String | ISO 4217 currency code  |
| `description` | String | Description  |
| `item_category` | String | Item category. Category ID must match the `item_group_id` field in the catalog that you upload. For example, `{&#39;item_category&#39;:Shoes&#39;,item_ids&#39;: [&#39;097man&#39;,16span&#39;]});`   |
| `item_ids` | Array | Item IDs. Item IDs must match the `id` field in the catalog that you upload. For example, `{&#39;item_category&#39;:Shoes&#39;,item_ids&#39;: [&#39;097man&#39;,16span&#39;]});`   |
| `number_items` | Number | Number of items   |
| `payment_info_available`| Boolean | Payment information available   |
| `price` | Number | Price of the purchase |
| `search_string` | String | Search string |
| `sign_up_method` | String | Sign up method (for example, Facebook, Email, X).  |
| `success` | Boolean | Success. `1` represents yes, `0` represents no.   |
| `transaction_id` | String | Transaction ID   |
| `custom_parameter`| String | Custom parameter.   |

For more information about each parameter, see [SnapChat Ads: Directly Implement the Pixel On Your Website](https://businesshelp.snapchat.com/s/article/pixel-direct-implementation?language=en_US).

#### Recommended custom parameters

We recommend that you include at least one of the following custom user parameters to improve your matching rates:

* First Name (`firstname`)
* Last Name (`lastname`)
* City (`geo_city`)
* State (`geo_region`)
* Zip Code (`geo_postal_code`)
* Country (`geo_country`)
* Age (`age`)

For more information, see [SnapChat Ads: Directly Implement the Pixel On Your Website](https://businesshelp.snapchat.com/s/article/pixel-direct-implementation?language=en_US).