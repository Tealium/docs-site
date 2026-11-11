---
title: Criteo Adblock Tag Setup Guide
description: This article describes how to set up the Criteo Adblock tag.
url: https://docs.tealium.com/client-side-tags/criteo-adblock-tag/
---
## Prerequisites

* Complete setup in your Criteo account: Make sure Passback and CPM settings are configured.
* Criteo ZoneID

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

1. Criteo Zone ID: A unique ID provided by Criteo.
1. Container ID: The HTML Element ID of a container.
1. CPM: Select whether to auto-optimize or abide by the CPM as set in your Criteo account.
1. Enable Passback: Select whether or not to enable Criteo Passback. This must match the selection you made in Criteo.

## Load rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag on your site.

Recommended Load Rule: **Load on all pages**.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The destination variables for the Criteo Adblock Tag are built into its Data Mapping tab. Available categories are:

### Standard

| **Destination Name** | **Description**                                                                           |
|:---------------------|:------------------------------------------------------------------------------------------|
| Zone ID              | Unique ID                                                                                 |
| Container ID         | HTML Element ID of container                                                              |
| CPM                  | CPM settings as set in your Criteo account. Possible string values are `auto` or `abide`. |
| Enable Passback      | Passback flag as set in your Criteo account. Possible string values are `yes` or `no`.    |

## Vendor Documentation

* [Criteo Publisher Support](https://support.criteo.com/hc/en-us/categories/200849245)
