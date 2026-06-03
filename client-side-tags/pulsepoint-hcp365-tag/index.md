---
title: PulsePoint HCP365 Pixel Tag Setup Guide
description: This article describes how to set up the PulsePoint HCP365 Pixel tag.
url: https://docs.tealium.com/client-side-tags/pulsepoint-hcp365-tag/
---
HCP365, the first self-serve product under the Signal platform, uncovers who, how, and when your HCP audience organically engages with branded digital touch points at the NPI-level. The HCP365 Pixel will send page-level information into your PulsePoint system.

## Tag Tips

*  Use mappings to override Standard parameters.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

*  **PulsePoint Container Pixel**: PulsePoint container pixel that is unique to each client
*  **Token**: PulsePoint internal identifier for a brand (for example, Merck advertiser has multiple brands so multiple tokens)

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable | Description |
| --- | --- |
| PulsePoint container pixel (`p`) | `String` |
| Token (`token`) | `String` |
| Base Url (`base_url`) | `String` |
| CCPA Opt-Out (`us_privacy`) (Required) | `String` |
| URL of the page the tag was fired (`url`) (Required) | `String` |
| Referrer of the page (`rr`) (Required) | `String` |
| Additional parameters for passing additional information to the pixel (`param1`) | `String` |
| Additional parameters for passing additional information to the pixel (`param2`) | `String` |
| Additional parameters for passing additional information to the pixel (`param3`) | `String` |
| Additional parameters for passing additional information to the pixel (`param4`) | `String` |
| Additional parameters for passing additional information to the pixel (`param5`) | `String` |
| Form details if tag is fired on form submission (`frmtext`) | `String` |
| Link text of the link being clicked or document name of the document being downloaded (`clktext`) | `String` |