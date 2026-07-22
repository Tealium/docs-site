---
title: Ipsos iris Tag Setup Guide
description: This article describes how to set up the Ipsos iris (formerly Dotmetrics) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/ipsos-iris-tag-setup-guide/
---

Ipsos iris is a state-of-the-art hybrid methodology that combines a nationally representative establishment survey, a passively measured single-source panel, and site-centric census measurement. Data collected through tags ensures Ipsos iris measures completely across all devices to represent a publisher’s brands fully to the market. Ipsos iris through a flexible and intuitive reporting interface provides a rich understanding of digital audience behaviour on a daily, weekly, and monthly basis to ultimately support more informed decisions

## Tag tips

* Use mappings to override or dynamically set the tag configurations.
* Each website tag contains a unique section ID. If the user's website consists of more than one site section and the user wants to measure data for each section separately (for example, news, sports, weather, and so on).
* Please note alphanumeric values throughout this document support the following:
  * Up to 20 character length
  * Lowercase characters
  * Characters [a-z]
  * Numbers [0-9]

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Numeric Site Section Id**: Will be used by default if no Site Section Name String is provided.
* **Site Section Name String**: Alphanumeric website section keyword.
* **Region**: There are 3 variations of the base script. Ipsos iris does not have Geolocation functionality so they have clients deploy different tags based on region to hit the correct regional servers.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|Numeric Site Section Id (numericSiteSectionId)| [String]|
|Site Section Name String (siteSectionNameString)| [String]|
|Region (region)| [String]|

### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

|Variable| Description|
|---| ---|
|Page View (pageview)| pageview|
