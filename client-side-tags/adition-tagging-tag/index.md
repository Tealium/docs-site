---
title: Adition (Tagging) Tag Setup Guide
description: This article describes how to set up the Adition (Tagging) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/adition-tagging-tag/
---
## Tag Tips

* This is the Tagging version of Adition.
* Set the domain according to your agreement with Adition.

  * Default value: `adfarm1.adition.com`
  * AdfarmID: `ad<id>.adfarm1.adition.com`
  * Custom: `<subdomain>.<domain>.<tld>`

* The default return type is `img`.
* Map `tag[key.subkey] ` as `tag.key.subkey` in mappings.

## Tag Configuration

First, go to Tealium's tag marketplace and add the Adition (Tagging) tag. (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Domain**
  * Domain supplied by Adition.
  * The default domain is: `adfarm1.adition.com`

* **Network ID**
  * (Required) A string of numbers, such as 241

### Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

#### Standard

| Variable   | Description  |
|:-----------|:-------------|
| Tag Type   | Tag Type     |
| Domain     | Domain       |
| Tag        | [Key.Subkey] |
| Network ID | Network ID   |
