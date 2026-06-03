---
title: Adition Cookie Matching Tag Setup Guide
description: This article describes how to set up the Adition Cookie Matching tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/adition-cookie-matching-tag/
---
 When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting]() to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes]() and [Considerations for tealium_visitor_id when upgrading to utag 4.50&#43;](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).

## Tag Tips

* This is the Cookie Matching version of Adition, allowing you to synchronize Visitor ID information between Tealium and Adition.
* This tag is used in conjunction with another Adition tag.
* Sends the following server-side attribute back to Tealium:
  * `adition_user_id`

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Adition Cookie Matching tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Tealium Account**
  * Name of your Tealium account.
  * Required to redirect to the correct vdata endpoint.
  * Defaults to your Tealium iQ account name.

* **Tealium Profile**
  * Name of your Tealium profile.
  * Required to redirect to the correct vdata endpoint.
  * Defaults to your Tealium iQ profile name.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealium Account&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealium Profile&lt;/li&gt;&lt;/ul&gt; |
