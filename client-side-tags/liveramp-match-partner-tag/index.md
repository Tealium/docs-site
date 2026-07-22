---
title: LiveRamp Match Partner Tag Setup Guide
description: This article describes how to set up the LiveRamp Match Partner tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/liveramp-match-partner-tag/
---
## Tag Tips

* Required parameters for the Email tag type:
  * Tag ID
  * Email (mapped)
* Required parameters for the Customer ID tag type:
  * Tag ID
  * Account ID
  * Customer ID (E-Commerce extension or mapped)
* Use mapping to:
  * Dynamically override the standard config values.
  * Pass a value for email.
  * Dynamically override the E-Commerce extension value for Customer ID
* If the value for email contains the `@` symbol, the email address will be converted to all lowercase, all whitespace will be removed, and it will be hashed using SHA-1.
* Supports the following E-Commerce extension values:
  * Customer ID
* If you are using the E-Commerce extension, and you have it configured to use Customer ID, no data mapping is needed for Customer ID for this tag.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Tag Type**: Select the tag type: **Email** or **Customer ID**.
* **Tag ID**: Your LiveRamp tag ID.
* **Account ID**: Your LiveRamp account ID (only for the **Customer ID** tag type).

## Load Rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Email Tag

| Variable | Description  |
|:---------|:-------------|
| `email`  | Email.       |

### Customer ID Tag

| Variable      | Description  |
|:--------------|:-------------|
| `customer_id` | Customer ID. |