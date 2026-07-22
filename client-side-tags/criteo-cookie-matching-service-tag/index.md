---
title: Criteo Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the Criteo Cookie Matching Service tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/criteo-cookie-matching-service-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


Criteo Cookie Matching Service enables a buyer to associate the cookie that identifies a Tealium visitor, and the cookie that identifies the user for Criteo.

## Tag Tips

* If left blank, Tealium Account and Profile will be automatically populated.
* Sends the following server-side attribute back to Tealium:
  * `criteo_user_id`

For more information about cookie matching in EventStream, see: [Understanding Persistent Cookie Matching in EventStream](https://docs.tealium.com/about-persistent-cookie-matching/).

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Tealium Account**: (Optional) Your Tealium account.
* **Tealium Profile**: (Optional) Your Tealium profile.
* **Days between syncs**: (Optional) How often to recheck the ID. This value defaults to 7 days.
* **Data Source Key**: (Optional) The data source key from your server-side configuration.
* **Use `/event` endpoint**: Send data to the `/event` endpoint.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|Tealium Account (`tealium_account`)| [String]|
|Tealium Profile (`tealium_profile`)| [String]|
|Days between syncs (`days_between_syncs`)| [Number]|
|Data Source Key (`tealium_datasource`)| [String]|
|Use `/event` endpoint (`use_event_endpoint`)| [Boolean]|
