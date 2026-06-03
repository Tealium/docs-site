---
title: Xandr Tag Setup Guide (Deprecated)
description: This article describes how to set up the Xandr tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/xandr-tag/
---
 The Xandr tag is deprecated and no longer supported. We recommend migrating to the [Xandr Universal Pixel tag]().  

## Requirements

* Xandr account

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Title**: (Required) Enter a descriptive title to identify the Tag instance.
* **Add**: (Required) Enter the Add value provided to you by Xandr. If you enter a value for Add, there is no need to enter an ID below.
* **IDs**: (Required) Enter the IDs provided to you by Xandr. If you enter IDs, there is no need to enter a value for Add above.
* **t**: (Required) Enter the value for t. Usually this value is either 1 or 2. Enter 1 for a JavaScript pixel, or enter 2 for an image pixel.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

## Data mappings

[Mapping]() is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor Tag.

You only need to map to the following destination variables if you want to dynamically set these Tag configurations. If you set one, you do not need to set the other.

* **add**
Map the data source that contains the add information.

* **id**
Map the data source that contains the ID information.

## Vendor documentation

* [Xandr wiki](https://wiki.xandr.com/)
