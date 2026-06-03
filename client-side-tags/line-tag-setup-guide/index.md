---
title: LINE Tag Setup Guide
description: This article describes how to set up the LINE tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/line-tag-setup-guide/
---
Boost your business growth by finding the right customers on LINE. Reach more audiences and achieve better results by managing campaign objectives, targeting, budget, and measurement anytime through LINE Ads.

## Tag Tips

* Use data mappings to override Configuration and Standard parameters.
* Supports the following E-Commerce extension values:
  * Type (`type`)
  * Item Ids (`itemIds`)
  * Price (`price`)
  * Currency (`currency`)
  * Order Id (`orderId`)

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Tag ID**: (Required) Your LINE account ID. Your LINE account ID may be set multiple items by concatenating with commas.
* **Customer Type**: The customer type. When set, the customer type is added to the tag custom parameters. When empty, the default value is `lap`.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

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

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/).

| Variable      | Description    |
|:--------------|:---------------|
| Page View     | `PageView`     |
| Category View | `CategoryView` |
| View Product  | `ViewProduct`  |
| Search        | `Search`       |
| Add To Cart   | `AddToCart`    |
| Purchase      | `Purchase`     |
| Custom Event  | `Custom`       |
