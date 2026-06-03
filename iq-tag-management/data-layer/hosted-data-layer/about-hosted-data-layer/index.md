---
title: About hosted data layer
url: https://docs.tealium.com/iq-tag-management/data-layer/hosted-data-layer/about-hosted-data-layer/
---
Hosted data layer facilitates the use of statically hosted data for the purpose of supplementing the dynamic on-page data layer of your website or for hosting JSON configuration files. The data layer implemented on your website is useful for capturing real-time information, but it can be a challenge to populate your data layer with all the data that might be relevant to your business.

Hosted data layer provides a convenient mechanism to upload your static data to Tealium, from where it can be accessed by your web pages to enrich the on-page data or power an application that uses JSON files.

## Data layer objects

Hosted data layer utilizes micro data layer objects that are associated to a variable in your on-page data layer. The hosted data layer object is a text file that contains a JSON object in which the key-value pairs represent the micro data layer. This file is uploaded to Tealium using the [hosted data layer API](). The on-page data layer contains lookup variables, which are configured in the [hosted data layer extension](), that are used to determine which hosted data layer object to fetch from Tealium.

The following sections provide a description of the two required components, the hosted data layer API and the hosted data layer extension.

These objects can also be plain JSON files used for purposes other than data layer augmentation and would not require the use of the hosted data layer extension.

## Hosted data layer API

The hosted data layer API lets you upload the supplemental data to Tealium in a flat JSON object called a hosted data layer object. The API enables the programmatic processing of large amounts of data to be used as hosted data layer objects.

The following example shows the contents of a hosted data layer object:

```json
{
    &#34;product_category&#34;           : [&#34;Accessories&#34;],
    &#34;product_brand&#34;              : [&#34;Acme&#34;],
    &#34;product_sku&#34;                : [&#34;GEN-PRD-BLU&#34;],
    &#34;product_has_free_shipping&#34;  : [&#34;0&#34;],
    &#34;product_has_instore_pickup&#34; : [&#34;1&#34;]
}
```

As shown in the example, a hosted data layer object looks similar to the data layer object on your website. While the on-page data layer describes the page and customer interactions, the hosted data layer object provides additional attributes based on a specific variable on the page. Additional attributes for a specific product are provided in the example.

The API can be used to store other types of information in JSON format besides data layer values.

For detailed instructions, see [How to use the hosted data layer API]().

## Hosted data layer extension

The hosted data layer extension is the component that combines the hosted data with the in-page data, as follows:

* The extension fetches the hosted data layer objects and combines the contents of each object with the on-page data layer.
* The extension then triggers a tracking call with the merged object.  
The extension is configured to identify the data layer variables, also known as lookup variables, that are used to determine which hosted data layer objects are fetched from Tealium.

For detailed instructions, see [How to set up the hosted data layer extension]().

## Lookup variable

A lookup variable identifies which variable in the on-page data layer will be used to fetch the corresponding hosted data layer object for that page. The lookup variable is the shared link between the hosted data layer objects and the hosted data layer extension.

You must identify your lookup variables first and then use the expected values of each variable to name your hosted data layer objects. For example, if your lookup variable is `item_id` and one of the values is `123`, the corresponding hosted data layer object will be named `123.js`.

## Order of operations

The following list summarizes the order of operations for the hosted data layer extension:

* The hosted data layer process begins when `utag.js` loads on the page.
* The hosted data layer extension runs in the All Tags scope, which is executed Before Load Rules.
* When the hosted data layer extension runs and delays page tracking by setting `utag.cfg.noview=true` to ensure that no tags, load rules, or other extensions are evaluated until the hosted data is retrieved.
* While the extension is running, the lookup variables are identified and each of their values is used to fetch the matching hosted data layer object.
* If a hosted data layer object is found, the data from that object is combined with the on-page data layer into a temporary object.
* After all lookup variables are processed and a new data layer object is finalized, the extension triggers `utag.view()` with that new object.

**Timing Issue**&lt;br&gt;
Due to the delay introduced by the hosted data layer extension, extensions scoped to &#34;DOM Ready&#34; might run before some &#34;All Tags&#34; extensions.

## Summary diagram

The following list and diagram summarizes how the hosted data layer extension processes data.

![](/images/iq-tag-management/hosted-data-layer-diagram.jpg)

1. The hosted data layer API is used to upload JSON data files to Tealium.
1. The hosted data layer extension is configured with identified lookup variables in Tealium iQ Tag Management.
1. The utag.js script combines the on-page data layer with the fetched hosted data layer objects and calls utag.view().