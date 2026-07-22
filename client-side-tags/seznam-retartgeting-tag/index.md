---
title: Seznam Retargeting Tag Setup Guide
description: This article describes how to set up the Seznam Retargeting tag.
url: https://docs.tealium.com/client-side-tags/seznam-retartgeting-tag/
---
Seznam Retargeting is designed to reach users who visit your site.

## Tag Tips

* Use mappings to:
    * Dynamically override standard configuration values.
    * Dynamically override E-Commerce extension values.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Rtg Id**: Your Seznam-supplied Merchant ID.
* **Auto Tracking**: Enable this option to call the `retargetingHit()` function every time the tag loads.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Configuration

| Variable | Type | Description |
|:---------|:-----|:------------|
| `rtgId` | String | Your Seznam-supplied Merchant ID. |
| `auto_tracking` | Boolean | Auto tracking. Enable this option to call the `retargetingHit()` function every time the tag loads. |

### Standard

| Variable | Type | Description |
|:---------|:-----|:------------|
| `eid` | String | User email. |
| `a1` | String | User country. |
| `a2` | String | User city. |
| `a3` | String | User street. |
| `a4` | String | User house number. |
| `a5` | String | User postcode. |
| `tid` |String | User phone number. |

### Retargeting

| Variable | Type | Description |
|:---------|:-----|:------------|
| `consent` | Number  | User consent. <ul><li>`0`: No consent.</li><li>`1`: Consent given.</li></ul> |
| `itemId` | String | Offer identifier. |
| `category` | String | Category. |
| `pageType` | String | Page type. |
| `rtgUrl` | String | Query string. |

### Conversion

| Variable | Type| Description |
|:---------|:-----|:------------|
| `id` | String | Conversion identifier. |
| `value` | String | Order value (Overrides `_ctotal`). |
| `orderId` | String | Order identifier (Overrides `_corder`). |
| `zboziType` | String | Type of measurement (Overrides `_ctype`). |
| `zboziId` | String | Premises ID. |

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Event | Description |
|:------|:------------|
| `eid` | User email. |
| `a1` | User country. |
| `a2` | User city. |
| `a3` | User street. |
| `a4` | User house number. |
| `a5` | User postcode. |
| `tid` | User phone number. |
| `consent` | User consent. |
| `itemId` | Offer identifier. |
| `category` | Category. |
| `pageType` | Page type. |
| `rtgUrl` | Query string. |
| `id` | Conversion identifier. |
| `value` | Order value. |
| `orderId` | Order identifier. |
| `zboziType` | Type of measurement. |
| `zboziId` | Premises ID. |
