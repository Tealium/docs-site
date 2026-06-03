---
title: Rubicon Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the Rubicon Cookie Matching Service tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/rubicon-cookie-matching-service-tag/
---
 When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting]() to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes]() and [Considerations for tealium_visitor_id when upgrading to utag 4.50&#43;](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).

## Tag Tips

* Sends the following server-side attribute back to Tealium:
  * `rubicon_vid`

* All parameters can be configured with mappings.
* The GDPR and GDPR Consent variables must be mapped in the European Economic Area (EEA).
* GDPR should be set to `1` when the user is in a EEA country, and `0` otherwise.)
* GDPR Consent is a string containing the Base64 encoded &#34;DaisyBit&#34; consent string.
* See [IAB Europe](https://advertisingconsent.eu/) for additional details on GDPR.

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Rubicon Project Cookie Matching Service tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Tealium Account**
  * Pass-through parameter for the vdata endpoint specifying the account name for EventStream.

* **Tealium Profile**
  * Pass-through parameter for the vdata endpoint specifying the profile name for EventStream.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealium Account&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealium Profile&lt;/li&gt;&lt;/ul&gt; |
|`gdpr`|  &lt;ul&gt;&lt;li&gt;GDPR&lt;/li&gt;&lt;/ul&gt; |
|`gdpr_consent`|  &lt;ul&gt;&lt;li&gt;GDPR Consent&lt;/li&gt;&lt;/ul&gt; |
