---
title: PriceGrabber Tag Setup Guide
description: This article describes how to configure the PriceGrabber tag.
url: https://docs.tealium.com/client-side-tags/pricegrabber-tag/
---
## Specifications

* **Name**: PriceGrabber
* **Vendor**: PriceGrabber
* **Type**: Conversion Tracking

## Required

**Services**: PriceGrabber Merchant Account

**Configurations**:

* Retailer ID
* Conversion Tracking Code (CTS)
* Merchant Survey Code
* Popup Position values (X and Y)

## Add the Tag

Tealium iQ&#39;s Tag marketplace offers a wide variety of tags. Click [here]() to learn how to add a tag to your profile.

## Configure the Tag

1. **Title**: (Required) Enter a descriptive title to identify the tag instance.
1. **Retailer ID**: (Required) Enter the numeric retailer id, which is the value of the `retid` parameter of your PriceGrabber code. For example, `12345`
1. **Tag**: (Required) From the drop-down list, choose the tag type you want to load.
  * `conversion.php`: This will load PriceGrabber&#39;s conversion tracking code.
  * `rating_merchrevpopjs.php`: This will load PriceGrabber&#39;s merchant survey code.

1. **Position X**: (Optional) Enter the value of the `popup_pos_x parameter` to specify where the merchant survey will popup in relation to the position X on a page. This value is specified in PriceGrabber&#39;s merchant survey code and is only applicable to the `rating_merchrevpopjs.php` tag type. For example, `popup_pos_x=200`;
1. **Position Y**: (Optional) Enter the value of the `popup_pos_y parameter` to specify where the merchant survey will popup in relation to the position Y on a page. This value is specified in PriceGrabber&#39;s merchant survey code and is only applicable to the `rating_merchrevpopjs.php` tag type. For example, `popup_pos_x=20`;

**Note**: For the merchant survey to popup in the center of the page, leave the Position X and Position Y fields blank.

## Apply Load Rules

[Load Rules]() determine when and where to load an instance of this tag. The **Load on All Pages** rule is the default load rule. To load this tag on a specific page, create a new load rule with the relevant conditions.

### Best Practices

* The `conversion.php` should be placed on the checkout page so the tag can grab any data specific to the order.
* The `rating_merchrevpopjs.php` tag must be placed on the confirmation page, one that appears post completion of an order.

### Set up Mappings

[Mapping]() is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor tag. The destination variables for this tag are available in the Mapping toolbox.

 We recommend that you add the [E-Commerce Extension]() and configure the Order and Product variables applicable to the conversion: `_cbrand`, `_cprod`, `_cprice`, `_csku`, and `_cquan`. This allows the Extension to map their values to the corresponding destinations supported by this tag. 

For the `conversion.php` tag type, map to these destinations:

* **retid**: The retailer ID specified in the PriceGrabber conversion code
* **Manufacturer [Array]**: The list of product manufacturers  
 Mapping to this destination overrides the Extension&#39;s `_cbrand` variable.
* **Manufacturer Part Number [Array]**: The list of product identifiers  
 Mapping to this destination overrides the Extension&#39;s `_cprod` variable.
* **Retailer Price [Array]**: The list of product prices  
 Mapping to this destination overrides the Extension&#39;s `_cprice` variable.
* **Internal Merchant SKU [Array]**: The list of product SKUs  
 Mapping to this destination overrides the Extension&#39;s `_csku` variable.
* **UPC [Array]**: The list of Universal Product Codes for the products
* **Quantity [Array]**: The list of quantities for the products in the order  
 Mapping to this destination overrides the Extension&#39;s `_cquan` variable.

For the `rating_merchrevpopjs.php` tag type, map to this destination:

* `popup_email`: The email address provided by the customer

## Vendor Documentation

* [PriceGrabber Merchant Resources](https://partner.pricegrabber.com/mss_main.php?ccode=us) (login required)
* [PriceGrabber Data Feed Requirements](https://partner.pricegrabber.com/mss_main.php?sec=2&amp;ccode=us)