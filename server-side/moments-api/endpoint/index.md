---
title: Moments API endpoint
description: This article describes the Moments API endpoint.
url: https://docs.tealium.com/server-side/moments-api/endpoint/
---
## How it works

The Moments API engine creates a unique endpoint for your region, account, and profile. Each engine assigns a unique engine ID to each endpoint.

Data for visitors becomes available after you enable the engine and visitors log active sessions and generate events in the system. If you request data for a visitor and they have not logged an active session yet, the API will not return any data.

To retrieve visitor data, configure a [Tealium iQ Advanced JavaScript Code Extension]() to make a request to the Moments API endpoint. 

## GET method

Use the GET method to retrieve audience, badge, and attribute data that you specified in your Moments API engine. 

### Tealium anonymous visitor ID 

```bash
GET  https://personalization-api.{REGION}.prod.tealiumapis.com/personalization/accounts/{ACCOUNT}/profiles/{PROFILE}/engines/{ENGINE_ID}/visitors/{IDENTIFIER}?suppressNotFound={SUPPRESS_NOT_FOUND}
```

This command uses the following parameters:

| **Parameter** |**Type**| **Description**|
|---| ---| ---|
|`identifier` |String&lt;br&gt;Path parameter| The Tealium anonymous visitor ID.|
| `suppressNotFound`| Boolean&lt;br&gt;Query parameter | Determines the response type returned when a visitor is not found. The default is `false`. &lt;ul&gt;&lt;li&gt;`true` - Returns an HTTP 200 code with an empty response body.&lt;/li&gt;&lt;li&gt;`false` - Returns an HTTP 404 code.&lt;/li&gt;&lt;/ul&gt;|

### Visitor ID attribute

```bash
GET  https://personalization-api.{REGION}.prod.tealiumapis.com/personalization/accounts/{ACCOUNT}/profiles/{PROFILE}/engines/{ENGINE_ID}?attributeId={attributeId}&amp;attributeValue={attributeValue}&amp;suppressNotFound={SUPPRESS_NOT_FOUND}
```

This command uses the following parameters:

| **Parameter** |**Type**| **Description**|
|---| ---| ---|
|`attributeId` |String&lt;br&gt;Query parameter| The numeric UID representing a [Visitor ID attribute]() from your account.|
|`attributeValue`|String&lt;br&gt;Query parameter | The value to look up. Values containing special characters must be URL encoded. |
| `suppressNotFound`| Boolean&lt;br&gt;Query parameter | Determines the response type returned when a visitor is not found. The default is `false`. &lt;ul&gt;&lt;li&gt;`true` - Returns an HTTP 200 code with an empty response body.&lt;/li&gt;&lt;li&gt;`false` - Returns an HTTP 404 code.&lt;/li&gt;&lt;/ul&gt;|

For more information about anonymous IDs and secondary visitor IDs, see [Anonymous IDs, user identifiers, and visitor ID attributes]().

## Objects

Moments API returns visitor data as JSON objects that contain the audience, badge, and attribute fields you specify in the engine configuration.

The following table summarizes the data types supported by Moments API:

* Badge
* Boolean 
* Date
* Number
* String

Attributes marked as PII are not supported.

You can configure audiences and visitor attributes to be returned with the UID or name, as seen in the following body examples:

### Name example

The following example demonstrates a typical JSON payload that uses the names of attributes:

```json
{
    &#34;audiences&#34;: [
        &#34;30 Days Since Last Login&#34;
    ],
    &#34;badges&#34;: [
        &#34;Frequent visitor&#34;
    ],
    &#34;metrics&#34;: {
        &#34;Total direct visits&#34;: 1
    },
    &#34;properties&#34;: {
        &#34;Company Name&#34;: &#34;&lt;attr_value&gt;&#34;
    },
    &#34;flags&#34;: {
        &#34;Returning visitor&#34;: false
    },
    &#34;dates&#34;: {
        &#34;First visit&#34;: 1491233145706
    }
}

```

### UID example

The following example demonstrates a typical JSON payload that uses the UIDs of attributes:

```json
{
    &#34;audiences&#34;: [
        &#34;tealium_main_205&#34;
    ],
    &#34;badges&#34;: [
        &#34;31&#34;
    ],
    &#34;metrics&#34;: {
        &#34;15&#34;: 1
    },
    &#34;properties&#34;: {
        &#34;27330&#34;: &#34;&lt;attr_value&gt;&#34;
    },
    &#34;flags&#34;: {
        &#34;27&#34;: false
    },
    &#34;dates&#34;: {
        &#34;23&#34;: 1491233145706
    }
}
```

## Headers

The following HTTP headers are required in a Moments API request:

* **Referer** - The value compared to the domain allow list. If the referrer and the allow list do not match, the request is refused.
  * Example: `https://www.example.com/`
* **Origin** - The value used to address CORS errors when calling the API from JavaScript.
  * Example: `https://www.example.com/`

### Error messages

Potential error messages for this endpoint:

|**Status Code**|**Description**|
|---|---|
|200 |Status OK. The request succeeded.|
|400 |Bad request.|
|403 |The Moments API engine is not enabled.|
|404 |Not Found. The Tealium visitor ID does not have moments stored in the database.|