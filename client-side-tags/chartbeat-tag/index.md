---
title: Chartbeat Tag Setup Guide
description: This article describes how to set up the Chartbeat tag.
url: https://docs.tealium.com/client-side-tags/chartbeat-tag/
---
## Tag Specifications and Requirements

### Specifications

* **Name**: Chartbeat
* **Vendor**: Chartbeat
* **Type**: Real-time Web Analytics

### Required

**Services**: Chartbeat Account

**Configurations**:

* Chartbeat User ID

## Tag Configuration in Tealium iQ

### Adding the Tag

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

### Configuring the Tag

1. **Title**: (Required) Enter a descriptive title to identify the tag instance.
1. **User ID**: (Required) Enter the numeric user ID provided to you by Chartbeat. This can be found in your Chartbeat account. For example, `1234`
1. **Domain**: (Required) Enter the domain name where you want to implement Chartbeat. Do not include the prefix `www`. For example, `yoursite.com`
1. **Use Canonical**: (Optional) Choose whether or not you want Chartbeat to use the [Canonical](https://support.google.com/webmasters/answer/139066?rd=1) path (the preferred URL) to access a page. By default, the Use Canonical drop-down is set to false, in which case Chartbeat will use the page's actual URL.  
  * Select `true` if you want Chartbeat to use the canonical path you have defined using a link element in your site's HTML.

For example, assume a page can be accessed by two different URLs:

```
http://yoursite.com/products?category=apparel&kids
http://yoursite.com/apparel/kids
```

But only URL #2 is set as canonical. By enabling the **Use Canonical** field, Chartbeat can use your preferred URL#2 for tracking purpose.  


<blockquote>
You have the option to override this selection by mapping to the `path` variable.
</blockquote>


You may use the Data Mapping toolbox to override or dynamically set the tag settings for #2 through #4.

### Applying Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag. The **Load on All Pages** rule is the default Load Rule. To load this tag on a specific page, create a new load rule with the relevant conditions.


<blockquote>
Leave the default **Load on All pages** rule as is. Chartbeat, like most analytics Tags, is recommended to load on all pages of the site to ensure accurate data collection.
</blockquote>


### Setting up Mappings

[Mapping](https://docs.tealium.com/about-data-mappings/) is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor tag. The destination variables for this tag are available in the Mapping toolkit.

* **User ID:** Map to this destination to send the numeric user ID, one that Chartbeat has provided you.
* **Domain**: Map to this destination to send the domain name where Chartbeat is implemented.
* **Use Canonical (canonical)**: Map to this destination to indicate whether or not the page's url is [Canonical](https://support.google.com/webmasters/answer/139066?rd=1). Make sure the value in the data source is either `true` or `false`.
* **title**: Map to this destination to send the page's current title.
* **path**: Map to this variable to send the page's path.
* **sections**: Map to this variable to send section information that contains the content you want Chartbeat to track. Multiple sections must be sent as a comma-separated list of values.
* **authors**: Map to this variable to send information about the content's author. Multiple authors must be sent as a comma-separated list of values.

## Vendor Documentation

* [About Chartbeat Publishing for Editorial](http://support.chartbeat.com/?b_id=195)
* [Chartbeat Implementation Docs](https://chartbeat.com/docs/)
* [Chartbeat Configuration Variables](https://chartbeat.com/docs/configuration_variables/)
* [Troubleshooting/FAQs](https://chartbeat.com/docs/troubleshooting/)
