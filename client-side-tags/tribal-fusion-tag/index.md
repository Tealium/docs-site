---
title: Tribal Fusion Tag Setup Guide
description: This article describes how to set up the Tribal Fusion Tag tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/tribal-fusion-tag/
---
## Requirements

* Tribal Fusion Account

## Tag configuration 

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Title**: (Required) Enter a descriptive title to identify the Tag instance.
* **Client**: (Required) Enter the numeric client ID provided to you by Tribal Fusion. Example: 746537
* **d**: (Optional) Set this field to the value of the "d" parameter specified in the Tribal Fusion pixel. Note: The default selection is set to "30". If you do not want to send this value, select "N/A".
* **ev**: (Required) Select the value of the 'ev' parameter that Tribal Fusion has specified in its tracking pixel. By default, this is set to "1".
* **Default Page Name**: Enter the default page name that you are tracking with this Tag. Example: "homepage" Note: If you want to override this value, use the mapping toolbox (see [Setting up Mappings](#Setting_up_Mappings)).

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

<blockquote>
Loading this tag on "All Pages" ensures optimal performance of this tag.
</blockquote>


## Data mappings

[Mapping](https://docs.tealium.com/about-data-mappings/) is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor Tag. The Mapping toolbox for this Tag does NOT offer any pre-defined destination variables. However, you can specify custom (more like 'user-defined') variables to function as the Tag's destination.

This tag lets you send the 'Default Page Name' value through a mapping: select the appropriate data source from the drop-down list and enter the destination in the adjacent text field.


<blockquote>
We recommend that you add the [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/) and configure the `_corder` variable. This allows the Extension to map the Order ID value to its corresponding Tag destination.
</blockquote>


## Vendor documentation

* [About Tribal Fusion](http://exponential.com/marketing-services/audience-engagement-solutions/tribal-fusion/)
* [Advertiser FAQs](https://www.tribalfusion.com/SmartAdvertisers/faqs.html)