---
title: POST User API
description: The POST User API creates a new user in the account.
url: https://docs.tealium.com/administration/early-access/api/scim-api/post-user-api/
---
## How it works

Use the POST method to create a new user:

```bash
POST /scim/v2/Users/
```

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication]().

## POST operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `userName` | Object | Required | The username of the user in email address format. This must be a valid email address. |
| `emails` | Array | Optional | If this value does not match `userName`, the value is ignored. |
| `active` | Boolean | Optional | Indicates whether the user is active. |
| `name` | Object | Optional | A list that contains the user’s name. Each name can contain `givenName` and `familyName`. Null and empty values are allowed. |

### Example cURL request

```bash
curl -X POST &#34;https://developer.tealiumapis.com/scim/v2/Users/&#34; \
-H &#34;Content-Type: application/scim&#43;json&#34; \
-H &#34;Accept: application/scim&#43;json&#34; \
-d &#39;{
  &#34;schemas&#34;: [&#34;urn:ietf:params:scim:schemas:core:2.0:User&#34;],
  &#34;userName&#34;: &#34;user@example.com&#34;,
  &#34;name&#34;: {
    &#34;givenName&#34;: &#34;New&#34;,
    &#34;familyName&#34;: &#34;User&#34;
  },
  &#34;emails&#34;: [{
    &#34;value&#34;: &#34;user@example.com&#34;
  }],
  &#34;active&#34;: true
}&#39;
```

### Example response


```json
{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:schemas:core:2.0:User&#34;
    ],
    &#34;id&#34;: &#34;913b0182-2531-402f-a302-fcd9d2aeda6a&#34;,
    &#34;userName&#34;: &#34;user@example.com&#34;,
    &#34;displayName&#34;: null,
    &#34;externalId&#34;: null,
    &#34;name&#34;: {
        &#34;givenName&#34;: &#34;New&#34;,
        &#34;familyName&#34;: &#34;User&#34;
    },
    &#34;emails&#34;: [
        {
            &#34;value&#34;: &#34;user@example.com&#34;
        }
    ],
    &#34;active&#34;: true,
    &#34;meta&#34;: {
        &#34;resourceType&#34;: &#34;User&#34;,
        &#34;location&#34;: &#34;/scim/v2/Users/913b0182-2531-402f-a302-fcd9d2aeda6a&#34;
    }
}
```


### Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;User payload is required.&#34;` |
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;Authentication failed.&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;Missing X-Tealium-Account header.&#34;}` |
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH.&#34;}`|
| 409 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;409&#34;,&#34;scimType&#34;: &#34;uniqueness&#34;,&#34;detail&#34;: &#34;User already exists in the given account.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;Error processing json for extension - account {ACCOUNT}&#34;}`|
