---
title: AIM XR Website Tag Setup Guide (formerly DMD)
description: This article describes how to set up the AIM XR Website tag.
url: https://docs.tealium.com/client-side-tags/aim-xr-website-tag/
---
DMD, an IQVIA Business, is a healthcare identity company dedicated to connecting marketers to key healthcare audiences for impactful engagement. Their Audience Identity Manager Extended Reach (AIM XR) provides identity resolution for Healthcare Professionals (HCPs). This tag will load DMD’s AIM XR library and will scan for a DMD tagged device. Upon identification, `AIM.ondetect()` will execute whatever is located within the function.

## Tag tips

* Use mappings to override standard config values.

## Tag configuration

When adding the tag, configure the following settings:

* **Version**: Select the version of the tag to use.
* **Data Layer Name**: By default, the data layer initiated and referenced by the global site tag is named `aimDataLayer`. Rename the data layer only if your project requires a separate name.
* **API KEY**: The AIM XR API key used in the `AIM.init` function.
* **Trigger Event AIM Signal**: Signal data is being sent to Tealium Collect on server-side.
* **Session Information Event**: Request session information (`id`, `timestamp`).
* **Include POI Identity Type**: Enable this option to include POI identity type. The default value is `No`.
* **Include TST Identity Type**: Enable this option to include TST identity type. The default value is `No`.
* **Include UNK Identity Type**: Enable this option to include UNK identity type. The default value is `No`.
* **Send HCP data to**: Specify the unique identifiers (UIDs) of the tags you want to selectively target for sending High-Value Customer (HCP) data through `utag.link` (separated by commas). By default, it uses all tags.
* **Tag must only fire on the first page view**: By setting the parameter to `Yes`, `utag.link` will exclusively activate during the initial page view of the website. If the parameter is set to `No`, `utag.link` will fire on all pages.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Configuration

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `apiKey` | String | API key. |
| `triggerEvent` | Boolean | Trigger Event AIM signal. |
| `sessionInformation` | Boolean | Session information. |
| `poiSelected` | Boolean | Include POI identity type. |
| `tstSelected` | Boolean | Include TST identity type. |
| `unkSelected` | Boolean | Include UNK identity type. |
| `selectedTagsToSend` | String | Send HCP data to. |
| `firstPageOnly` | Boolean | Tag must only fire on the first page view. |