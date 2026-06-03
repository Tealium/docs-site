---
title: Flashtalking Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the Flashtalking Cookie Matching Service tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/flashtalking-cookie-matching-service-tag/
---
 When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting]() to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes]() and [Considerations for tealium_visitor_id when upgrading to utag 4.50&#43;](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).

## Tag tips

* Use mappings to override standard config values.
* Custom mappings will be included in the cookie sync request to Tealium.
* This tag will only execute once per session, using the `utag_main_flashtalking_cms_&lt;tag UID&gt;` cookie to control that execution.
* Sends the following server-side attribute back to Tealium:
  * `flashtalking_id`

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Flashtalking Key**
  * Your Flashtalking Key.
* **Tealium Account**:
  * Optional
  * Override the `tealium_account` used for server-side requests.
* **Tealium Profile**:
  * Optional
  * Override the `tealium_profile` used for server-side requests.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`key`|  &lt;ul&gt;&lt;li&gt;Flashtalking Key&lt;/li&gt;&lt;/ul&gt; |
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealium Account&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealium Profile&lt;/li&gt;&lt;/ul&gt; |
|`tealium_event`|  &lt;ul&gt;&lt;li&gt;Tealium Event&lt;/li&gt;&lt;/ul&gt; |
