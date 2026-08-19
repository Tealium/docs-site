---
title: Skai Server-to-Server Connector Setup Guide
description: Set up the Skai Server-to-Server connector to send click and conversion data to Skai's S2S API.
url: https://docs.tealium.com/server-side-connectors/skai-server-to-server-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Skai API
* API Version: v1
* API Endpoint: `https://{subdomain}.xg4ken.com`

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Subdomain**: The Skai subdomain provided during onboarding, used to build the request host `https://{subdomain}.xg4ken.com/...` (for example, `1234`).
* **Token**: The Skai secure token from onboarding. The connector sends this value as the `token` query parameter. To override this value per event, add an event-level mapping.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Conversion | ✓ | ✓ |
| Send Click | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Conversion

#### Event Data

| Parameter | Description |
| --- | --- |
| Conversion Type | String up to 100 chars (for example, `sale`, `purchase`, `signup`). |
| Revenue | Numeric (integer or decimal), no currency symbol. |
| Currency | Currency code such as `USD`. |
| Order ID | String up to 64 chars. Used by Skai for deduplication of duplicate `orderId + conversionType` combinations within 24 hours. |
| Promo Code | Optional. Free text up to 1024 chars. |
| Skai UUID | UUID string (`k_user_id`). May be empty if user ID is unavailable. Takes precedence over **User ID** when both are mapped. |
| User ID | A raw user identifier the connector converts into a Skai-compatible UUID (MD5 hash formatted as `8-4-4-4-12`) for `k_user_id`. Use this value when you do not already produce a UUID. |
| Token | Skai secure token. Defaults to the connector configuration value. Override this value per event with an event-level mapping. |

#### Additional Parameters

| Parameter | Description |
| --- | --- |
| ken_gclid | Google Click ID (`gclid`). A unique tracking parameter Google Ads appends to a URL when a user clicks an ad. Automapped from `gclid` query parameter or cookie parameter when available. |
| ken_msclkid | Microsoft Click ID (`msclkid`). A unique 32-character tracking parameter Microsoft Advertising appends to landing page URLs. Automapped from `msclkid` query parameter or cookie parameter when available. |

#### SKU Details

Map product SKU arrays to send per-product quantity and revenue data. For each SKU in an order, the connector sends `quantity_[sku]` and `revenue_[sku]` as separate query parameters. For example, `quantity_56549611915=3&revenue_56549611915=149.97`.

#### Category Aggregations

Optional. Map category names to item counts (for example, `cameras=3`, `accessories=3`) to send category-level data in the conversion request. The connector flattens these values into the query string.

#### Automapping

| Parameter | Description |
| --- | --- |
| Disable Ecommerce Automapping | When enabled, the standard ecommerce attributes `tealium_event`, `_csubtotal`, `_ccurrency`, `_corder`, and `_cpromo` are not automapped to the Skai conversion parameters `conversionType`, `revenue`, `currency`, `orderId`, and `promoCode`. |
| Disable Identifier Automapping | When enabled, the identifier attributes `skai_k_user_id`, `gclid`, and `msclkid` are not automapped to the Skai parameters `k_user_id`, `ken_gclid`, and `ken_msclkid`. |

### Send Click

#### Event Data

| Parameter | Description |
| --- | --- |
| Skai UUID | UUID string (`k_user_id`) consistent with conversions. Takes precedence over **User ID** when both are mapped. |
| User ID | A raw user identifier the connector converts into a Skai-compatible UUID (MD5 hash formatted as `8-4-4-4-12`) for `k_user_id`. Use this value when you do not already produce a UUID. |
| Redirect URL | Redirect URL, appended as the last query parameter. Defaults to `http://dummyfortracking.skai.com`. |
| prof | Skai profile ID. |
| camp | Skai campaign ID. |
| kct | Skai channel type. |
| kchid | Skai channel ID. |
| criteriaid | Keyword ID, Audience ID, or Product Group ID. |
| campaignid | Publisher campaign ID. |
| locphy | User physical location, from the publisher. |
| adgroupid | Ad group ID. |
| adpos | Ad position. |
| cid | Ad ID. |
| networkType | Network type: `Search` or `Content`. |
| kdv | Device type: `mobile`, `desktop`, or `tablet`. |
| kext | Ad extension ID. |
| kpg | Product Group ID. Microsoft only. |
| kadtype | Ad type. |
| kmc | Merchant ID for Shopping campaigns. |
| kpid | Product ID for Shopping campaigns. |
| queryStr | Search term. Microsoft only. |
| npclid | Optional publisher click ID (for example, `gclid` or `msclkid`). Use this to pass conversion data back to publishers for publisher-side optimization such as Smart Bidding. |
| Additional Parameters | Optional. Pass through any extra query parameters for the click event. |

#### Automapping

| Parameter | Description |
| --- | --- |
| Disable Identifier Automapping | When enabled, the derived `skai_k_user_id` attribute is not automapped to the Skai `k_user_id` parameter. |

