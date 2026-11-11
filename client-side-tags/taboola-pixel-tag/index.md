---
title: Taboola Pixel Tag Setup Guide
description: This article describes how to set up the Taboola Pixel tag.
url: https://docs.tealium.com/client-side-tags/taboola-pixel-tag/
---
## Tag tips

* This tag uses event triggers and parameters to send data.
* When you use multiple Taboola IDs, identical data is sent to each ID.
* Use mappings to override or set parameter values and send custom data.
* Check with Taboola Support before adding custom variables.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Taboola ID(s)**: This is a numeric value. Separate multiple IDs by commas.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`client_name`|  Taboola ID. |
|`orderid`|  Order ID, overrides `_corder`. |
|`revenue`|  Order total, overrides `_ctotal`. |
|`currency`|  Currency, overrides `_ccurrency`. |
|`quantity`|  Quantity. |
| `item-url` |  Page URL, overrides `document.location.href`. |

### Events

|Variable| Description|
|---| ---|
|`page_view`|  Pageview. |
|`view_content`|  View Content. |
|`lead`|  Lead. |
|`complete_registration`|  Complete Registration. |
|`make_purchase`|  Purchase. |
|`search`|  Search. |
|`add_to_cart`|  Add to Cart. |
|`add_to_wishlist`|  Add to wish list. |
|`start_checkout`|  Start Checkout. |
|`add_payment_info`|  Add Payment Info. |
|`app_install`|  App Install. |
|`custom`|  Custom. |

### Event Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/tag-management/data-mappings/manage/#add-an-event-mapping)

|Variable| Description|
|---| ---|
|`orderid`|  Order ID. |
|`revenue`|  Order total. |
|`currency`|  Currency. |
|`quantity`|  Quantity. |
|`custom`|  Custom. |

### E-commerce Events

|Variable| Description|
|---| ---|
| `HOME_PAGE_VISIT` | Home Page Visit.| 
| `CATEGORY_VIEW` | Category View. | 
| `PRODUCT_VIEW` | Product View. | 
| `ADD_TO_CART` | Add to Cart. | 
| `REMOVE_FROM_CART` | Remove from Cart. | 
| `CHECKOUT` | Checkout. | 
| `PURCHASE` | Purchase. | 
| `SEARCH` | Search. | 
| `ADD_TO_WISH_LIST` | Add to wish list. | 
| `REMOVE_FROM_WISH_LIST` | Remove from wish list. |

### E-commerce Event Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/tag-management/data-mappings/manage/#add-an-event-mapping)

| Event | Description |
|:------|:------------|
| `productIds` | Product ID. |
| `category` | Category. |
| `categoryId` | Category ID. |
| `searchTerm` | Search term. |
| `orderId` | Order ID. |
| `value` | Value. |
| `currency` | Currency. |
| `cartDetails.productId` | Cart products. |
| `cartDetails.quantity` | Cart quantities. |
| `cartDetails.price` | Cart prices. |
