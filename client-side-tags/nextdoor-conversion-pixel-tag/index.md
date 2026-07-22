---
title: NextDoor Conversion Pixel (Legacy)
description: This article describes how to set up the Nextdoor Conversion Pixel tag.
url: https://docs.tealium.com/client-side-tags/nextdoor-conversion-pixel-tag/
---

<blockquote>
This is the legacy version of the tag. It will soon be deprecated and replaced with the [Nextdoor Universal Pixel tag](https://docs.tealium.com/nextdoor-universal-pixel-tag/).
</blockquote>


Use the Nextdoor Conversion Pixel to accurately measure conversions that can be attributed to your ads on Nextdoor. The Nextdoor Pixel is key to understanding your campaign’s Cost Per Action (CPA). Additionally, it lets you optimize your targeting and creative strategy, which will ultimately lead to a more effective Return on Investment (ROI).

## Tag tips

* Use mappings to override Standard parameters.
* Supported E-Commerce extension parameters.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Pixel ID**: Your NextDoor Pixel ID.
* **Auto Page View**: Automatically create a trigger for page views.
* **Auto Purchase Event**: Automatically create a trigger for purchase events.
* **Generate Event ID**: Automatically generate an event ID for every Nextdoor tracking event.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Configurations

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `pixelId`  | String | NextDoor Pixel ID |
|  `autoPageView`  | Boolean | Auto Page View |
| `autoPurchaseEvent`  | Boolean | Auto Purchase Event  |
| `generate_event_id` | Boolean | Generate event IDs |
| `event_id` | String | Event ID |

### User

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `userEmail`  | String | User Email |
|  `UserEmailHashed`  | String | User Email (Already Hashed) |

### E-Commerce

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `order_id` (Overrides `_corder`)  | String | Order ID |

### Events
To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `PAGE_VIEW`| PageView  |
| `LEAD`| Lead  |
| `PURCHASE`| Purchase  |
| `SIGN_UP`| Sign Up  |
| `ADD_TO_CART` | Add to Cart |
| `INITIATE_CHECKOUT` | Initiate Checkout |
| `SEARCH` | Search |
| `ADD_TO_WISHLIST` | Add to Wishlist |
| `SUBSCRIBE` | Subscribe |
| `VIEW_CONTENT` | View Content |
| `CUSTOM_CONVERSION_1` | Custom Conversion 1 |
| `CUSTOM_CONVERSION_2` | Custom Conversion 2 |
| `CUSTOM_CONVERSION_3` | Custom Conversion 3 |
| `CUSTOM_CONVERSION_4` | Custom Conversion 4 |
| `CUSTOM_CONVERSION_5` | Custom Conversion 5 |
| `CUSTOM_CONVERSION_6` | Custom Conversion 6 |
| `CUSTOM_CONVERSION_7` | Custom Conversion 7 |
| `CUSTOM_CONVERSION_8` | Custom Conversion 8 |
| `CUSTOM_CONVERSION_9` | Custom Conversion 9 |
| `CUSTOM_CONVERSION_10` | Custom Conversion 10 | 

