---
title: Google Cookie Matching Service for Google Ad Manager and DV360 (Google-hosted) Tag Setup Guide
description: This article describes how to set up the Google Cookie Matching Service for Google Ad Manager and DV360 (Google-hosted) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/google-cookie-matching-admgr-dv360/
---
 When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting]() to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes]() and [Considerations for tealium_visitor_id when upgrading to utag 4.50&#43;](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).

Google&#39;s Cookie Matching Service enables a buyer to associate a first-party cookie that identifies a visitor, and the doubleclick.net cookie that identifies the user for Google. This Google-hosted match tag sends the Tealium Visitor ID, or a client-specified identifier, to Google for matching. This identifier can then be used in the Ad Manager and DV360 connectors.

## Tag tips

* To access cookie hosted matching, you must contact your Google Account Manager to configure your account.
* `tealium_visitor_id` (md5 hashed) is automatically sent to Google for hosted matching as `google_hm` unless overridden with mapping (both will be base64 encoded).
* The identifier attribute sent with this tag should be mapped to the Partner Provided ID in the DV360/Ad Manager connectors.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Network ID**: Your Google provided Network or Buyer ID.

### Load rules

Load the tag on all pages or set conditions for when the tag will load. For more information, see [About load rules]().

### Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

#### Standard

| Variable | Description |
|:---------|:------------|
| `google_nid` | Google Network ID (String) |
| `google_hm`  | Google Hosted Match Data (String) |
| `process_consent` | If you are not using a consent management platform with IAB support, map `T` to this variable to indicate that the end user has given consent. |
