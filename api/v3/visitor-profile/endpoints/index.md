---
title: Visitor Profile API endpoints
description: The Visitor Profile API lets you retrieve a visitor record and get a historical visitor.
url: https://docs.tealium.com/api/v3/visitor-profile/endpoints/
---
## GET Visitor

You must use the region-specific host returned in the authentication API with this call. For more information, see [Authentication]().

Use the following GET command to retrieve a visitor record:

```bash
GET /v3/customer/visitor/accounts/{account}/profiles/{profile}?attributeId={attributeId}&amp;attributeValue={attributeValue}&amp;prettyName={prettyName}&amp;responseFilters=[&#34;{attributeId}&#34;, &#34;{attributeId}&#34;]
```

This command uses the following parameters:

* `attributeId`
  * The numeric ID representing a [Visitor ID attribute]() from your account.
* `attributeValue`
  * The value to look up.
  * Values containing special characters must be URL encoded.
* `prettyName`
  * A Boolean value indicating how attribute keys appear in the response:
    * `true` – Attributes display as user-friendly names, such as &#34;Lifetime Order Value&#34;.
    * `false` – Attributes display as numeric ID&#39;s, such as &#34;28471&#34;.
* `searchPriority`
    * The data source for your request, passed as a JSON string array. The default is `[&#34;live&#34;, &#34;historical&#34;]`.
        * `[&#34;live&#34;]` – Fetches live data from your website about current visitors.
        * `[&#34;historical&#34;]` — Fetches historical data from your website about completed visits after a 30 minute waiting period.
        * `[&#34;live&#34;, &#34;historical&#34;]` — The API will attempt to fetch live visitor data. If no live visitor data is available, the API will fetch historical visitor data.
        * `[&#34;historical&#34;, &#34;live&#34;]` — The API will attempt to fetch historical visitor data. If no historical data is available, the API will fetch live visitor data.
* `responseFilters`
    * A JSON array of IDs for filtering visitor data. If left unset, the API will return all the visitor data. When set, the `attributeId` values included in `responseFilters` will be returned in the response.
    * The maximum number of `attributeId` values that the API will return at one time is 150. If you provide more than 150 `attributeId` values, the API will return only the first 150 IDs.
    * Example: `responseFilters=[&#34;5051&#34;, &#34;5016&#34;]`

### Example cURL request

```bash
curl --location -g --request \
GET &#39;https://us-east-1-platform.tealiumapis.com/v3/customer/visitor/accounts/{account}/profiles/{profile}?attributeId=5013&amp;attributeValue=liveOnly&amp;searchPriority=[&#34;live&#34;, &#34;historical&#34;]&amp;responseFilters=[&#34;5051&#34;, &#34;5016&#34;]&#39; \
--header &#39;Authorization: Bearer {token}&#39;
```

### Example response

See the example visitor object for the format of the response.

### Error messages

Potential error messages for this include the following:

| ERROR MESSAGE | DESCRIPTION |
| --- | --- |
| 400 | `{&#34;message&#34;: &#34;You are missing an attribute Id or Attribute Value&#34;}` |
| 401 | `{&#34;message&#34;: &#34;Unauthorized&#34;}` |
| 404 | `Visitor was not found, empty response.`&lt;br&gt;`{&#34;message&#34;: &#34;Invalid query parameter value for &#39;searchPriority&#39; detected.&#34;}` |

## GET Historical Visitor

You must use the region-specific host returned in the authentication API with this call. For more information, see [Authentication]().

The GET Historical Visitor method is optimized for faster response times by searching only historical visitors.

Use the following GET command to retrieve a historical visitor record:

```bash
GET &#39;/v3/customer/visitor/historical/accounts/{account}/profiles/{profile}?attributeId={attributeId}&amp;attributeValue={attributeValue}&amp;prettyName={prettyName}&amp;responseFilters=[&#34;{attributeId}&#34;, &#34;{attributeId}&#34;]&#39;
```

This command uses the following parameters:

* `attributeId`
  * The numeric ID representing a [Visitor ID attribute]() from your account.
* `attributeValue`
    * The value to look up.
    * Values containing special characters must be URL encoded.
* `prettyName`
  * A Boolean value indicating how attribute keys display in the response:
     * `true` – Attributes display as user-friendly names, such as &#34;Lifetime Order Value&#34;.
     * `false` – Attributes display as numeric ID&#39;s, such as &#34;28471&#34;.
* `responseFilters`
    * A JSON array of IDs for filtering visitor data. If left unset, the API will return all the visitor data. When set, the `attributeId` values included in `responseFilters` will be returned in the response. The maximum number of `attributeId` values that the API will return at one time is 150. If you provide more than 150 `attributeId` values, the API will return only the first 150 IDs.

### Example cURL request

```bash
curl --location -g --request \
GET &#39;https://us-east-1-platform.tealiumapis.com/v3/customer/visitor/historical/{account}/profiles/{profile}?attributeId=5013&amp;attributeValue=liveOnly&amp;responseFilters=[&#34;5051&#34;, &#34;5016&#34;]&#39; \
--header &#39;Authorization: Bearer {token}&#39;
```

### Example response

See the example visitor object for the format of the response.

### Error messages

Potential error messages for this endpoint:

| ERROR MESSAGE | DESCRIPTION |
| --- | --- |
| 400 | `{&#34;message&#34;: &#34;You are missing an attribute Id or Attribute Value&#34;}` |
| 401 | `{&#34;message&#34;: &#34;Unauthorized&#34;}` |
| 404 |`Visitor was not found, empty response.` |
