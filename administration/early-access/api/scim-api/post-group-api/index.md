---
title: POST Group API
description: The POST Group API creates a new group in the account.
url: https://docs.tealium.com/administration/early-access/api/scim-api/post-group-api/
---
## How it works

Use the POST method to create a group:

```bash
POST /scim/v2/Groups/
```

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication]().

## POST operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `displayName` | String | Required | The name of the group. Use only letters, digits, and spaces. The name cannot be longer than 63 characters. |
| `members` | Array | Optional | A list of members in the group. Each member can contain `value`, `type`, `display`, and `$ref`. |

Built-in groups cannot be renamed and a custom group cannot have the same name as a built-in group. For more information, see .

### Example cURL request

```bash
curl -X POST &#34;https://developer.tealiumapis.com/scim/v2/Groups/&#34; \
-H &#34;Content-Type: application/scim&#43;json&#34; \
-H &#34;Accept: application/scim&#43;json&#34; \
-d &#39;{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:schemas:core:2.0:Group&#34;
    ],
    &#34;displayName&#34;: &#34;Group 1&#34;,
    &#34;members&#34;: [
        {
            &#34;value&#34;: &#34;aa3b970c-b459-4843-9f95-853a49b65f87&#34;,
            &#34;type&#34;: &#34;User&#34;,
            &#34;display&#34;: &#34;user1@example.com&#34;,
            &#34;$ref&#34;: &#34;/scim/v2/Users/aa3b970c-b459-4843-9f95-853a49b65f87&#34;
        },
        {
            &#34;value&#34;: &#34;aa3b970c-b459-4843-9f95-853a49b65f88&#34;,
            &#34;type&#34;: &#34;User&#34;,
            &#34;display&#34;: &#34;user2@example.com&#34;,
            &#34;$ref&#34;: &#34;/scim/v2/Users/aa3b970c-b459-4843-9f95-853a49b65f88&#34;
        }
    , &#34;/early-access/api/scim-api/post-group-api&#34;]
}&#39;
```

### Example response


```json
{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:schemas:core:2.0:Group&#34;
    ],
    &#34;id&#34;: &#34;c177ba78-88d9-43e0-8670-9f2d8c3cc83d&#34;,
    &#34;displayName&#34;: &#34;Group 1&#34;,
    &#34;members&#34;: [
        {
            &#34;value&#34;: &#34;aa3b970c-b459-4843-9f95-853a49b65f87&#34;,
            &#34;type&#34;: &#34;User&#34;,
            &#34;display&#34;: &#34;user1@example.com&#34;,
            &#34;$ref&#34;: &#34;/scim/v2/Users/aa3b970c-b459-4843-9f95-853a49b65f87&#34;
        },
        {
            &#34;value&#34;: &#34;aa3b970c-b459-4843-9f95-853a49b65f88&#34;,
            &#34;type&#34;: &#34;User&#34;,
            &#34;display&#34;: &#34;user2@example.com&#34;,
            &#34;$ref&#34;: &#34;/scim/v2/Users/aa3b970c-b459-4843-9f95-853a49b65f88&#34;
        }
    ],
    &#34;meta&#34;: {
        &#34;resourceType&#34;: &#34;Group&#34;,
        &#34;location&#34;: &#34;/scim/v2/Groups/c177ba78-88d9-43e0-8670-9f2d8c3cc83d&#34;
    }
}
```


### Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;User payload is required.&#34;}` |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;Group name &#39;Standard User&#39; is reserved and cannot be used.&#34;}`|
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;Authentication failed.&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;Missing X-Tealium-Account header.&#34;}` |
| 404 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;404&#34;,&#34;scimType&#34;: &#34;noTarget&#34;,&#34;detail&#34;: &#34;User UUID {uuid} not found in account {ACCOUNT}.&#34;}`|
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;Method is not allowed on this endpoint. Allowed methods: GET, POST.&#34;}`|
| 409 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;409&#34;,&#34;scimType&#34;: &#34;uniqueness&#34;,&#34;detail&#34;: &#34;Group name &#39;group 1&#39; already exists in the given account.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;Error processing json for extension - account {ACCOUNT}&#34;}`|