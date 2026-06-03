---
title: Comscore Tag Setup Guide
description: This article describes how to set up the Comscore tag.
url: https://docs.tealium.com/client-side-tags/comscore-tag/
---
## Tag Tips

* First-party cookie functionality is enabled by default. To override this behavior, set `enableFirstPartyCookie` to `false`.
* If you are using a Consent Management Platform (CMP) which implements iAB Transparency and Consent Framework (TCF) version 2.0. the Comscore tag integrates with the CMP to automatically collect user consent.
* You can manually indicate a visitor&#39;s consent by setting the `cs_ucfr` parameter to `0` (no consent) or `1` (consent).
* When the first-party cookie functionality is enabled, the Publisher Tag inspects available user consent signals to determine setting the cookie is allowed. Set `bypassUserConsentRequirementFor1PCookie` to `true` to indicate that the website/publisher is exempt from any user consent requirements.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Comscore Publisher ID**: A Comscore-provided number with at least seven digits that is unique for each publisher.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:-----|:------------|
| `c2` | String | Comscore publisher ID |
| `enableFirstPartyCookie` | `String` | Enable first-party cookie |
| `bypassUserConsentRequirementFor1PCookie` | `String` | Bypass user consent |
| `cs_ucfr` | String | Consent |

### Automatically Collected Data

| Variable | Type | Description |
|:---------|:-----|:------------|
| `c7` | String | Full page URL |
| `c8` | String | Referring URL |
| `cs_fpcu` | String | First-party `_scor_uid` cookie value |

### Demographic Data

| Variable | Type | Description |
|:---------|:-----|:------------|
| `cs_fpid` | String | First-party identifier |
| `cs_fpit` | String | Identifier type |
| `cs_fpdm` | String | First-party demographic data |
| `cs_fpdt` | String | Demographic data type |