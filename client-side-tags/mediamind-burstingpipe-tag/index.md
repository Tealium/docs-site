---
title: MediaMind (BurstingPipe) Tag Setup Guide
description: This article describes how to set up the MediaMind (BurstingPipe) tag.
url: https://docs.tealium.com/client-side-tags/mediamind-burstingpipe-tag/
---
## Tag Specifications and Requirements

### Specifications

**Name**: MediaMind (BurstingPipe)

**Vendor**: Sizmek

**Type**: Display Ad

### Required

**Services**: Activity or Advertiser ID

**Configurations**:

* Activity/Advertiser ID

Tealium only supports the iframe version of this Tag. Keep in mind that since this Tag loads an iframe, you may load other scripts or Tags within that iframe that are not immediately apparent.

## Tag Configuration in Tealium iQ

### 1. Adding the Tag

Tealium iQ&#39;s Tag marketplace offers a wide variety of tags. Click [here]() to learn how to add a Tag to your profile.

### 2. Configuring the Tag

![](/images/client-side-tags/no-title-1681i26b1bf0ea1667891.png)

1. **Title**: (Required) Enter a descriptive title to identify the tag instance.
1. **Activity ID**: (Required) Enter the client ID assigned to you by MediaMind/Sizmek. If you select the **Remarketing Tag** option below, this is where you enter the Advertiser ID. If you plan to dynamically set this with mapping, leave this field blank.
1. **Tag Type**: (Required) Select the type of MediaMind/Sizmek tag you want to use. If you&#39;re not sure, select `Conversion Tag`.
  * **Conversion Tag** - Select this option if you want to use the Conversion version of this tag.
  * **Remarketing Tag** - Select this option if you want to use the Remarketing version of this tag.

### 3. Applying Load Rules

[Load Rules]() determine when and where to load an instance of this Tag. The **Load on All Pages** rule is the default Load Rule. To load this Tag on a specific page, create a new load rule with the relevant conditions.

**Best Practice**: If you&#39;re using the Conversion Tag version, create load rules so this Tag only loads on page in which conversions occur.

### 4. Setting up Mappings

[Mapping]() is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor Tag.

For this Tag, we recommend that you add and configure the [E-Commerce extension](). To override any of the E-Commerce mappings, manually map the data sources to their destinations where applicable.

## Conversion Tag

* **Activity ID (ActivityID)**
Map the data source that identifies the Activity ID to dynamically set it for this Tag.

* **Session ID (Session)**
Map the data source that identifies the session ID to this destination.

* **Revenue (Value)**
The E-Commerce extension&#39;s `_csubtotal` variable maps to this destination.

* **Order ID (OrderID)**
The E-Commerce extension&#39;s `_corder` variable maps to this destination.

* **Product ID (ProductID)**
The E-Commerce extension&#39;s `_cprod` variable maps to this destination.

* **Product Info (ProductInfo)**
Map the data source that contains the product information to this destination.

* **Quantity (Quantity)**
The E-Commerce extension&#39;s `_cquan` variable maps to this destination.

## Retargeting Tag

* **Advertiser ID**
Map the data source that contains the Advertising ID to this destination.

* **V1 (TKV!)**
* **Tag ID (TID)**
* **Dynamic Tag ID (TVAL)**

### Deprecated &amp; Unsupported Mappings

* **V2 (TKV2)**
This mapping is not supported in the latest MediaMind (BurstingPipe) Tag template. Mapping to this destination does nothing.

## Vendor Documentation

* [Sizmek MDX Login](https://platform.mediamind.com/Eyeblaster.ACM.Web/Login/Login.aspx)
