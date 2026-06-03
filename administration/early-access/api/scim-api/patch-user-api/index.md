---
title: PATCH User API
description: The PATCH User API updates an existing user in the account.
url: https://docs.tealium.com/administration/early-access/api/scim-api/patch-user-api/
---
## How it works

Use the PATCH method to update an existing user:

```bash
PATCH /scim/v2/Users/{id}
```

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication]().

## PATCH operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | URL-parameter | Required | The unique identifier for the user. This value is sent as part of the REST API call.|
| `op` | String | Optional | The operation to perform. Supported values are `add`, `replace`, and `remove`. |
| `path` | String | Optional | The attribute path that specifies the target of the operation. If omitted, the operation is performed on the entire resource. |
| `active` | Boolean | Optional | Whether the user is active. This parameter cannot be removed. Use the `replace` operation to set it to `false`. |
| `displayName` | String | Optional | The display name of the user. |
| `externalId` | String | Optional | The external ID of the user. |
| `name.givenName` | String | Optional | The given name of the user. |
| `name.familyName` | String | Optional | The family name of the user. |

`userName` cannot be changed.

### Example cURL request

#### Microsoft Entra ID

```bash
curl -X PATCH &#34;https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b&#34; \
-H &#34;Content-Type: application/scim&#43;json&#34; \
-H &#34;Accept: application/scim&#43;json&#34; \
-d &#39;{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:api:messages:2.0:PatchOp&#34;
    ],
    &#34;Operations&#34;: [
        {
            &#34;op&#34;: &#34;replace&#34;,
            &#34;path&#34;: &#34;active&#34;,
            &#34;value&#34;: &#34;false&#34;
        }
    , &#34;/early-access/api/scim-api/patch-user-api&#34;]
}&#39;
```

#### Okta

```bash
curl -X PATCH &#34;https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b&#34; \
-H &#34;Content-Type: application/scim&#43;json&#34; \
-H &#34;Accept: application/scim&#43;json&#34; \
-d &#39;{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:api:messages:2.0:PatchOp&#34;
    ],
    &#34;Operations&#34;: [
        {
            &#34;op&#34;: &#34;replace&#34;,
            &#34;value&#34;: {
                &#34;active&#34;: false
            }
        }
    , &#34;/early-access/api/scim-api/patch-user-api&#34;]
}&#39;
```

### Example response

This call returns a 204 status code.

## Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;User payload is required.&#34;` |
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;Authentication failed.&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;Missing X-Tealium-Account header.&#34;}` |
| 404 |` {&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;User not found in account {ACCOUNT}.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;Error processing json for extension - account {ACCOUNT}&#34;}`|