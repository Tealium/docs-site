---
title: Criteo Adblock Tag Setup Guide
description: This article describes how to set up the Criteo Adblock tag.
url: https://docs.tealium.com/client-side-tags/criteo-adblock-tag/
---
## Prerequisites

* Complete setup in your Criteo account: Make sure Passback and CPM settings are configured.
* Criteo ZoneID

## Tag Configuration

First, go to the tag marketplace and add the Criteo Adblock Tag to your profile ([how to add a tag]()).

After adding the tag, configure the below settings:

1. Criteo Zone ID: A unique ID provided by Criteo.
1. Container ID: The HTML Element ID of a container.
1. CPM: Select whether to auto-optimize or abide by the CPM as set in your Criteo account.
1. Enable Passback: Select whether or not to enable Criteo Passback. This must match the selection you made in Criteo.

## Load Rules

[Load Rules]() determine when and where to load an instance of this tag on your site.

Recommended Load Rule: **Load on all pages**.

## Data Mappings

Mapping is the process of sending data from a [Data Layer Variable](/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor Tag. For instructions on how to map a Variable to a Tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

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
