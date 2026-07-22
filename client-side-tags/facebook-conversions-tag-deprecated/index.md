---
title: Facebook Conversions Tag Setup Guide (Deprecated)
description: This article describes how to set up the Facebook Conversions tag.
url: https://docs.tealium.com/client-side-tags/facebook-conversions-tag-deprecated/
---

<blockquote>
This tag is deprecated and no longer available in the tag marketplace. Users can upgrade to the [Facebook Pixel tag](https://docs.tealium.com/facebook-pixel-tag/), which combines Custom Audiences and Conversion Tracking functionality.
</blockquote>


## Specifications and Requirements

### Specifications

* **Name**: Facebook Conversions
* **Vendor**: Facebook
* **Type**: Conversion Tracking

### Required

* Facebook Ads Account
* Configurations
  * Pixel Id
  * Conversion Value
  * Conversion Type (ONLY available to legacy tag)

## Tag Configuration

### Adding the Tag

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

### Configuring the Tag

1. **Title**: Enter a descriptive title to identify the tag instance.
1. **Pixel ID**: Enter the numeric ID of the conversion pixel, which is a code snippet that you place on the conversion page of your site.  
If you prefer to dynamically set this parameter or otherwise override any existing ID, map to `pixel_id` in the Mapping Toolbox.
1. **Conversion Type**: This is deprecated in the recent tag template. Do not make a selection from the drop-down list.
1. **Conversion Value**: Enter the value of the conversion type in your account currency.  

<blockquote>
If you want to configure the Conversion Value dynamically or override its existing value, map to `value` in the Mapping toolbox.
</blockquote>


### Applying Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag. The **Display on All Pages** rule is the default load rule. To load this tag on a specific page, create a new load rule with the relevant conditions.

We recommend that you load this tag on the page where the conversion event happens. For instance, load this tag only on the checkout page if you want to track checkout events.

#### Setting up Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).


<blockquote>
We recommend setting up the [E-Commerce data layer](https://docs.tealium.com/e-commerce-extension/) for this tag so the value in `_csubtotal` can be automatically sent to matching tag destination.
</blockquote>


* **Pixel ID** (`pixel_id`)  
The numeric identifier of your conversion pixel.  
Mapping a data source to this destination will dynamically set this parameter and override the numeric id you provided in the tag configuration.
* **Conversion Value** (`value`)  
The value of the conversion event you are tracking.  
Mapping a data source to this destination will dynamically set this parameter and override the conversion value you provided in the tag configuration.
* **Currency** (`currency`)  
The currency in which the transaction was completed.  
Mapping a data source to this destination will send the currency information.
* **Subtotal** (`order_subtotal`)  
The subtotal value of the final order.  
Mapping a data source to this destination will override the `_csubtotal` variable in the E-Commerce data layer, if configured.

## Additional Information

* What is [conversion tracking](https://www.facebook.com/help/460491677335370)?
* How do I use [conversion pixels](https://www.facebook.com/help/www/373979379354234?rdrhc)?
* What is the value field in a [conversion pixel](https://www.facebook.com/help/464828030234857)?
