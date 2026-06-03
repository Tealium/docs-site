---
title: X Plus One Tag Setup Guide
description: This article describes how to set up the X Plus One tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/x-plus-one-tag/
---
## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Title**: (Required) Enter a descriptive title to identify the tag instance.
* **Tag Type**: (Required) You must choose the type of tag you want to load for the tag instance. From the drop-down list, select between &#34;script&#34; and iframe&#34; type.  
**Note**: The domain information in the code snippet is an indicator of the tag type: &#34;s.xp1&#34; is the Script type whereas &#34;d.xp1&#34; is the iframe type.
* **Account**: (Required) Enter the account information provided to you by [x&#43;1]. The account is the value of the &#34;\_o&#34; parameter in the code snippet.
* **Placement**: (Required) Enter the alphanumeric placement value in this field. If you want to populate this value dynamically, use the tag&#39;s [mapping toolbox](#mappings) instead. If you intend to dynamically set this value through mapping, you must still provide a default Placement value under the Vendor Configurations.  For example: pt-1234-001

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

## Data mappings

[Mapping]() is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor tag. The destination variables for this tag are available in the Mapping toolbox.

* **placement (\_t)**: Destination variable for the tag&#39;s Placement parameter.  
 Mapping to this destination will dynamically set the placement value.
* **ssv\_TRT1** through **ssv\_TRT15**: Set of 15 destinations for custom mappings.  
 Map to these destination if you want to send custom values to the tag.