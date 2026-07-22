---
title: X Plus One Tag Setup Guide
description: This article describes how to set up the X Plus One tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/x-plus-one-tag/
---
## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Title**: (Required) Enter a descriptive title to identify the tag instance.
* **Tag Type**: (Required) You must choose the type of tag you want to load for the tag instance. From the drop-down list, select between "script" and iframe" type.  
**Note**: The domain information in the code snippet is an indicator of the tag type: "s.xp1" is the Script type whereas "d.xp1" is the iframe type.
* **Account**: (Required) Enter the account information provided to you by [x+1]. The account is the value of the "\_o" parameter in the code snippet.
* **Placement**: (Required) Enter the alphanumeric placement value in this field. If you want to populate this value dynamically, use the tag's [mapping toolbox](#mappings) instead. If you intend to dynamically set this value through mapping, you must still provide a default Placement value under the Vendor Configurations.  For example: pt-1234-001

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

[Mapping](https://docs.tealium.com/about-data-mappings/) is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor tag. The destination variables for this tag are available in the Mapping toolbox.

* **placement (\_t)**: Destination variable for the tag's Placement parameter.  
 Mapping to this destination will dynamically set the placement value.
* **ssv\_TRT1** through **ssv\_TRT15**: Set of 15 destinations for custom mappings.  
 Map to these destination if you want to send custom values to the tag.