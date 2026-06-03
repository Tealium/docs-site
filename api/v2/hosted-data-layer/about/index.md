---
title: About Hosted Data Layer API
description: The Hosted Data Layer API lets you upload and access data layer objects or JSON files on Tealium's servers.
url: https://docs.tealium.com/api/v2/hosted-data-layer/about/
---## How it works

Hosted data layer objects are static JavaScript files that can be fetched by your website to supplement the on-page data layer. JSON files can be used in a variety of applications to transmit data efficiently.

Before you begin, we recommend that you read about [the key concepts of the Hosted Data Layer feature]().

This API is commonly used in conjunction with the [Hosted Data Layer extension]().

## Permission requirements

* Save/Save-as

## Naming guidelines

Before uploading hosted data layer objects, you must know what to name the object and the value of the lookup variable. The name of the hosted data layer object must match the expected value of the lookup variable on the page. The name of the lookup variable becomes the value of the `datalayer_id` parameter, which is the shared link between the on-page data layer and the hosted data layer object .

Hosted JSON files, which are not directly related to the on-page data layer, can have any name that conforms to the URI restrictions described in the following table:

|Value| Description|
|---| ---|
|`product_id`|  Lookup variable. |
|`prod123456`|  Value populated on the page. |
|`utag_data.product_id = [&#34;prod123456&#34;];`|  Data layer on page. |
|`prod123456`|  Hosted data layer object name. Object names must not contain whitespace or the following restricted characters: `/ : ? # [ ] @ ! $ &amp; &#39; ( ) \ &#43; , ; = % . &#34;` |

## API rate limit

While Tealium does not enforce an API rate limit, we recommend throttling your own access to this API to under 100 requests/second to maintain a stable integration.

## Authentication

The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. 

See the [Getting Started]() guide to learn about generating a bearer token from the API key.
