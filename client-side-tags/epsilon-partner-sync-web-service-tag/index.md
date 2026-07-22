---
title: Epsilon Partner Sync Web Service Tag Setup Guide
description: This article describes how to set up the Epsilon Partner Sync Web Service Tag tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/epsilon-partner-sync-web-service-tag/
---

Epsilon is the leader in outcome-based marketing with a rich, 50-year heritage in helping marketers anticipate, activate, and prove measurable business outcomes.

## Tag Configuration

First, go to the tag marketplace and add the Epsilon Partner Sync Web Service tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Advertiser Identifier**: `dtm_cid`
* **Secondary Advertiser Identifier**: `dtm_cmagic`
* **Page Visit Form ID**: `dtm_fid`

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Tag Configuration

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

    
