---
title: Piano Tag Setup Guide
description: This article describes how to configure the Piano tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/piano-tag/
---
## Tag Tips

*   Replace `custom` with your datapoint name when mapping custom values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Application ID**: (Required) Your unique ID provided by Piano.
* **Use Sandbox**: Set to `true` if you are using a Piano Sandbox. The default is `false`.
* **Track Pages**: Set to `false` to disable page tracking. The default is `true`.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The destination variables for the Piano tag are built into its **Data Mapping** tab. Available categories are:

### Standard

| Variable | Type | Description |
|---| ---|---|
| `AID` | String | Your unique application ID provided by Piano. Use this to override the configuration value.|
| `isSandbox`| Boolean | Set to `true` if you are using a Piano Sandbox. Use this to override the configuration value. Available options are `true` and `false`.|
| `trackPages`| Boolean | Set to false to `disable` page tracking. Use this to override the configuration value. Available options are `true` and `false`.|
| `contentNative`| Boolean | Set to `true` to indicate sponsored content. Available options are `true` and `false`.|
| `contentCreated`| String |  An ISO 8601 formatted string local to website timezone representing the publish date and time of the content.|
| `contentAuthor`| String | The author for the published content.|
| `contentSection`|String | The section in which the content currently viewed belongs.|
| `tags`| Array of Strings | An array of tags related to the page content.|
|`zone`| String | Used to indicate the AAM platform or subsection of your site.|
| `variable.custom` | String | Additional variable data that can be used for segmentation. Replace `custom` with the name of the variable.|
| `param.user.custom`| String | Additional parameter describing the current user. Replace `custom` with the name of the parameter.|
|`param.content.custom`|String | Additional parameter describing the content consumed. Replace `custom` with the name of the parameter.|
| `param.request.custom`| String | Additional parameter describing the page request. Replace `custom` with the name of the parameter.|

## Vendor documentation

* [Piano: Implementation](https://docs.piano.io/track/implementing-piano/)