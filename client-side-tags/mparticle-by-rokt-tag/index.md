---
title: mParticle by Rokt Tag Setup Guide
description: This article describes how to set up the mParticle by Rokt tag in your Tealium Tag Management account.
url: https://docs.tealium.com/client-side-tags/mparticle-by-rokt-tag/
---
## Tag tips

Use mappings to:
  * Set up event triggers.
  * Map event-specific parameters to event names.
  * Dynamically override standard config values.
  * Dynamically override E-Commerce extension values.


<blockquote>
A tag template update is required to use the new identity, attribute, and placement mappings added in the v3 update. Existing mappings continue to work with older templates.
</blockquote>


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
| `userIdentities.email_sha256` | String | Hashed email. |
| `userIdentities.mobile_number` | String | Mobile number in E.164 format. |
| `userIdentities.mobile_sha256` | String | Hashed mobile number. |
| `userIdentities.customerid` | String | Customer or account identifier. |
| `userIdentities.other` | String | (Deprecated) Hashed email. Use `userIdentities.email_sha256` instead. |

### User attributes

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `firstname` | String | First name. |
| `firstnamesha256` | String | Hashed first name. |
| `lastname` | String | Last name. |
| `lastnamesha256` | String | Hashed last name. |
| `mobile_number` | String | Mobile number. |
| `mobilesha256` | String | Hashed mobile number. |
| `mobile` | String | (Deprecated) Mobile number. Use `mobile_number` instead. |
| `age` | String | Age. |
| `gender` | String | Gender. |
| `city` | String | City. |
| `state` | String | State. |
| `zip` | String | Zip code. |
| `zipsha256` | String | Hashed zip code. |
| `zip4sha256` | String | Hashed zip code +4. |
| `billingzipsha256` | String | Hashed billing zip code. |
| `billingzip4sha256` | String | Hashed billing zip code +4. |
| `dob` | String | Date of birth. |
| `title` | String | Title. |
| `language` | String | Language. |
| `value` | String | Value. |
| `predictedltv` | String | LTV. |

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

### Select placements

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `identifier` | String | Rokt placement identifier. |
| `cartItems` | Array of Objects | Cart line items. Each item is a structured object. |

### Event-specific parameters

| Parameter | Description |
|:------|:------------|
| `email` | Email |
| `firstname` | Customer First Name |
| `lastname` | Customer Last Name |
| `paymenttype` | Payment Type |
| `shippingtype` | Shipping Type |
| `shippingmethod` | Shipping Method |
| `paymentServiceProvider` | Payment Service Provider |
| `ccbin` | ccbin |
| `billingaddress1` | Billing Address |
| `billingaddress2` | Billing Address 2 |
| `billingzipcode` | Billing Zip Code |
| `mobile` | Mobile/Cell |
| `mobile_number` | Mobile Number |
| `mobilesha256` | Mobile SHA256 |
| `firstnamesha256` | First Name SHA256 |
| `lastnamesha256` | Last Name SHA256 |
| `zipsha256` | Zip SHA256 |
| `zip4sha256` | Zip4 SHA256 |
| `billingzipsha256` | Billing Zip SHA256 |
| `billingzip4sha256` | Billing Zip4 SHA256 |
| `country` | Country |
| `language` | Language |
| `age` | Age |
| `gender` | Gender |
| `identifier` | Page Identifier |
| `cartItems` | Cart Items |
| `pageView` | Page View |
| `selectPlacements` | Select Placements |