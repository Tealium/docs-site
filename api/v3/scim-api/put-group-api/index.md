---
title: PUT Group API
description: The PUT Group API replaces an existing group in the account.
url: https://docs.tealium.com/api/v3/scim-api/put-group-api/
---
## How it works

Use the PUT method to replace the membership of an existing group or rename a custom group:

```bash
PUT /scim/v2/Groups/{id}
```

PUT applies to both custom groups and built-in groups for membership changes. Built-in groups cannot be renamed. SCIM cannot change group permissions. Set [group permissions]() in the Tealium UI.

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication]().

## PUT operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | URL-parameter | Required | The unique identifier for the group. This value is sent as part of the REST API call. |
| `displayName` | String | Required | The name of the group. Use only letters, digits, and spaces. The name cannot be longer than 63 characters. |
| `members` | Array | Optional | A list of members in the group. Each member can contain `value`, `type`, `display`, and `$ref`. |

Built-in groups cannot be renamed and a custom group cannot have the same name as a built-in group. For more information, see .

### Example cURL request

```bash
curl -X PUT &#34;https://developer.tealiumapis.com/scim/v2/Groups/eb987394-b2b0-4a21-a1d8-7915a91e06b&#34; \
-H &#34;Content-Type: application/scim&#43;json&#34; \
-H &#34;Accept: application/scim&#43;json&#34; \
-d &#39;{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:schemas:core:2.0:Group&#34;
    ],
    &#34;displayName&#34;: &#34;Group 1&#34;,
    &#34;id&#34;: &#34;3268d9ce-54a2-4758-a19c-beb2b47059d3&#34;,
    &#34;members&#34;: [
        {
            &#34;value&#34;: &#34;298273b4-74a3-4150-aa0b-e308bbcbf06b&#34;,
            &#34;type&#34;: &#34;User&#34;,
            &#34;display&#34;: &#34;user1@example.com&#34;,
            &#34;$ref&#34;: &#34;/scim/v2/Users/298273b4-74a3-4150-aa0b-e308bbcbf06b&#34;
        },
        {
            &#34;value&#34;: &#34;33ce4543-d35c-4441-a2b7-2dd3b9f7a4fb&#34;,
            &#34;type&#34;: &#34;User&#34;,
            &#34;display&#34;: &#34;user2@example.com&#34;,
            &#34;$ref&#34;: &#34;/scim/v2/Users/33ce4543-d35c-4441-a2b7-2dd3b9f7a4fb&#34;
        }
    ]
}&#39;
```

### Example response



```json
{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:schemas:core:2.0:Group&#34;
    ],
    &#34;id&#34;: &#34;9d379d2c-2601-42d8-842c-579dc3c58612&#34;,
    &#34;displayName&#34;: &#34;Group 1&#34;,
    &#34;members&#34;: [
        {
            &#34;value&#34;: &#34;298273b4-74a3-4150-aa0b-e308bbcbf06b&#34;,
            &#34;type&#34;: &#34;User&#34;,
            &#34;display&#34;: &#34;user1@example.com&#34;,
            &#34;$ref&#34;: &#34;/scim/v2/Users/298273b4-74a3-4150-aa0b-e308bbcbf06b&#34;
        },
        {
            &#34;value&#34;: &#34;33ce4543-d35c-4441-a2b7-2dd3b9f7a4fb&#34;,
            &#34;type&#34;: &#34;User&#34;,
            &#34;display&#34;: &#34;user2@example.com&#34;,
            &#34;$ref&#34;: &#34;/scim/v2/Users/33ce4543-d35c-4441-a2b7-2dd3b9f7a4fb&#34;
        }
    ],
    &#34;meta&#34;: {
        &#34;resourceType&#34;: &#34;Group&#34;,
        &#34;location&#34;: &#34;/scim/v2/Groups/9d379d2c-2601-42d8-842c-579dc3c58612&#34;
    }
}
```


### Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;Group name (%very long name with symbols%) can not include any special characters, be longer than 63 characters.&#34;}` |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;Cannot rename built-in group &#39;Standard User&#39;. Built-in group names are immutable.&#34;}`|
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;Authentication failed.&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;Missing X-Tealium-Account header.&#34;}` |
| 404 |` {&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;Group not found in account {ACCOUNT}.&#34;}`|
| 404 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;User UUID {uuid} not found in account {ACCOUNT}.&#34;}`|
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH.&#34;}`|
| 409 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;409&#34;,&#34;scimType&#34;: &#34;uniqueness&#34;,&#34;detail&#34;: &#34;Group name &#39;grouptest&#39; already exists in account accounttest.&#34;}` |
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;Error processing json for extension - account {ACCOUNT}&#34;}`|