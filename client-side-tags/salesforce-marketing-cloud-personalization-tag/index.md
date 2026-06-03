---
title: Salesforce Marketing Cloud Personalization Tag
description: This article describes how to set up the Salesforce Marketing Cloud Personalization tag.
url: https://docs.tealium.com/client-side-tags/salesforce-marketing-cloud-personalization-tag/
---
## Tag tips

* Use mapping to override the standard configuration values dynamically.
* Supports the following E-Commerce extension parameters:
  * Customer ID (`_ccustid`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Account**: Your Salesforce MCP account name.
* **Dataset ID**: The dataset ID for event tracking.

You can find your account name and dataset ID in your Salesforce beacon URL. For example, `{{MY_ACCOUNT}}` is the account name and `{{MY_DATASET}}` is the dataset ID in `//cdn.evgnet.com/beacon/{{MY_ACCOUNT}}/{{MY_DATASET}}/scripts/evergage.min.js`.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `acct` | Account ID. |
| `dataset` | Dataset ID. |
| `company_name` | Company name. |
| `customer_id` | Customer ID (Overrides `_ccustid`). |

### Custom

| Variable | Description |
|:---------|:------------|
| `custom.request.myvar` | Custom request field. |
| `custom.page.myvar` | Custom page field. |
| `custom.visit.myvar` | Custom visit field. |
