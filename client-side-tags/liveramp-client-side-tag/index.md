---
title: LiveRamp Client-Side Tag Setup Guide
description: This article describes how to set up the LiveRamp Client-Side tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/liveramp-client-side-tag/
---
## Tag tips

* Use mapping to set the `pdata` values to be sent.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Tag ID**: Your tag ID provided by the vendor.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable           | Description                    |
|:-------------------|:-------------------------------|
| `tag_id`           | Tag ID.                        |
| `pdata.myvar`      | pdata.myvar.                   |
| `timestamp`        | Timestamp.                     |
| `repeat_visitor`   | Repeat visitor.                |
| `domain`           | Domain.                        |
| `device_type`      | Device type.                   |
| `traffic_source`   | Traffic source.                |
| `referral_channel` | Referral channel.              |
| `referral_source`  | Referral source.               |
| `search_group`     | Search group.                  |
| `key_act_1`        | Key #1 of custom data.         |
| `key_act_2`        | Key #2 of custom data.         |
| `key_act_3`        | Key #3 of custom data.         |
| `key_act_4`        | Key #4 of custom data.         |
| `key_act_5`        | Key #5 of custom data.         |
| `key_act_6`        | Key #6 of custom data.         |
| `key_act_7`        | Key #7 of custom data.         |
| `url_path`         | URL path.                      |