---
title: Criteo Server to Server Identification Service Tag Setup Guide
description: This article describes how to set up the Criteo Server to Server Identification Service tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/criteo-server-to-server-id-service-tag/
---
The Criteo Server to Server Identification Service tag allows an advertiser to pass a first-party identifier to Criteo to setup mapping between the first-party identifier and Criteo user identifier. This first-party identifier is subsequently used in the Criteo connector’s Send Event (First-party ID) action.

## Tag tips

* Use mappings to override standard configuration values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Partner ID**: Your Criteo partner ID. Contact your Criteo representative if you do not have this value.
* **First-party Name**: The advertiser name.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:-----|:------------|
| `p` | String | Partner ID. |
| `first_party_id` | String | First-party identifier. |
| `first_party_domain` | String | First-party domain. |
| `first_party_name` | String | First-party name. |