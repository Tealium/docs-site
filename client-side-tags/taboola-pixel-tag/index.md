---
title: Taboola Pixel Tag Setup Guide
description: This article describes how to set up the Taboola Pixel tag.
url: https://docs.tealium.com/client-side-tags/taboola-pixel-tag/
---
## Tag Tips

* This tag uses event triggers and parameters to send data.
* When you use multiple Taboola IDs, identical data is sent to each ID.
* Use mappings to override or set parameter values and send custom data.
* Check with Taboola Support before adding custom variables.

## Tag Configuration

First, go to Tealium's tag marketplace and add the Taboola Pixel tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Taboola ID(s)**: This is a numeric value. Separate multiple IDs by commas.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

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

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

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

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

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
