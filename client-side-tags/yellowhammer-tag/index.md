---
title: YellowHammer Tag Setup Guide
description: This article describes how to configure YellowHammer in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/yellowhammer-tag/
---YellowHammer Media Group is an ad-serving service provider that focuses on high-impact online display performance solutions for the entire Direct Response spectrum—including brands and agencies.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* Path (tr): Path is part of the image pixel just after jump.omnitarget.com. For example, `tr123456` in <http://jump.omnitarget.com/tr123456>?.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.


## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The destination variables for the YellowHammer (Omnitarget) tag are built into its **Data Mapping** tab. Available categories are:

### Standard

|**Destination Name**| **Description**|
|---| ---|
|Path (tr)| Use this to override the configuration value.|
|SSP Data (sspdata)| Map a cookie whose value you set on the landing page.|

### E-Commerce

Since the YellowHammer (Omnitarget) tag is e-commerce enabled, it will automatically use the default E-Commerce Extension mappings. Manually mapping in this category is generally not needed unless:

* You want to override any extension mappings.
* an e-commerce variable you want is not offered in the extension.

|**Destination Name**| **Description**|
|---| ---|
|Order ID (order\_id)| Use this to override the default e-commerce value `_corder`.|
|Subtotal/Sale Amount (order\_subtotal)| Use this to override the default e-commerce value `_csubtotal`.|
|Customer ID (customer\_id)| Use this to override the default e-commerce value `_ccustid`.|
