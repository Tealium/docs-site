---
title: Tealium Pixel Container Tag
description: The Tealium Pixel Container is a tag that can load up to eight pixels on the same page. This tag can be used to implement vendor tags that have not yet been added to the tag marketplace.
url: https://docs.tealium.com/iq-tag-management/tags/tealium-pixel-container-tag/
---
In most cases where the Pixel Container tag might be used, the [Tealium Generic Tag]() is a better choice that offers more options. The Pixel Container is best used when adding multiple simple tags that use the same load rule.

## Tag types

This tag supports two formats: image and iframe. Determining the correct format is essential for proper configuration. Use the following guidelines to identify which type you are working with. If the code for the tag matches one of the patterns below, select the corresponding tag type during setup.

### Image

Image tag code snippets usually contain one of the following:

* `new Image()`
* `&lt;img src=&#34;https://`
* `document.write(&#34;&lt;img src=&#34; ... &#34;&gt;&#34;);`

For example, a vendor might provide a snippet like this:

```html
&lt;img src=&#34;http://ads.example.net/track?src=1234567&amp;type=abcde123&amp;cat=fghij456&#34; width=&#34;1&#34; height=&#34;1&#34; style=&#34;display:none&#34;&gt;
```

To configure this pixel, extract the `src` URL and enter it in the **Pixel URL** field:

`http://ads.example.net/track?src=1234567&amp;type=abcde123&amp;cat=fghij456`

### Iframe

Iframe tag code snippets usually contain one of the following:

* `document.createElement(&#39;iframe&#39;)`
* `&lt;iframe src=&#34;https://`
* `document.write(&#34;&lt;iframe src=&#34; ... &#34;&gt;&lt;/iframe&#34;);`

For example, a vendor might provide a snippet like this:

```html
&lt;iframe src=&#34;http://ads.example.net/track?src=1234567&amp;type=abcde123&amp;cat=fghij456&#34; width=&#34;1&#34; height=&#34;1&#34; frameborder=&#34;0&#34;&gt;&lt;/iframe&gt;
```

To configure this pixel, extract the `src` URL and enter it in the **Pixel URL** field:

`http://ads.example.net/track?src=1234567&amp;type=abcde123&amp;cat=fghij456`

## Tag configuration

First, go to the tag marketplace and add the Tealium Pixel Container to your profile.

![](/images/iq-tag-management/tags/tealium_pixel_container_tag.png)

After adding the tag, configure the following settings:

* **Title**: The default is `Tealium Pixel (or Iframe) Container`. You may replace it with a custom name of choice.
* **Type**: Select the type of tag.
* **Auto Cache Bust:** When enabled, a randomly generated value is appended to each pixel URL as a query parameter. This value prevents browsers and ad servers from serving a cached version of the pixel. For example, if your pixel URL is `https://ads.example.net/track?src=1234567`, the tag fires it as: `https://ads.example.net/track?src=1234567&amp;_rnd=0.7351829476`
* **Cache Bust Name**: (Optional) Specify a custom name for the cache bust parameter instead of the default `_rnd`. For example, entering `ord` causes the tag to fire: `https://ads.example.net/track?src=1234567&amp;ord=0.7351829476`
* **Pixel 1-8**: The URL of each pixel to load. Ensure that each URL begins with `http://`, `https://`, or `//`.
* **Pixel 1-8 Title**: Provide a title for each pixel.

## Dynamic value substitution

This tag supports dynamic value substitution, which lets you reference data layer variables directly in the Pixel 1-8 configuration fields. This provides the flexibility to create dynamic tag URLs based on your data layer. To use a data layer variable in a pixel URL, reference the variable name by surrounding it with `@@`. For example, to insert a data layer variable named `account_id` into the path of the URL, enter a value like this: `//example.com/path/@@account_id@@/i.gif`

Each type of data layer variable can be substituted using the following prefixes:

* **Universal Data Object**:`@@variable@@`
* **JavaScript Page Variable**: `@@js\_page.variable@@`
* **Meta Tag**: `@@meta.variable@@`
* **Querystring Parameter**: `@@qp.variable@@`
* **Cookie Value**: `@@cp.variable@@`

## Load rules

[Load rules]() determine when and where to load an instance of this tag on your site.

## Data mappings

This tag does not support data mappings. All parameters must be set in the URL of the pixel.