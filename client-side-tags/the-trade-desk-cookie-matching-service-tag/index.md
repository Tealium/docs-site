---
title: The Trade Desk Cookie Matching Service Tag Setup Guide
description: This article describes how to set up the The Trade Desk Cookie Matching Service tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/the-trade-desk-cookie-matching-service-tag/
---

<blockquote>
When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting](https://docs.tealium.com/platforms/javascript/settings/#always_set_v_id) to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes](https://docs.tealium.com/platforms/javascript/version-4-50/#updating-to-version-450-or-later) and [Considerations for tealium_visitor_id when upgrading to utag 4.50+](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).
</blockquote>


## Requirements

* iQ Tag Management
* AudienceStream

## How it works

The Trade Desk Cookie Matching Service tag sets a new variable named `ttd_uuid`. It is stored as a session cookie and as a standard data layer variable. The tag triggers only once per session, by default.

The Trade Desk Cookie Matching Service tag communicates with the Trade Desk servers to request the current user's identifier. When this value is returned to the tag, the value is passed to AudienceStream so that it can be used to populate a visitor attribute containing the synced user ID. This attribute can then be used in The Trade Desk connector actions as a mapping to "Trade Desk ID (TDID)".

## Data Layer Variables

Before you add the tag, create the following data layer variables:

* `ttd_uuid`: UDO Variable
* `utag_main_ttd_uuid`: First Party Cookie

These variables are populated automatically by the cookie matching tag.

![](https://docs.tealium.com/images/client-side-tags/the-trade-desk-cookie.png)

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

After adding the tag, configure the following settings:

* **Tealium Account**: leave blank unless sending The Trade Desk user ID to a different account.
* **Tealium Profile**: leave blank unless sending The Trade Desk user ID to a different profile.

### Load Rules

[Load rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag on your site.

This tag only needs to run if the cookie match has not already occurred. You can determine this by using the cookie variable `utag_main_ttd_uuid` in a load rule condition such as:

`utag_main_ttd_uuid` is not defined

The tag also has built-in logic to only fire when the cookie is not defined, but using a load rule ensures that the tag is not loaded on a page when it has already run for the current session.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/about-data-mappings/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/manage-data-mappings/).

|**Destination Name**| **Type** | **Description**|
|---| ---| ---|
|`tealium_account`| String | The Tealium account to sync the user ID to. The default is the current account. |
|`tealium_profile`| String | The Tealium profile to sync the user ID to. The default is the current profile. |
|`gdpr`| Boolean | Pass a value that indicates if the current user resides in the European Union (EU), and therefore subject to GDPR.<ul><li>Set to `0` (default) if the user is not subject to GDPR.<br> Set to `1` if the user is subject to GDPR.</li><li>If you set this value to `0` and the visitors are located in the EU, the Cookie Sync Service returns an empty array.</li></ul> |
|`gdpr_consent_string`| String | Base64 URL-encoded GDPR consent string.|
| `domain` | String | The domain where the cookie synchronization initiates. <br> NOTE: You must add this domain to **Allowlist** in The Trade Desk configuration. |
|`order_id`| String | Overrides the `_corder` e-commerce extension value.|

## AudienceStream Setup

After you save and publish your changes to Prod, the new variables will be available in AudienceStream. The `ttd_uuid` variable appears as an event attribute, but you must create it as a visitor attribute so that it can be used in The Trade Desk connector action.

To add a visitor attribute to store the `ttd_uuid` value:

1. Navigate to **Transform > Visitor / Visit Attributes**.
1. Click **Add Attribute** and select **Visitor** scope, then **String** data type.
1. Enter the name `Trade Desk User ID`.
1. Click **Add Enrichment** and select **Set String**.
1. From **Set String to** drop-down menu select `ttd_uuid`.
1. Click **Finish**.

You can now create audiences of visitors that have their Trade Desk User ID populated. Those audiences will be used in connector actions with The Trade Desk. Map this attribute to the "Trade Desk ID (TDID)" parameter in The Trade Desk connector actions.
