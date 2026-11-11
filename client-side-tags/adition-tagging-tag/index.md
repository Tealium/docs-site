---
title: Adition (Tagging) Tag Setup Guide
description: This article describes how to set up the Adition (Tagging) tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/adition-tagging-tag/
---
## Tag tips

* This is the Tagging version of Adition.
* Set the domain according to your agreement with Adition.

  * Default value: `adfarm1.adition.com`
  * AdfarmID: `ad<id>.adfarm1.adition.com`
  * Custom: `<subdomain>.<domain>.<tld>`

* The default return type is `img`.
* Map `tag[key.subkey] ` as `tag.key.subkey` in mappings.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Domain**
  * Domain supplied by Adition.
  * The default domain is: `adfarm1.adition.com`

* **Network ID**
  * (Required) A string of numbers, such as 241

### Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

#### Standard

| Variable   | Description  |
|:-----------|:-------------|
| Tag Type   | Tag Type     |
| Domain     | Domain       |
| Tag        | [Key.Subkey] |
| Network ID | Network ID   |
