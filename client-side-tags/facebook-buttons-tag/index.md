---
title: Facebook Buttons Tag Setup Guide
description: This article describes how to set up the Facebook Buttons tag.
url: https://docs.tealium.com/client-side-tags/facebook-buttons-tag/
---
## Tag Tips

* Some configuration parameters only apply to **Like** box, such as border color and height.
* If you do not already have one, use the **Content Modification** extension to insert a new `DIV` in your page.
* `HREF` defaults to the page URL unless override by mappings.
* Language needs to be in the format `ll_cc`
  * `ll` is the two-letter language code
  * `cc` is the two-letter country code
  * See [Facebook Locales](https://www.facebook.com/translations/FacebookLocales.xml) for all supported codes.

* Kid Directed
  * Must be set to true if your web site or online service, or a portion of your service, is directed to children under 13.

## Tag Configuration

First, go to Tealium's tag marketplace and add the Facebook Buttons tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Action**
* **Div ID**
  * `DIV ID` where the button displays.

* **HREF**
  * URL of the page.
  * Defaults to `dom.url` in the data layer

* **Language**
  * Default is `en_US`
  * The basic format is `ll_CC`, where `ll` is a two-letter language code, and `CC` is a two-letter country code.
  * See [Facebook Locales](https://www.facebook.com/translations/FacebookLocales.xml) for all supported codes.

* **Color Scheme**
* **Layout**
  * For use with **Like** and **Share** buttons.

* **Kid Directed**
  * Must be set to `true` if your web site or online service, or a portion of your service, is directed to children under 13.

* **Size**
* **Width**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`action`|  <ul><li>Action</li></ul> |
|`language`|  <ul><li>Language</li></ul> |
|`href`|  <ul><li>Href Link</li></ul> |
|`config.colorscheme`|  <ul><li>Color Scheme</li><li>Values are `light` or `dark`</li></ul> |
|`appId`|  <ul><li>App ID</li></ul> |
|`config.size`|  <ul><li>Size</li></ul> |
|`config.width`|  <ul><li>Width</li></ul> |

### Like

|Variable| Description|
|---| ---|
|`like.layout`|  <ul><li>Layout</li></ul> |
|`like.show_faces`|  <ul><li>Show Faces</li><li>Values are `true` or `false`.</li></ul> |
|`like.kid_directed`|  <ul><li>Kid Directed Site</li><li>Values are `true` or `false`.</li></ul> |
|`like.color_scheme`|  <ul><li>Color Scheme</li><li>Values are `light` or `dark`.</li></ul> |
|`like.###`|  <ul><li>Custom Like Value</li></ul> |

### Recommend

|Variable| Description|
|---| ---|
|`rec.layout`|  <ul><li>Layout</li></ul> |
|`rec.show_faces`|  <ul><li>Show Faces</li><li>Values are `true` or `false`.</li></ul> |
|`rec.kid_directed`|  <ul><li>Kid Directed Site</li><li>Values are `true` or `false`.</li></ul> |
|`rec.color_scheme`|  <ul><li>Color Scheme</li><li>Values are `light` or `dark`.</li></ul> |
| `rec.###` |  <ul><li>Custom Recommend Value</li></ul> |

### Share

|Variable| Description|
|---| ---|
|`share.layout`|  <ul><li>Layout</li></ul> |
|`share.kid_directed`|  <ul><li>Kid Directed Site</li><li>Values are `true` or `false`.</li></ul> |
| `share.###` |  <ul><li>Custom Share Value</li></ul> |

### Send

|Variable| Description|
|---| ---|
|`send.kid_directed`|  <ul><li>Values are `true` or `false`.</li></ul> |
|`send.color_scheme`|  <ul><li>Values are `light` or `dark`.</li></ul> |
|`send.###`|  <ul><li>Custom Send Value</li></ul> |
