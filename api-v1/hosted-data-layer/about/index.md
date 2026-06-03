---
title: About Hosted Data Layer API
description: The Hosted Data Layer API lets you upload and access data layer objects or JSON files on Tealium's servers.
url: https://docs.tealium.com/api-v1/hosted-data-layer/about/
---This is an older version of the [current Tealium Hosted Data Layer API]().

The Hosted Data Layer API is a component of the Hosted Data Layer feature. This component lets you upload and access data layer objects on Tealium&#39;s servers. The data layer objects are static JSON objects that can be fetched by your website to supplement the on-page data layer.

## Before you begin

Before you begin, we recommend that you read about [the key concepts of the Hosted Data Layer feature]().

## Prerequisites

The following items are required to implement this feature:

* **Hosted Data Layer Extension**  
This is the first component of the Hosted Data Layer feature. The purpose of this component is to enrich the Hosted Data Layer objects into the target data layers. You must [add and configure]() the Hosted Data Layer extension before uploading the data layer objects.
* **Save or Save-As Permissions**  
If you do not currently have [Save or Save-As permissions](), contact your account administrator to grant either permission.

## Naming guidelines

Before uploading a data layer object, you must know what to name the object. The name of the data object uploaded must match the value of the lookup variable (data layer) on the page. Use the Hosted Data Layer API to upload static information about these products.

You must know the value of the lookup variable first and then name the hosted data layer objects to match the expected values. The name of the lookup variable becomes the shared link between the on-page data layer and the hosted data layer object.

### Example

For example, the name of a data layer object for the lookup variable `product_id` must match the value populated on the page. For example: &#34;prod123456&#34;. If the variable on the page is `product_id`, the value will be the ID of the product being viewed, such as &#34;prod123456&#34;.

* Data Layer on page: `utag_data.product_id = [&#34;prod123456&#34;];`
* Hosted Data Layer Object name: &#34;prod123456&#34;
* The name of your data layer object becomes the value of the `dl_id` parameter.

The name must not contain whitespace or the following Uniform Resource Identifier (URI) reserved characters: / : ? # [ ] @ ! $ &amp;amp; &#39; ( ) \* &#43; , ; = % . &#34;

