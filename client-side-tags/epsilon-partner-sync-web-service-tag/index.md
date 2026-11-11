---
title: Epsilon Partner Sync Web Service Tag Setup Guide
description: This article describes how to set up the Epsilon Partner Sync Web Service Tag tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/epsilon-partner-sync-web-service-tag/
---

Epsilon is the leader in outcome-based marketing with a rich, 50-year heritage in helping marketers anticipate, activate, and prove measurable business outcomes.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Advertiser Identifier**: `dtm_cid`
* **Secondary Advertiser Identifier**: `dtm_cmagic`
* **Page Visit Form ID**: `dtm_fid`

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Tag configuration

| Variable | Data Type| Description |
|---|---|---|
| `dtm_cid`  | String |Company ID |
| `dtm_cmagic`  | String |Secondary Company ID |
|  `dtm_fid`  | String |Form ID|
| `dtm_cookie_id`  | String |Cookie ID |
| `dtm_user_id`  | String |User ID |
|  `dtm_token_sc`  | String |dtm_token_sc|
|  `dtmc_tcf_string`  | String |dtmc_tcf_string|
| `cachebuster`  | String |Cache Buster |

    
