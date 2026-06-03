---
title: Tribal Fusion Tag Setup Guide
description: This article describes how to set up the Tribal Fusion Tag tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/tribal-fusion-tag/
---
## Requirements

* Tribal Fusion Account

## Tag configuration 

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Title**: (Required) Enter a descriptive title to identify the Tag instance.
* **Client**: (Required) Enter the numeric client ID provided to you by Tribal Fusion. Example: 746537
* **d**: (Optional) Set this field to the value of the &#34;d&#34; parameter specified in the Tribal Fusion pixel. Note: The default selection is set to &#34;30&#34;. If you do not want to send this value, select &#34;N/A&#34;.
* **ev**: (Required) Select the value of the &#39;ev&#39; parameter that Tribal Fusion has specified in its tracking pixel. By default, this is set to &#34;1&#34;.
* **Default Page Name**: Enter the default page name that you are tracking with this Tag. Example: &#34;homepage&#34; Note: If you want to override this value, use the mapping toolbox (see [Setting up Mappings](#Setting_up_Mappings)).

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.
 Loading this tag on &#34;All Pages&#34; ensures optimal performance of this tag. 

## Data mappings

[Mapping]() is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor Tag. The Mapping toolbox for this Tag does NOT offer any pre-defined destination variables. However, you can specify custom (more like &#39;user-defined&#39;) variables to function as the Tag&#39;s destination.

This tag lets you send the &#39;Default Page Name&#39; value through a mapping: select the appropriate data source from the drop-down list and enter the destination in the adjacent text field.

 We recommend that you add the [E-Commerce Extension]() and configure the `_corder` variable. This allows the Extension to map the Order ID value to its corresponding Tag destination. 

## Vendor documentation

* [About Tribal Fusion](http://exponential.com/marketing-services/audience-engagement-solutions/tribal-fusion/)
* [Advertiser FAQs](https://www.tribalfusion.com/SmartAdvertisers/faqs.html)