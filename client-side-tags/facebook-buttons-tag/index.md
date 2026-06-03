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

First, go to Tealium&#39;s tag marketplace and add the Facebook Buttons tag (Learn more about [how to add a tag]()).

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

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`action`|  &lt;ul&gt;&lt;li&gt;Action&lt;/li&gt;&lt;/ul&gt; |
|`language`|  &lt;ul&gt;&lt;li&gt;Language&lt;/li&gt;&lt;/ul&gt; |
|`href`|  &lt;ul&gt;&lt;li&gt;Href Link&lt;/li&gt;&lt;/ul&gt; |
|`config.colorscheme`|  &lt;ul&gt;&lt;li&gt;Color Scheme&lt;/li&gt;&lt;li&gt;Values are `light` or `dark`&lt;/li&gt;&lt;/ul&gt; |
|`appId`|  &lt;ul&gt;&lt;li&gt;App ID&lt;/li&gt;&lt;/ul&gt; |
|`config.size`|  &lt;ul&gt;&lt;li&gt;Size&lt;/li&gt;&lt;/ul&gt; |
|`config.width`|  &lt;ul&gt;&lt;li&gt;Width&lt;/li&gt;&lt;/ul&gt; |

### Like

|Variable| Description|
|---| ---|
|`like.layout`|  &lt;ul&gt;&lt;li&gt;Layout&lt;/li&gt;&lt;/ul&gt; |
|`like.show_faces`|  &lt;ul&gt;&lt;li&gt;Show Faces&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`like.kid_directed`|  &lt;ul&gt;&lt;li&gt;Kid Directed Site&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`like.color_scheme`|  &lt;ul&gt;&lt;li&gt;Color Scheme&lt;/li&gt;&lt;li&gt;Values are `light` or `dark`.&lt;/li&gt;&lt;/ul&gt; |
|`like.###`|  &lt;ul&gt;&lt;li&gt;Custom Like Value&lt;/li&gt;&lt;/ul&gt; |

### Recommend

|Variable| Description|
|---| ---|
|`rec.layout`|  &lt;ul&gt;&lt;li&gt;Layout&lt;/li&gt;&lt;/ul&gt; |
|`rec.show_faces`|  &lt;ul&gt;&lt;li&gt;Show Faces&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`rec.kid_directed`|  &lt;ul&gt;&lt;li&gt;Kid Directed Site&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`rec.color_scheme`|  &lt;ul&gt;&lt;li&gt;Color Scheme&lt;/li&gt;&lt;li&gt;Values are `light` or `dark`.&lt;/li&gt;&lt;/ul&gt; |
| `rec.###` |  &lt;ul&gt;&lt;li&gt;Custom Recommend Value&lt;/li&gt;&lt;/ul&gt; |

### Share

|Variable| Description|
|---| ---|
|`share.layout`|  &lt;ul&gt;&lt;li&gt;Layout&lt;/li&gt;&lt;/ul&gt; |
|`share.kid_directed`|  &lt;ul&gt;&lt;li&gt;Kid Directed Site&lt;/li&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
| `share.###` |  &lt;ul&gt;&lt;li&gt;Custom Share Value&lt;/li&gt;&lt;/ul&gt; |

### Send

|Variable| Description|
|---| ---|
|`send.kid_directed`|  &lt;ul&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |
|`send.color_scheme`|  &lt;ul&gt;&lt;li&gt;Values are `light` or `dark`.&lt;/li&gt;&lt;/ul&gt; |
|`send.###`|  &lt;ul&gt;&lt;li&gt;Custom Send Value&lt;/li&gt;&lt;/ul&gt; |
