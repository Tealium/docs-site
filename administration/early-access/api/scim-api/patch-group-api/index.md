---
title: PATCH Group API
description: The PATCH Group API updates an existing group in the account.
url: https://docs.tealium.com/administration/early-access/api/scim-api/patch-group-api/
---
## How it works

Use the PATCH method to update an existing group:

```bash
PATCH /scim/v2/Groups/{id}
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
| `value` | Array | Optional | An array of user IDs. |

### Example cURL request

#### Microsoft Entra ID

```bash
curl -X PATCH &#34;https://developer.tealiumapis.com/scim/v2/Groups/eb987394-b2b0-4a21-a1d8-7915a91e06b&#34; \
-H &#34;Content-Type: application/scim&#43;json&#34; \
-H &#34;Accept: application/scim&#43;json&#34; \
-d &#39;{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:api:messages:2.0:PatchOp&#34;
    ],
    &#34;Operations&#34;: [
        {
            &#34;op&#34;: &#34;replace&#34;,
            &#34;path&#34;: &#34;members&#34;,
            &#34;value&#34;: [
               {
                   &#34;value&#34;: &#34;cb300cb6-9702-45a9-a909-f8b7c972ab7e&#34;
               }
           , &#34;/early-access/api/scim-api/patch-group-api&#34;]
        }
    , &#34;/early-access/api/scim-api/patch-group-api&#34;]
}&#39;
```

#### Okta

```bash
curl -X PATCH &#34;https://developer.tealiumapis.com/scim/v2/Groups/eb987394-b2b0-4a21-a1d8-7915a91e06b&#34; \
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
                &#34;members&#34;: [
                   {
                       &#34;value&#34;: &#34;cb300cb6-9702-45a9-a909-f8b7c972ab7e&#34;
                   }
               , &#34;/early-access/api/scim-api/patch-group-api&#34;]
            }
        }
    , &#34;/early-access/api/scim-api/patch-group-api&#34;]
}&#39;
```

### Example response



```json
{
   &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:schemas:core:2.0:Group&#34;
    ],
    &#34;id&#34;: &#34;eb987394-b2b0-4a21-a1d8-7915a91e06b&#34;,
    &#34;displayName&#34;: &#34;example group&#34;,
    &#34;members&#34;: [
        {
            &#34;value&#34;: &#34;cb300cb6-9702-45a9-a909-f8b7c972ab7e&#34;,
            &#34;type&#34;: &#34;User&#34;,
            &#34;display&#34;: &#34;exampleuser@example.onmicrosoft.com&#34;,
            &#34;$ref&#34;: &#34;/scim/v2/Users/cb300cb6-9702-45a9-a909-f8b7c972ab7e&#34;
        },
        {
            &#34;value&#34;: &#34;3bfa1b1f-5f1f-45c1-bcb8-25a70b1a4bb2&#34;,
            &#34;type&#34;: &#34;User&#34;,
            &#34;display&#34;: &#34;exampleuser@okta.com&#34;,
            &#34;$ref&#34;: &#34;/scim/v2/Users/3bfa1b1f-5f1f-45c1-bcb8-25a70b1a4bb2&#34;
        }
    ],
    &#34;meta&#34;: {
        &#34;resourceType&#34;: &#34;Group&#34;,
        &#34;location&#34;: &#34;/scim/v2/Groups/7987a965-411b-4816-b485-29fd81ca81ac&#34;
    }
}
```


## Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;User payload is required.&#34;}` |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;Cannot rename built-in group &#39;Account Admins&#39;. Built-in group names are immutable.&#34;}`|
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;Authentication failed.&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;Missing X-Tealium-Account header.&#34;}` |
| 404 |` {&#34;schemas&#34;:[&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;, &#34;scimType&#34;: &#34;noTarget&#34;, &#34;detail&#34;:&#34;Group uuid 1987a965-411b-4816-b485-29fd81ca81ac not found in account testaccount&#34;}`|
| 404 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;User UUID {uuid} not found in account {ACCOUNT}.&#34;}`|
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;], &#34;status&#34;: &#34;405&#34;, &#34;scimType&#34;: &#34;invalidMethod&#34;, &#34;detail&#34;: &#34;Method is not allowed on this endpoint. Allowed methods: GET, POST.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;Error processing json for extension - account {ACCOUNT}&#34;}`|
| 501 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;501&#34;,&#34;scimType&#34;: &#34;unsupported&#34;,&#34;detail&#34;: &#34;The operation {operation} is not supported.&#34;}`|