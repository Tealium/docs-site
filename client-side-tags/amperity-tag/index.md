---
title: Amperity Tag Setup Guide
description: This article describes how to set up the Amperity tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/amperity-tag/
---
## Tag tips

* Use mapping to override the standard config values dynamically.
* This tag supports the following [E-Commerce extension](https://docs.tealium.com/e-commerce-extension/) parameters:
    * Order ID
    * Product ID

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Write Token**: Non-expiring public write token
* **Stream ID**: Identifies which stream is being written to
* **Tenant Name**: Name of the Amperity tenant being written to
* **Hosted JavaScript Endpoint**: URL that hosts the JavaScript embedded

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `writeToken`  | String | Write Token |
|  `streamID`  | String | Stream ID |
|  `tenantName`  | String | Tenant Name |
|  `hostedJavaScriptEndpoint`  | String | Hosted JavaScript Endpoint |
| `tenantUrl`  | Boolean | Tenant URL  |
|  `is-mobile`  | Boolean | Whether the user accesses the site with a mobile device or a browser. |
|  `session-id`  | String | The ID of the web session in which the event took place. |
|  `property`  | String | For multi-brand or multisite, the specific property. |
| `brand`  | String | For multi-brand, the brand associated with the page. |
|  `page-url`  | String | The URL where the event occurred. |
|  `page-name`  | String | The page name where the event occurred. |
|  `referral-url`  | String | The URL that referred the user to the site. |
|  `referral-source`  | String | The referring medium/source to the site (direct, organic search, etc.). |
|  `search-value`  | String | The entered search value when a site query is run. |

### Identifiers

| Variable | Type | Description |
|:---------|:------------|:------------|
| `first-party-web-id`  | String | The first party customer identifier stored with the session.|
|  `first-party-cookie`  | String | The first party cookie/hashed ID passed from a source. |
|  `visitor-id`  | String | The assigned visitor ID by the provider. This field can be used to store sessions but may not be unique or identifiable. |
|  `device-id`  | String | The device ID associated with the event. This may be hidden depending on the privacy restrictions for the data source. |
|  `mobile-ad-id`  | String | The mobile ad ID or MAID associated with the event. This is an unreliable customer identifier, but is worth capturing. |
|  `captured-email`  | String | The entered email for an order status, restock alert, subscription signup, credit card signup, or loyalty signup. |
|  `identifiers.custom`  | String | Any other capturable customer identifier. |

### Campaign/Ad Info

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `campaign-id`  | String | The referring/tracked campaign ID from an email, digital ad, or other form of campaign. |
|  `campaign-name`  | String | The referring/tracked campaign name from an email, digital ad, or other form of campaign. |
|  `adword-group`  | String | The adword group that referred the user. | 
|  `adword-keyword`  | String | The ad/search keyword list that referred the user. |

### E-Commerce

| Variable | Type | Description |
|:---------|:------------|:------------|
| `order-id` (Overrides `_corder`)  | [Number, String] | Order ID  |
| `product-id` (Overrides `_cprod`)  | Array | Product ID |

### Event Parameters

| Variable | Type |Description |
|:---------|:------------|:------------|
|  `event-datetime`  | DATETIME | The time and day the event occurred | 

### Event Triggers
To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `purchase` | Purchase |
| `productDetailPageBrowse` | Product Detail Page Browse |
| `viewProduct` | View Product |
| `categoryPageBrowse` | Category Page browse |
| `viewCartAbandon` | View Cart Abandon  | 
| `storeLocatorSearch` | Store Locator Search  |
| `highValuePageView` | High-Value Page View |
| `productFilterSelections` | Product Filter selections |
| `accountCreation` | Account Creation |
| `emailListServ` | Email List Serv |
| `promoCodeSignup` | Promo Code Signup |
| `creditCardBrowse` | Credit Card Browse |
| `creditCardSignup` | Credit Card Signup |
| `checkOrderStatus` | Check Order Status |
| `leaveReview` | Leave a Review |
| `siteSearch` | Site Search |
| `supportContact` | Support/Contact |
| `productRestockAlert` | Product Restock Alert |
| `addToWishlist` |  Add to wish list  |

### Event-specific Parameters
To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `purchase` | Purchase |
| `productDetailPageBrowse` | Product Detail Page Browse |
| `viewProduct` | View Product |
| `categoryPageBrowse` | Category Page browse |
| `viewCartAbandon` | View Cart Abandon |
| `storeLocatorSearch` | Store Locator Search |
| `highValuePageView` | High-Value Page View |
| `productFilterSelections` | Product Filter selections |
| `accountCreation` | Account Creation |
| `emailListServ` | Email List Serv |
| `promoCodeSignup` | Promo Code Signup |
| `creditCardBrowse` | Credit Card Browse |
| `creditCardSignup` | Credit Card Signup |
| `checkOrderStatus` | Check Order Status |
| `leaveReview` | Leave a Review |
| `siteSearch` | Site Search | 
| `supportContact` | | Support/Contact |
| `productRestockAlert` | Product Restock Alert |
| `addToWishlist` | Add to wish list |

    