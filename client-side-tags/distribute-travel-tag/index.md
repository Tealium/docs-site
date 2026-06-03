---
title: Distribute Travel Tag Setup Guide
description: This article describes how to set up the Distribute Travel tag.
url: https://docs.tealium.com/client-side-tags/distribute-travel-tag/
---
## Tag Configuration

First, go to the tag marketplace and add the Distribute Travel Tag to your profile (See [Add a tag]()).

After adding the Tag, configure the below settings:

* **Distribute Travel ID:** An integer value (for example, `123456`) provided by Distribute Travel

## Load Rules

[Load Rules]() determine when and where to load an instance of this Tag on your site.

Recommended Load Rule: **All Pages**

## Data Mappings

Mapping is the process of sending data from a [Data Layer Variable](/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor Tag. For instructions on how to map a Variable to a Tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The destination variables for the Distribute Travel Tag are built into its Data Mapping tab. Available categories are:

### Standard

| **Destination Name** | **Description**                          |
|:---------------------|:-----------------------------------------|
| Distribute Travel ID | The ID given to you by Distribute Travel |
