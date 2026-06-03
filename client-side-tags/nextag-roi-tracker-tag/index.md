---
title: Nextag ROI Tracker Tag Setup Guide
description: This article describes how to configure the Nextag ROI Tracker tag in your iQ Tag Management (TiQ) account.
url: https://docs.tealium.com/client-side-tags/nextag-roi-tracker-tag/
---
## Tag Specifications and Requirements

### Specifications

* **Name**: Nextag ROI Tracker
* **Vendor**: Nextag
* **Type**: Conversion Tracking for [Comparison Shopping Service](http://en.wikipedia.org/wiki/Price_comparison_service)

### Required

**Services**: Nextag Account

**Configuration**:

* Merchant ID

## Tag Configuration in Tealium iQ

### Adding the Tag

Tealium iQ&#39;s Tag marketplace offers a wide variety of tags. Click [here]() to learn how to add a tag to your profile.

### Configuring the Tag

1. **Title**: (Required) Enter a descriptive title to identify the tag instance.
1. **Account ID**: (Optional) Enter the numeric merchant ID provided to you by Nextag. You also have the option to dynamically set this field by mapping to `id` as the destination variable (see [Setting up Mappings](#mappings)). For example, `12345`.

### Applying Load Rules

[Load Rules]() determine when and where to load an instance of this tag. The **Load on All Pages** rule is the default load rule. To load this tag on a specific page, create a new load rule with the relevant conditions.

**Best Practice**: Set up load rule conditions to load this tag on the order confirmation page (Thank You or Receipt) of your site.

### Setting up Mappings

[Mapping]() is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor tag. The Mapping toolbox for this tag does not offer any pre-defined destination variables. However, you can dynamically set the Account ID with a mapping. To do so, select the appropriate data source from the drop-down list and enter `id` in the adjacent text field (see example screenshot below).

 Make certain that the [E-Commerce Extension]() is set up and configured before you configure this tag. The E-Commerce variables this tag uses are `_cprod`, `_corder`, `_ccat`, `_cquan`, and `_ctotal`. 

## Vendor Documentation

* [Nextag Merchant Help Center](http://blog.nextag.com/merchants/)
* [Quick guide to Nextag&#39;s ROI Optimizer](http://blog.nextag.com/merchants/wp-content/uploads/2012/03/ROI_Optimizer.pdf)