---
title: Pardot Tag Set Up Guide
description: This article describes how to set up the Pardot tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/pardot-tag/
---
## Tag tips

* Use mapping to override the standard config values dynamically.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Account ID**: An integer value. For example: `123456`.
* **Campaign ID**: An integer value. For example: `123456`.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|piAId| Sets your pardot account ID|
|piCId| Sets your pardot campaign ID|
