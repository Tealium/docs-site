---
title: mParticle by Rokt Tag Setup Guide
description: This article describes how to set up the mParticle by Rokt tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/mparticle-by-rokt-tag/
---
## Tag tips

Use mappings to:
  * Set up event triggers.
  * Map event-specific parameters to event names.
  * Dynamically override standard config values.
  * Dynamically override E-Commerce extension values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **mParticle API Key**: Your mParticle API Key.
* **Development Mode**: Set development mode to `True` for non-production environments.
* **Send Page View**: Set to `True` to automatically track page view events each time the tag loads.
* **First-Party Domain**: (Optional) The Rokt custom domain. If you use the Rokt first-party domain integration, enter your custom domain. For example: `rkt.yourcompany.com`.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Tag Configuration

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `account_id` | String | mParticle account ID. |
| `isDevelopmentMode` | Boolean | Development mode. |
| `domain` | String | First-party domain. |

### User identities

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `userIdentities.email` | String | Email. |
| `userIdentities.other` | String | Hashed email. |

### User attributes

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `firstname` | String | First name. |
| `lastname` | String | Last name. |
| `mobile` | String | Mobile number. |
| `age` | String | Age. |
| `gender` | String | Gender. |
| `city` | String | City. |
| `state` | String | State. |
| `zip` | String | Zip code. |
| `dob` | String | Date of birth. |
| `title` | String | Title. |
| `language` | String | Language. |
| `value` | String | Value. |
| `predictedltv` | String | LTV. |
| `cartItems` | Array of Strings | Cart items array. |

### Page view attributes

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `pageName` | String | Page name. |
| `url` | String | URL. |

### E-Commerce

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `confirmationref` | String | Confirmation number (Overrides `_corder`). |
| `amount` | String | Amount (Overrides `_csubtotal`). |
| `currency` | String | Currency (Overrides `_ccurrency`). |

### Event-specific parameters

To map events, refer to [Create an event mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Event | Description |
|:------|:------------|
| `email` | Email. |
| `firstname` | Customer first name. |
| `lastname` | Customer last name. |
| `paymenttype` | Payment type. |
| `shippingtype` | Shipping type. |
| `ccbin` | Credit card BIN. |
| `billingaddress1` | Billing address. |
| `billingaddress2` | Billing address line 2. |
| `billingzipcode` | Billing zip code. |
| `mobile` | Mobile/cell. |
| `country` | Country. |
| `language` | Language. |
| `age` | Age. |
| `gender` | Gender. |
| `identifier` | Page identifier. |
| `cartItems` | Cart items array. |
| `pageView` | Page view. |
| `selectPlacements` | Select placements. |