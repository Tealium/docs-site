---
title: Google Cloud Retail Tag Setup Guide
description: This article describes how to set up the Google Cloud Retail tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/google-cloud-retail-tag/
---
The Google Cloud Retail API is a suite of solutions built to help you implement personalized search and recommendations, based on machine learning models. Implement the Google Cloud Retail tag to record real-time user events. The Google Cloud Retail API uses real-time user events to generate recommendations and search results.

## Tag tips

* Use data mappings to set up event triggers.
* The `tealium_visitor_id` is passed as `visitorId` unless overwritten with a mapping.
* Supports these E-Commerce extension parameters:
    * Sub Total
    * Currency
    * List of Product IDs
    * List of Product Prices
    * List of Product Quantities

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Project Number**: (Required) The Google Cloud Retail project number. 
* **API Key**: (Required) Your Google Cloud Retail API key. 

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable |  Type | Description |
|:---------|:------------|:------------|
| `projectNumber`  | String |Project Number |
| `apiKey`  | String |API Key |
| `locationId`  | String |  Location ID|
| `catalogId`  | String |Catalog ID|
| `cartId`  | String |Cart ID |
| `pageCategories`  | String |Page Categories |
| `searchQuery`  | String |Search Query |
| `completionDetail.completionAttributionToken`  | String |Search Completion Token |
| `completionDetail.selectedSuggestion`  | String |Search Selected Suggestion |
| `completionDetail.selectedPosition`  | String |Search Selected Position |
| `attributionToken`  | String |Attribution Token |
| `debug`  | Boolean |Debug |
| `custom.myvar` | |Custom|

### User Parameters

| Variable |  Type | Description|
|:---------|:------------|:------------|
|`visitorId`  | String | Visitor ID |
|`userInfo.userId`  | String | User ID |

### E-Commerce

| Variable |  Type | Description|
|:---------|:------------|:------------|
|`purchaseTransaction.id` (Overrides `_corder`)  | String | Transaction ID  |
|`purchaseTransaction.revenue` (Overrides `_csubtotal`)  | String | Sub Total |
|`purchaseTransaction.currencyCode` (Overrides `_ccurrency`)  | String | Currency Code |
|`productDetails.product.id` (Overrides `_cprod`)  | Array | List of Product IDs |
|`productDetails.product.priceInfo.price` (Overrides `_cprice`)  | Array | List of Prices |
|`productDetails.product.quantity` (Overrides `_cquan`)  | Array | List of Quantities |

### Attributes

| Variable | Data Type | Description|
|:---------|:------------|:------------|
|`attributes.myvar.text`  | Array | Attribute Text |
|`attributes.myvar.numbers`  | Array | Attribute Numbers |

### Events

To map events, see [Add an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Variable | Description |
|:---------|:------------|
| `add-to-cart`| Add to Cart |
| `category-page-view` | Category Page View | 
| `detail-page-view` | Product Detail Page View  | 
| `home-page-view` | Home Page View | 
| `purchase-complete` | Purchase | 
| `search` |Search | 
| `shopping-cart-page-view` | Shopping Cart View | 

### Event-specific Parameters

To map events, see [Add an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Variable | Type | Description|
|:---------|:------------|:------------|
| `cartId` |  String | Cart ID|
| `pageCategories` |String | Page Categories|
| `searchQuery` |String | Search Query|
| `completionDetail.completionAttributionToken` |String | Search Completion Token  |
| `completionDetail.selectedSuggestion` |String| Search Selected Suggestion  |
| `completionDetail.selectedPosition` |String| Search Selected Position  |
| `attributionToken` |String | Attribution Token |
| `visitorId` |String| Visitor ID  |
| `userInfo.userId` |String| User ID|
| `purchaseTransaction.id` | String | Transaction ID |
| `purchaseTransaction.cost` | String | Cost |
| `purchaseTransaction.tax` | String | Tax |
| `purchaseTransaction.revenue` |String| Sub Total (Overrides `_csubtotal`)  |
| `purchaseTransaction.currencyCode` |String| Currency Code  (Overrides `_ccurrency`) |
| `productDetails.product.id` |Array| List of Product IDs (Overrides `_cprod`) |
| `productDetails.product.priceInfo.price` |Array| List of Prices  (Overrides `_cprice`) |
| `productDetails.quantity` |Array| List of Quantities (Overrides `_cquan`) |
| `attributes.myvar.text` |Array| Attribute Text |
| `attributes.myvar.numbers` |Array| Attribute Numbers |
| `Custom_Parameter` | |Custom Parameter|
| `add-to-cart` | | Add to Cart |
| `category-page-view` | | Category Page View| 
| `detail-page-view`| | Product Detail Page View  | 
| `home-page-view`| |Home Page View | 
| `purchase-complete`| | Purchase  | 
| `search` | | Search  | 
| `shopping-cart-page-view` | |Shopping Cart View  | 

