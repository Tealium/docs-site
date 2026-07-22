---
title: PayPal Shopping Analytics Tag Setup Guide
description: This article describes how to set up the PayPal Shopping Analytics tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/paypal-shopping-analytics-tag/
---
The SDK collects analytical data from visitors to your website. This data is used by PayPal to provide you an option to re-target visitors who drop off.

## Tag tips

* Use mappings to:   
- Dynamically override config data   
- Dynamically override the E-Commerce extension values   
- Event trigger

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Client ID**: For merchants, this is the production client ID. For partners, this is the partner client ID.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Settings

|Variable| Description|
|---| ---|
|Screen Name (client\_id) (Required)| String|
|User Id (user\_id)| String|
|First Time Visit (first\_time\_visit)| [Boolean]|

### Page View

|Variable| Description|
|---| ---|
|Page Type (page\_type) (Required)| String|
|Page Name (page\_name)| String|
|Page Path (page\_path)| String|
|Page Category Name (page\_category\_name)| String|
|Page Category Id (page\_category\_id)| String|
|Deal Id (deal\_id)| String|
|Deal Name (deal\_name)| String|
|Deal Value (deal\_value)| String|
|Search Results Count (search\_results\_count)| String|

### Product View

|Variable| Description|
|---| ---|
|Product Id (product\_id) | (Required) String (Overrides \_cprod)|
|Product Name (product\_name) | String (Overrides \_cprodname)|
|Product Url (product\_url)| String|
|Product Price (product\_price) | String (Overrides \_cprice)|
|Product Brand (product\_brand) | String (Overrides \_cbrand)|
|Product Category Name (product\_category\_name)| String (Overrides \_ccat)|
|Product Category Id (product\_category\_id)| String |
|Product Discount (product\_discount) | String (Overrides \_cpdisc)|

### Events

|Variable| Description|
|---| ---|
|Page View (page\_view)| page\_view|
|Product View (product\_view)| product\_view|
