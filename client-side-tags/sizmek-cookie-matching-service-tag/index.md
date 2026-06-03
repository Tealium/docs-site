---
title: Sizmek Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the Sizmek Cookie Matching Service tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/sizmek-cookie-matching-service-tag/
---
 When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting]() to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes]() and [Considerations for tealium_visitor_id when upgrading to utag 4.50&#43;](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).

## How it works

Sizmek Cookie Matching Service enables a user to associate the cookie that identifies a Tealium visitor and the cookie that identifies the user for Sizmek.

## Tag Tips

* This tag only fires once per Tealium Visit Session.
* If left blank, Tealium Account and Profile are automatically populated.
* Sends the following server-side attribute back to Tealium:
  * `sizmek_id`

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Sizmek Cookie Matching Service tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Sizmek UUID**
  * (Required) Your unique ID provided by Sizmek.

* **Tealium Account**
  * (Required) Your Tealium account name

* **Tealium Profile**
  * (Required) Your Tealium profile name.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`sizmek_uuid`| Sizmek ID|
|`tealium_account`| Tealium Account name|
|`tealium_profile`| Tealium Profile name|
