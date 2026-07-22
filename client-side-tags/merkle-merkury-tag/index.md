---
title: Merkle Merkury Tag Setup Guide
description: This article describes how to set up the Merkle Merkury tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/merkle-merkury-tag/
---
## Tag Tips

* Adobe MediaSDK requires the Adobe Experience Cloud ID Service as well as AppMeasurement for JS to be loaded first, preferably bundled.
* This tag is fired through `utag.track('video', data);` which should be implemented in your video event handlers.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

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

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

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