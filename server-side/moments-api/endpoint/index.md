---
title: Moments API endpoint
description: This article describes the Moments API endpoint.
url: https://docs.tealium.com/server-side/moments-api/endpoint/
---
## How it works

The Moments API engine creates a unique endpoint for your region, account, and profile. Each engine assigns a unique engine ID to each endpoint.

Data for visitors becomes available after you enable the engine and visitors log active sessions and generate events in the system. If you request data for a visitor and they have not logged an active session yet, the API will not return any data.

To retrieve visitor data, configure a [Tealium iQ Advanced JavaScript Code Extension](https://docs.tealium.com/advanced-javascript-code-extension/) to make a request to the Moments API endpoint. 

## GET method

Use the GET method to retrieve audience, badge, and attribute data that you specified in your Moments API engine. 

### Tealium anonymous visitor ID 

```bash
GET  https://personalization-api.{REGION}.prod.tealiumapis.com/personalization/accounts/{ACCOUNT}/profiles/{PROFILE}/engines/{ENGINE_ID}/visitors/{IDENTIFIER}?suppressNotFound={SUPPRESS_NOT_FOUND}
```

This command uses the following parameters:

| **Parameter** |**Type**| **Description**|
|---| ---| ---|
|`identifier` |String<br>Path parameter| The Tealium anonymous visitor ID.|
| `suppressNotFound`| Boolean<br>Query parameter | Determines the response type returned when a visitor is not found. The default is `false`. <ul><li>`true` - Returns an HTTP 200 code with an empty response body.</li><li>`false` - Returns an HTTP 404 code.</li></ul>|

### Visitor ID attribute

```bash
GET  https://personalization-api.{REGION}.prod.tealiumapis.com/personalization/accounts/{ACCOUNT}/profiles/{PROFILE}/engines/{ENGINE_ID}?attributeId={attributeId}&attributeValue={attributeValue}&suppressNotFound={SUPPRESS_NOT_FOUND}
```

This command uses the following parameters:

| **Parameter** |**Type**| **Description**|
|---| ---| ---|
|`attributeId` |String<br>Query parameter| The numeric UID representing a [Visitor ID attribute](https://docs.tealium.com/visitor-id-attribute/) from your account.|
|`attributeValue`|String<br>Query parameter | The value to look up. Values containing special characters must be URL encoded. |
| `suppressNotFound`| Boolean<br>Query parameter | Determines the response type returned when a visitor is not found. The default is `false`. <ul><li>`true` - Returns an HTTP 200 code with an empty response body.</li><li>`false` - Returns an HTTP 404 code.</li></ul>|

For more information about anonymous IDs and secondary visitor IDs, see [Anonymous IDs, user identifiers, and visitor ID attributes](https://docs.tealium.com/anonymous-user-visitor-id-attributes/).

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
    "audiences": [
        "30 Days Since Last Login"
    ],
    "badges": [
        "Frequent visitor"
    ],
    "metrics": {
        "Total direct visits": 1
    },
    "properties": {
        "Company Name": "<attr_value>"
    },
    "flags": {
        "Returning visitor": false
    },
    "dates": {
        "First visit": 1491233145706
    }
}

```

### UID example

The following example demonstrates a typical JSON payload that uses the UIDs of attributes:

```json
{
    "audiences": [
        "tealium_main_205"
    ],
    "badges": [
        "31"
    ],
    "metrics": {
        "15": 1
    },
    "properties": {
        "27330": "<attr_value>"
    },
    "flags": {
        "27": false
    },
    "dates": {
        "23": 1491233145706
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