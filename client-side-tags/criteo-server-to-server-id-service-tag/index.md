---
title: Criteo Server to Server Identification Service Tag Setup Guide
description: This article describes how to set up the Criteo Server to Server Identification Service tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/criteo-server-to-server-id-service-tag/
---
The Criteo Server to Server Identification Service tag allows an advertiser to pass a first-party identifier to Criteo to setup mapping between the first-party identifier and Criteo user identifier. This first-party identifier is subsequently used in the Criteo connector’s Send Event (First-party ID) action.

## Tag Tips

* Use mappings to override standard configuration values.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Partner ID**: Your Criteo partner ID. Contact your Criteo representative if you do not have this value.
* **First-party Name**: The advertiser name.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:-----|:------------|
| `p` | String | Partner ID. |
| `first_party_id` | String | First-party identifier. |
| `first_party_domain` | String | First-party domain. |
| `first_party_name` | String | First-party name. |