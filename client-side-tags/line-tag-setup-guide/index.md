---
title: LINE Tag Setup Guide
description: This article describes how to set up the LINE tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/line-tag-setup-guide/
---
Boost your business growth by finding the right customers on LINE. Reach more audiences and achieve better results by managing campaign objectives, targeting, budget, and measurement anytime through LINE Ads.

## Tag tips

* Use data mappings to override Configuration and Standard parameters.
* Supports the following E-Commerce extension values:
  * Type (`type`)
  * Item Ids (`itemIds`)
  * Price (`price`)
  * Currency (`currency`)
  * Order Id (`orderId`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Tag ID**: (Required) Your LINE account ID. Your LINE account ID may be set multiple items by concatenating with commas.
* **Customer Type**: The customer type. When set, the customer type is added to the tag custom parameters. When empty, the default value is `lap`.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Configuration parameters

| Variable                       | Description |
|:-------------------------------|:------------|
| Tag ID (`tagId`)               | [String]    |
| Customer Type (`customerType`) | [String]    |

### Standard parameters

| Variable                                           | Description |
|:---------------------------------------------------|:------------|
| Type (`type`) (Overrides `_ctype`)                 | [String]    |
| Item Ids (`itemIds`) (Overrides `_cprod`)          | [Array]     |
| Category (`category`)                              | [String]    |
| Keywords (`keywords`)                              | [String]    |
| Price (`price`) (Overrides `_csubtotal`)           | [String]    |
| Currency (`currency`) (Overrides `order_currency`) | [String]    |
| Order Id (`orderId`) (Overrides `_corder`)         | [String]    |
| Start Date (`startDate`)                           | [String]    |
| End Date (`endDate`)                               | [String]    |

### Events

Enter the value of the mapped variable needed to trigger the selected Event. If you select **CustomEvent**, enter a name for the event in the **Custom event name** field. After you configure the **CustomEvent** mapping and events are sent to LINE, you can select the specified **CustomEvent** name when creating custom audiences in the LINE Ads Platform Account.

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/tag-management/data-mappings/manage/).

| Variable      | Description    |
|:--------------|:---------------|
| Page View     | `PageView`     |
| Category View | `CategoryView` |
| View Product  | `ViewProduct`  |
| Search        | `Search`       |
| Add To Cart   | `AddToCart`    |
| Purchase      | `Purchase`     |
| Custom Event  | `Custom`       |
