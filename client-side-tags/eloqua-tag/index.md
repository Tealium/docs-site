---
title: Eloqua Tag Set Up Guide
description: This article describes how to set up the Eloqua tag.
url: https://docs.tealium.com/client-side-tags/eloqua-tag/
---
## Tag tips

* Keep the default setting of **Wait = Yes** so that the Eloqua JavaScript (JS) file runs on DOM Ready.
* For form tracking, use mapping to set values for the following parameters:
  * `form_tracking` (on)
  * `elqFormName`
  * `elqFormGUIDElement`

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see .

When adding the tag, configure the following settings:

* **Site ID**: Your site ID number.
* **First-Party Cookie Domain Name**: The domain name for your first-party cookie.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `form_tracking` | Form tracking. |
| `elqFormName` | Form name. |
| `elqFormGUIDElement` | Form element. |
| `base_url` | JavaScript file URL. |
| `elqDomainName` | First-party cookie domain name. |
| `page_url` | Page URL. |
