---
title: LiveRamp Arbor Tag Setup Guide
description: This article describes how to set up the LiveRamp Arbor tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/liveramp-arbor-tag/
---
## Tag Tips

* Set a customer's email to be hashed through mapping to **Customer ID**.
* Mapping to **MD5 Hash**, **SHA1 Hash**, or **SHA256 Hash** will override the respective automatic hashing of **Customer ID**.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Partner ID**: Your LiveRamp partner ID.

## Load Rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

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