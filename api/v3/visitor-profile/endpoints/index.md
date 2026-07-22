---
title: Visitor Profile API endpoints
description: The Visitor Profile API lets you retrieve a visitor record and get a historical visitor.
url: https://docs.tealium.com/api/v3/visitor-profile/endpoints/
---
## GET Visitor


<blockquote>
You must use the region-specific host returned in the authentication API with this call. For more information, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/).
</blockquote>


Use the following GET command to retrieve a visitor record:

```bash
GET /v3/customer/visitor/accounts/{account}/profiles/{profile}?attributeId={attributeId}&attributeValue={attributeValue}&prettyName={prettyName}&responseFilters=["{attributeId}", "{attributeId}"]
```

This command uses the following parameters:

* `attributeId`
  * The numeric ID representing a [Visitor ID attribute](https://docs.tealium.com/visitor-id-attribute/) from your account.
* `attributeValue`
  * The value to look up.
  * Values containing special characters must be URL encoded.
* `prettyName`
  * A Boolean value indicating how attribute keys appear in the response:
    * `true` – Attributes display as user-friendly names, such as "Lifetime Order Value".
    * `false` – Attributes display as numeric ID's, such as "28471".
* `searchPriority`
    * The data source for your request, passed as a JSON string array. The default is `["live", "historical"]`.
        * `["live"]` – Fetches live data from your website about current visitors.
        * `["historical"]` — Fetches historical data from your website about completed visits after a 30 minute waiting period.
        * `["live", "historical"]` — The API will attempt to fetch live visitor data. If no live visitor data is available, the API will fetch historical visitor data.
        * `["historical", "live"]` — The API will attempt to fetch historical visitor data. If no historical data is available, the API will fetch live visitor data.
* `responseFilters`
    * A JSON array of IDs for filtering visitor data. If left unset, the API will return all the visitor data. When set, the `attributeId` values included in `responseFilters` will be returned in the response.
    * The maximum number of `attributeId` values that the API will return at one time is 150. If you provide more than 150 `attributeId` values, the API will return only the first 150 IDs.
    * Example: `responseFilters=["5051", "5016"]`

### Example cURL request

```bash
curl --location -g --request \
GET 'https://us-east-1-platform.tealiumapis.com/v3/customer/visitor/accounts/{account}/profiles/{profile}?attributeId=5013&attributeValue=liveOnly&searchPriority=["live", "historical"]&responseFilters=["5051", "5016"]' \
--header 'Authorization: Bearer {token}'
```

### Example response

See the example visitor object for the format of the response.

### Error messages

Potential error messages for this include the following:

| ERROR MESSAGE | DESCRIPTION |
| --- | --- |
| 400 | `{"message": "You are missing an attribute Id or Attribute Value"}` |
| 401 | `{"message": "Unauthorized"}` |
| 404 | `Visitor was not found, empty response.`<br>`{"message": "Invalid query parameter value for 'searchPriority' detected."}` |

## GET Historical Visitor


<blockquote>
You must use the region-specific host returned in the authentication API with this call. For more information, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/).
</blockquote>


The GET Historical Visitor method is optimized for faster response times by searching only historical visitors.

Use the following GET command to retrieve a historical visitor record:

```bash
GET '/v3/customer/visitor/historical/accounts/{account}/profiles/{profile}?attributeId={attributeId}&attributeValue={attributeValue}&prettyName={prettyName}&responseFilters=["{attributeId}", "{attributeId}"]'
```

This command uses the following parameters:

* `attributeId`
  * The numeric ID representing a [Visitor ID attribute](https://docs.tealium.com/visitor-id-attribute/) from your account.
* `attributeValue`
    * The value to look up.
    * Values containing special characters must be URL encoded.
* `prettyName`
  * A Boolean value indicating how attribute keys display in the response:
     * `true` – Attributes display as user-friendly names, such as "Lifetime Order Value".
     * `false` – Attributes display as numeric ID's, such as "28471".
* `responseFilters`
    * A JSON array of IDs for filtering visitor data. If left unset, the API will return all the visitor data. When set, the `attributeId` values included in `responseFilters` will be returned in the response. The maximum number of `attributeId` values that the API will return at one time is 150. If you provide more than 150 `attributeId` values, the API will return only the first 150 IDs.

### Example cURL request

```bash
curl --location -g --request \
GET 'https://us-east-1-platform.tealiumapis.com/v3/customer/visitor/historical/{account}/profiles/{profile}?attributeId=5013&attributeValue=liveOnly&responseFilters=["5051", "5016"]' \
--header 'Authorization: Bearer {token}'
```

### Example response

See the example visitor object for the format of the response.

### Error messages

Potential error messages for this endpoint:

| ERROR MESSAGE | DESCRIPTION |
| --- | --- |
| 400 | `{"message": "You are missing an attribute Id or Attribute Value"}` |
| 401 | `{"message": "Unauthorized"}` |
| 404 |`Visitor was not found, empty response.` |
