---
title: adMarketplace Tag Setup Guide
description: This article describes how to set up the adMarketplace tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/admarketplace-tag/
---
## Tag Specifications and Requirements

### Specifications

* **Name**: adMarketplace
* **Vendor**: adMarketplace
* **Type**: Search Network Advertising

### Required

**Services**: adMarketplace Dashboard

**Configurations**:

* Partner ID
* Customer ID
* Event ID

## Tag Configuration in Tealium iQ

### Adding the Tag

Tealium iQ's Tag marketplace offers a wide variety of Tags. Click [here](https://docs.tealium.com/manage-tags/) to learn how to add a Tag to your profile.

### Configuring the Tag

1. **Title**: (Required) Enter a descriptive title to identify the Tag instance.
1. **Partner ID**: (Required) Enter the numeric Partner ID provided to you by adMarketplace. For example: `3749`
1. **Customer ID**: (Required) Enter the customer's numeric identifier. For example: `15294`
1. **Event ID**: (Required) Enter the numeric value that identifies the conversion event being tracked.
1. **Custom Info**: (Optional) Enter additional information pertinent to the order.

**Note**: You have the option to dynamically set the values for Partner ID, Customer ID, Event ID, and Custom Info through the Mapping toolbox.

### Applying Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this Tag. The **Load on All Pages** rule is the default Load Rule. To load this Tag on a specific page, create a new load rule with the relevant conditions.

**Best Practice**: To capture necessary order details post conversion, load this Tag on the order confirmation pages of your site.

### Setting up Mappings

[Mapping](https://docs.tealium.com/about-data-mappings/) is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor Tag. The destination variables for this Tag are available in the Mapping toolbox.

**Note**: We recommend adding the [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/) and configuring the `_corder` and `_csubtotal` values. By doing so, the Extension can automatically send their values to the corresponding destinations. However, you can override the Extension's values by mapping to the Tag's destination(s) listed in the Mapping toolbox.

* **pid**: The partner id assigned to you by adMarketplace
* **cid**: The customer's unique identifier
* **eventid**: A numeric value assigned to the conversion event
* **orderval**: The amount value before shipping and tax  
 Map to this destination if you prefer to override the Extension's `_csubtotal` variable.
* **orderid**: The value that uniquely identifies the order  
 Map to this destination if you prefer to override the Extension's `_corder` variable.
* **custominfo**: Additional information pertinent to the order

### Vendor Documentation

* [About adMarketplace](http://www.admarketplace.com/who-we-are.php)
* [adMarketplace Blog](http://blog.admarketplace.com/)
