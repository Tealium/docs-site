---
title: Distribute Travel Tag Setup Guide
description: This article describes how to set up the Distribute Travel tag.
url: https://docs.tealium.com/client-side-tags/distribute-travel-tag/
---
## Tag configuration

First, go to the tag marketplace and add the Distribute Travel Tag to your profile (See [Add a tag](https://docs.tealium.com/manage-tags/#add-a-tag)).

After adding the Tag, configure the below settings:

* **Distribute Travel ID:** An integer value (for example, `123456`) provided by Distribute Travel

## Load rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this Tag on your site.

Recommended Load Rule: **All Pages**

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The destination variables for the Distribute Travel Tag are built into its Data Mapping tab. Available categories are:

### Standard

| **Destination Name** | **Description**                          |
|:---------------------|:-----------------------------------------|
| Distribute Travel ID | The ID given to you by Distribute Travel |
