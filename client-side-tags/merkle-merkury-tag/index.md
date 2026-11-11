---
title: Merkle Merkury Tag Setup Guide
description: This article describes how to set up the Merkle Merkury tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/merkle-merkury-tag/
---
## Tag tips

* Adobe MediaSDK requires the Adobe Experience Cloud ID Service as well as AppMeasurement for JS to be loaded first, preferably bundled.
* This tag is fired through `utag.track('video', data);` which should be implemented in your video event handlers.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **CID**  
A client-specific numeric account number generated from Merkury Team.
* **Domain**  
The client website's domain. For example: `merkleinc.com`.
* **Send Merkury Identity Event**  
Whether to generate the `merkury_identity` event, which contains the following information:
  * `event`
  * `merkury_email_sha256`
  * `merkury_hmid`
  * `merkury_confidence_score`

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Description|Variable|
|---| ---|
| `sv_cid`|CID|
| `sv_origin`| Domain
| `uID`| Client ID |
| `em`|Email address|
| `eme`|MD5 email hash|
| `emID`| Client email ID|
| `base_url` | Base URL |