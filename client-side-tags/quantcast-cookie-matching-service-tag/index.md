---
title: Quantcast Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the Quantcast Cookie Matching Service tag in your Tealium iQ Tag Management account. This tag is used to generate a Quantcast ID for use in the [Quantcast Audiences]({{< relref "quantcast-audiences-connector" >}}) connector.
url: https://docs.tealium.com/client-side-tags/quantcast-cookie-matching-service-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


The Quantcast Cookie Matching Service associates the Tealium anonymous ID cookie with the Quantcast visitor ID.

## Tag Tips

* If left blank, Tealium Account and Tealium Profile are populated automatically with the current account and profile.
* Use mappings to override standard config values.
* Custom mappings will be included in the cookie sync request to Tealium.

## Tag Configuration

First, go to the tag marketplace and add the Quantcast Cookie Matching Service tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Account Code**: Account Code (P-code) is a 13 character case sensitive alpha-numeric code starting with `p-`. Contact your Quantcast representative if you have questions.
* **Tealium Account**: (Optional) Your Tealium Account name
* **Tealium Profile**: (Optional) Your Tealium Profile name

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|Account Code| (`account_code`)|
|Tealium Account| (`tealium_account`)|
|Tealium Profile| (`tealium_profile`)|

## AudienceStream Setup

This tag sends a server-side event once per session for each visitor with an event attribute named `quantcast_id`. Use this attribute to create a visitor attribute of the same name to use with the Quantcast Audiences connector.

![](https://docs.tealium.com/images/client-side-tags/quantcast-id-attribute.png)

To set up the Quantcast ID in AudienceStream:

1. Create a string event attribute named `quantcast_id`.
1. Create a string visitor attribute named `quantcast_id` with an enrichment to set the value from the event attribute.
1. In the Quancast Audiences connector, map the visitor attribute `quantcast_id` to the parameter Quancast Cookie User ID.
