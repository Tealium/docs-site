---
title: Marin Software Tag Setup Guide
description: This article describes how to set up the Marin Software tag.
url: https://docs.tealium.com/client-side-tags/marin-software-tag/
---
## Tag Specifications and Requirements

### Specifications

**Name**: Marin Software

**Vendor**: Marin Software

**Type**: Search

### Required

**Services**: Marin Software Account

**Configurations**:

* Client ID

## Tag Configuration in Tealium iQ

### 1. Adding the Tag

Tealium iQ&#39;s Tag marketplace offers a wide variety of tags. Click [here]() to learn how to add a Tag to your profile.

### 2. Configuring the Tag

1. **Title**: (Required) Enter a descriptive title to identify the tag instance.
1. **Client ID**: (Required) Enter the client ID assigned to you by Marin Software.

### 3. Applying Load Rules

[Load Rules]() determine when and where to load an instance of this tag. The **Load on All Pages** rule is the default Load Rule. To load this tag on a specific page, create a new load rule with the relevant conditions.

**Best Practice**: Create a load rule to load this tag on order confirmation pages only. Moreover, make certain you only load 1 instance of this tag on the order confirmation page. Loading multiple instances on the same page will cause the Marin Software tag to fail.

### 4. Setting up Mappings

[Mapping](/iq-tag-management/data-mappings/manage/) is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor tag.

This tag requires that you add and configure the [E-Commerce extension](). The following data points are automatically sent to Marin by the E-Commerce extension. Mapping to these destinations in the Mappings Toolbox overrides the E-Commmerce mappings, where applicable.

* **convType**
The E-Commerce extension&#39;s `_ctype` variable maps to this destination. This data point identifies the cart or order type.

* **orderid**
The E-Commerce extension&#39;s `_corder` variable maps to this destination. This data point identifies the ID of the order.

* **category**
The E-Commerce extension&#39;s `_ccat` variable maps to this destination. This data point identifies the product&#39;s category.

* **currency**
The E-Commerce extension&#39;s `_ccurrency` variable maps to this destination. This data point identifies the order&#39;s currency type.

* **product**
The E-Commerce extension&#39;s `_cprod` variable maps to this destination. This variable does not show up in the Mappings Toolbox as a destination. To map to this, you must manually enter `product` into the mapping field. This is the list of products ordered.

* **quantity**
The E-Commerce extension&#39;s `_cquan` variable maps to this destination. This variable does not show up in the Mappings Toolbox as a destination. To map to this, you must manually enter `quantity` into the mapping field. This is the quantities of products ordered.

* **price**
The E-Commerce extension&#39;s `_cprice` variable maps to this destination. This variable does not show up in the Mappings Toolbox as a destination. To map to this, you must manually enter `price` into the mapping field. This is the list of product prices.

#### Deprecated Mappings

* **Affiliation**
This destination is deprecated in the most recent Marin Software tag template. Mapping to this destination does nothing.

#### Vendor Documentation

* [Marin Software](http://www.marinsoftware.com/)
