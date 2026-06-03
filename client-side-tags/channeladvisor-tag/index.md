---
title: ChannelAdvisor Tag Setup Guide
description: This article describes how to set up the ChannelAdvisor tag.
url: https://docs.tealium.com/client-side-tags/channeladvisor-tag/
---
## Tag Specifications and Requirements

### Specifications

* **Name**: ChannelAdvisor
* **Vendor**: ChannelAdvisor
* **Type**: Conversion Tracking

### Required

**Services**: ChannelAdvisor Platform

**Configurations**:

* ChannelAdvisor Account ID

## Tag Configuration in Tealium iQ

### Adding the Tag

Tealium iQ&#39;s Tag marketplace offers a wide variety of tags. Click [here]() to learn how to add a tag to your profile.

### Configuring the Tag

1. **Title**: (Required) Enter a descriptive title to identify the Tag instance.
1. **Account ID**: (Optional) Enter the numeric ID associated with your ChannelAdvisor Account. For example: `10055350`   

You can choose to dynamically populate the Account ID (also called Profile ID) field by mapping to the `pid` parameter.


### Applying Load Rules

[Load Rules]() determine when and where to load an instance of this tag. The **Load on All Pages** rule is the default Load Rule. To load this Tag on a specific page, create a new load rule with the relevant conditions.

**Best practice**: Set up load rule conditions to load this tag on the order confirmation page of your site. This will allow the tag to capture the order information following a conversion.

### Setting up Mappings

[Mapping]() is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor tag. The destination variables for this tag are available in the Mapping toolbox.

* **pid**: Map to this variable to dynamically set the numeric ID of your ChannelAdvisor account.

**Note**: Make certain that the [E-Commerce Extension]() is configured to automatically map the order and product variables. However, you can override the E-Commerce Extension mappings with their corresponding destination variables listed in the toolkit.

* **orderId**: The Extension&#39;s `_corder` variable maps to this destination. This data point indicates the order identifier.
* **revenue**: The Extension&#39;s `_csubtotal` variable maps to this destination. This data point identifies the order subtotal.
* **currency**: The Extension&#39;s `_ccurrency` variable maps to this destination. This data point identifies the currency code.
* **sku**: The Extension&#39;s `_cprod` variable (List of product IDs) maps to this destination. This data point identifies the list of product SKUs, with each SKU unique to a line item in the order.
* **price**: The Extension&#39;s `_cprice` variable maps to this destination. This data point identifies the list of unit prices associated with the items in the order.
* **quan**: The Extension&#39;s `_cquan` variable maps to this destination. This data point identifies the list of quantities for each item in the order.

## Vendor Documentation

* [How to implement the Order Tracking Pixel](http://ssc.channeladvisor.com/howto/my-account/account-settings/tracking-pixel#Order)
* [How to implement the Tracking pixel with Tealium](http://ssc.channeladvisor.com/howto/implementing-tracking-pixels-tealium)
* [About Channel Advisor Platform](http://ssc.channeladvisor.com/howto)
* [ChannelAdvisor Strategy and Support Center](http://ssc.channeladvisor.com/)
