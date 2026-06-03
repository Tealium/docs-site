---
title: Right Media (Yieldmanager) Tag Setup Guide
description: This article describes how to set up the Right Media (Yieldmanager) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/right-media-yieldmanager-tag/
---
## Specifications

* **Name**: Right Media (Yieldmanager)
* **Vendor**: Yahoo
* **Type**: Advertising

## Required

**Services**: Yahoo Ad Exchange

**Configurations**:

* Pixel ID
* Advertiser ID(s)
* Advertiser Code(s)

## Add the Tag

Tealium iQ&#39;s Tag marketplace offers a wide variety of tags. Click [here]() to learn how to add a tag to your profile.

## Configure the Tag

1. **Title**: (Required) Enter a descriptive title to identify the tag instance.
1. **Tag Type**: (Required) From the drop-down list, choose the type of Yieldmanager pixel you want to implement.
  * Script: This will load the script tag for which the pixel parameter `t` equals `1`.
  * Image: This will load the image tag for which the pixel parameter `t` equals `2`.

1. **ADV**: (Required) Enter the numeric value of the `adv` parameter. This field applies only to the Script Tag. For example, `adv=734359`
1. **IDs**: (Required) Enter the numeric value of the `id` parameter in the pixel. This can be a single ID or a comma-separated list of IDs. For example, `id=342764`
1. **Codes**: (Required) Enter the alphanumeric value of the `code` parameter. This can be a single code or a comma-separated list of codes. For example, `code=bz7rfgm61y397`

## Apply Load Rules

[Load Rules]() determine when and where to load an instance of this tag. The **Load on All Pages** rule is the default load rule. To load this tag on a specific page, create a new load rule with the relevant conditions.

 It is recommended to load this tag on all pages of your site; use the default **Load on All Pages** Rule. 

## Set up Mappings

[Mapping]() is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor tag. The **Mapping** toolbox for this tag does NOT offer any pre-defined destination variables. However, you can provide custom (more like &#39;user-defined&#39;) variables as the tag&#39;s destination. To do so, select the appropriate data source from the drop-down list and enter a custom label in the adjacent text field.

## Vendor Documentation

* [Yieldmanager by Yahoo ad exchange](https://my.yieldmanager.com/) (login required)