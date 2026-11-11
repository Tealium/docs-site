---
title: LiveRamp Arbor Tag Setup Guide
description: This article describes how to set up the LiveRamp Arbor tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/liveramp-arbor-tag/
---
## Tag tips

* Set a customer's email to be hashed through mapping to **Customer ID**.
* Mapping to **MD5 Hash**, **SHA1 Hash**, or **SHA256 Hash** will override the respective automatic hashing of **Customer ID**.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Partner ID**: Your LiveRamp partner ID.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable     | Description    |
|:-------------|:---------------|
| `partner_id` | Partner ID.    |
| `md5`        | MD5 hash.      |
| `sha1`       | SHA1 hash.     |
| `sha256`     | SHA256 hash.   |

### E-Commerce

| Variable      | Description                         |
|:--------------|:------------------------------------|
| `customer_id` | Customer ID (Overrides `_ccustid`). |