---
title: Liveclicker Tag Setup Guide
description: This article describes how to set up the Liveclicker tag.
url: https://docs.tealium.com/client-side-tags/liveclicker-tag/
---
Liveclicker is a video commerce solution for marketing channels.

## Tag configuration

Navigate to the tag marketplace to add a new tag. For more information, see .

When adding the tag, configure the following settings:

* **Account ID**: Your Liveclicker account identifier, provided by Liveclicker, used to associate tracking requests with your account.
* **Base URL**: The Liveclicker tracking endpoint hostname and path, for example, `sc.liveclicker.net/service/track`. Do not include the protocol.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `value` | The monetary value to attribute to the conversion or order. |
| `order_id` | The unique identifier for the order or transaction associated with the conversion. |