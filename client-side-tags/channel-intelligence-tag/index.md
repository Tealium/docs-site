---
title: Channel Intelligence Tag Setup Guide
description: This article describes how to set up the Channel Intelligence tag.
url: https://docs.tealium.com/client-side-tags/channel-intelligence-tag/
---
## Tag Specifications and Requirements

### Specifications

* **Name**: TrueTag
* **Vendor**: Channel Intelligence
* **Type**: Conversion Tracking

### Required

**Services**: Channel Intelligence Account

**Configurations**:

* Vendor ID
* Production Domain

## Tag Configuration in Tealium iQ

### Adding the Tag

Tealium iQ&#39;s Tag marketplace offers a wide variety of Tags. Click [here]() to learn how to add a Tag to your profile.

### Configuring the Tag

1. **Title**: (Required) Enter a descriptive title to identify the Tag instance.
1. **Tag Version**: (Required) Choose the version you want to load for the Tag instance.
  * V1: This will load the Tealium-specific Tag version
  * V2: This will serve external `.js` libraries from `channelinteligence.com`

1. **VID** :(Optional) Enter the numeric vendor ID provided to you by Channel Intelligence. You have the option to set this field dynamically.
1. **Domain**: (Required) Enter the domain name where you want to implement Channel Intelligence. Prefix a period to the domain name. Example: `.yoursite.com`

### Applying Load Rules

[Load Rules]() determine when and where to load an instance of this Tag. The **Load on All Pages** rule is the default Load Rule. To load this tag on a specific page, create a new load rule with the relevant conditions.

**Best Practice**: Leave the default **Load on All Pages** selection as is. This will load the Tag on all pages of your site.

### Setting up Mappings

[Mapping]() is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor Tag.

**Best Practice**: This Tag uses the [E-Commerce Extension]() to send the order information to the tag. Configure the necessary order and product variables in the extension so they can be mapped to their corresponding destinations. Be sure to set up mapping for the below listed variables in the extension:

* `_corder`: The order identifier
* `_cquan`: The list of quantities, with each quantity in the list unique to a product
* `_cprod`: The list of product IDs, with each identifier in the list unique to a product

You can dynamically set the vendor ID by mapping to its destination variable in the **Mapping** toolbox.

## Vendor Documentation

* [TrueTag Tracking Implementation](https://support.google.com/ci-ses/answer/4643079?hl=en)
* [Channel Intelligence FAQs](https://support.google.com/ci-ses/answer/4634733?hl=en)