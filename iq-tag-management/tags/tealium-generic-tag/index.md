---
title: Tealium Generic Tag
description: This article shows how to set up and configure the Tealium Generic Tag, a one-size-fits-most generic tag container used for implementing almost any third-party vendor image, iframe, or script-style tag to your pages.
url: https://docs.tealium.com/iq-tag-management/tags/tealium-generic-tag/
---
## Tag types

This tag supports one of three types: image, iframe, or script. Identifying the type of tag you are working with is important, so here are some clues to look for when setting up your tag. If the code for your tag matches any of these patterns, then choose the corresponding tag type in the tag configuration.

### Image

Image tag code snippets usually contain one of the following:

* `new Image()`
* `&lt;img src=&#34;https://`
* `document.write(&#34;&lt;img src=&#34; ... &#34;&gt;&#34;);`

### Iframe

Iframe tag code snippets usually contain one of the following:

* `document.createElement(&#39;iframe&#39;)`
* `&lt;iframe src=&#34;https://`
* `document.write(&#34;&lt;iframe src=&#34; ... &#34;&gt;&lt;/iframe&#34;);`

### Script

Script tag code snippets usually contain one of the following:

* `&lt;script type=&#34;text/javascript&#34; src=&#34;//example.com/tag.js&#34;&gt;&lt;/script&gt;`
* `document.createElement(&#39;script&#39;)`

## Tag components

To configure the Generic Tag you will need to understand the following components that make up your tag.

### Base URL

The base URL is the hostname, pathname, and file pointing to the location of the pixel. It does not include the `?` character or the query string parameters.

In our sample pixel above, the base URL is: `//www.example.com/tag.gif`

### Static and dynamic parameters

Many tags collect data by using the query string of the URL. These are the key-value pairs that appear in the URL after the `?` character. In our example the parameters are:

```nohl
cid=112233&amp;rg=us&amp;rnd=&#39; &#43; rnd_nocache &#43; &#39;&amp;ref=&#39; &#43; referrer
```

Static parameters have values that you can see in the snippet and do not change from page to page. In this example, the static parameters are:

* `cid=112233`
* `rg=us`

Dynamic parameters can be set using values that change from page to page. In this example, the dynamic parameters are:

* `rnd=`
* `ref=`

Dynamic parameters must be configured using [data mappings](). All variables configured as mappings will be appended to the query string parameter of the tag URL as key-value pairs.

### Cache bust

It&#39;s common for vendor tags to require a cache bust variable in the query string. This value is randomly generated and added to URLs to prevent the browser from caching the request. Our example includes a cache busting variable called `rnd`.

This functionality is built into the Generic Tag. Simply enable the cache bust setting and specify the name of the cache bust parameter and the Generic Tag will generate and assign the random value for you.

## Tag configuration

First, go to the tag marketplace and add the Generic Tag to your profile.

![](/images/iq-tag-management/tags/tealium_generic_tag_configuration.png)

After adding the Tag, configure the following settings:

* **Title**: (Required) The default is **Tealium Generic Tag**. You may replace it with a custom name of choice.
* **Type**: (Required) Select the type of tag.
* **Base URL**: (Required) Enter the base URL (excluding the protocol)
* **HTTPS URL**: Use this field if the HTTPS URL is different from the Base URL. 
    * If the base and HTTPS URL are the same, then add `//` as the prefix in the **Base URL** field and leave the **HTTPS URL** field empty. This tells the tag to apply HTTP and HTTPS appropriately based on the current location protocol.
    * If the URLs are different, set their respective fields.
* **Query String Delimiter**: The delimiter character that separates the query string portion from the URL. The default is `?`, but this can be changed.
* **Parameter Delimiter**: The delimiter character that separates each key-value pair in the query string. The default is `&amp;`, but this can be changed.
* **key-value Delimiter**: The delimiter character that separates a key from its value. The default is `=`, but this can be changed.
* **Query String**: Enter static and dynamic query string parameters using the delimiters defined.

### Dynamic value substitution

This tag supports dynamic value substitution, which lets you reference data layer variables directly in the Base URL, HTTPS URL, or Query String configuration fields. This provides the flexibility to create a dynamic tag based on your data layer. To use a data layer variable in a field, reference the variable name by surrounding it with `@@`. For example, to insert a data layer variable named `account_id` into the path of the URL, enter a value like this: `//example.com/path/@@account_id@@/i.gif`

Each type of data layer variable can be substituted using the following prefixes:

* **JavaScript Page Variable**: `@@js_page.variable@@`
* **Meta Tag**: `@@meta.variable@@`
* **Querystring Parameter**: `@@qp.variable@@`
* **Cookie Value**: `@@cp.variable@@`

### Load rules

[Load rules]() determine when and where to load an instance of this tag on your site.

### Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings]().

The Generic Tag supports custom mappings only. You can define a custom destination name in the text field.

### Callback function

If your tag requires code to run after the main library has loaded you can use the callback function.The Generic Tag defines an internal callback property named `u.callback` that you can redefine within a tag-scoped [Javascript Code extension](). Simply create a new extension, add your callback code, and scope it to the Generic Tag. This code will then run after the tag code has executed on the page.

The `u.callback` function cannot be used when the Generic Tag type is set to `image`.

Example:

```js
// Put this code in a Javascript Code extension scoped to the tag.
u.callback = function() {
 console.log(&#34;The tag has loaded, now do cool stuff!&#34;);
}
```

![](/images/iq-tag-management/generic-tag-callback-extension.jpg)

### Map HTML attributes

If the tag **Type** is `Script` or `Iframe`, you can add attributes to the tag by mapping a custom value or a variable to a custom destination.

For example, the following script uses a `data-id` attribute.

```js
&lt;script async data-id=&#34;1234567890&#34; src=&#34;https://example.com/js/embed.js&#34;&gt;&lt;/script&gt;
```

To provide a value for the `data-id` attribute, map a custom value to the `attribute.data-id` custom destination, as shown in the following figure:

![](/images/iq-tag-management/generic-tag-map-to-attribute-data-id.png)