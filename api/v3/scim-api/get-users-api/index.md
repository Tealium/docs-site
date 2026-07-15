---
title: GET Users API
description: The GET Users API retrieves a list of users from the account.
url: https://docs.tealium.com/api/v3/scim-api/get-users-api/
---
## How it works

Use the GET method to retrieve a list of users:

```bash
GET /scim/v2/Users/
```

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication]().

## GET operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `count` | Number | Optional | The number of records to return. The maximum value is `100`. |
| `startIndex` | Number | Optional | The first record to return in the index. If count exceeds the number of records, this value is ignored. |
| `filter` | String | Optional | Filter the users based on the username. Uses the `eq` operator to find equivalent values. |

### Example cURL request

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
https://developer.tealiumapis.com/scim/v2/Users?startIndex=1&amp;count=10&amp;filter=userName%20eq%20%22user@example.com%22
```

### Example response



```json
{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:api:messages:2.0:ListResponse&#34;
    ],
    &#34;totalResults&#34;: 1,
    &#34;startIndex&#34;: 1,
    &#34;itemsPerPage&#34;: 1,
    &#34;Resources&#34;: [
        {
            &#34;schemas&#34;: [
                &#34;urn:ietf:params:scim:schemas:core:2.0:User&#34;
            ],
            &#34;id&#34;: &#34;913b0182-2531-402f-a302-fcd9d2aeda6a&#34;,
            &#34;userName&#34;: &#34;test.userxz1@example.com&#34;,
            &#34;displayName&#34;: null,
            &#34;externalId&#34;: null,
            &#34;name&#34;: {
                &#34;givenName&#34;: &#34;Test&#34;,
                &#34;familyName&#34;: &#34;User&#34;
            },
            &#34;emails&#34;: [
                {
                    &#34;value&#34;: &#34;test.userxz1@example.com&#34;
                }
            ],
            &#34;active&#34;: true,
            &#34;meta&#34;: {
                &#34;resourceType&#34;: &#34;User&#34;,
                &#34;location&#34;: &#34;/scim/v2/Users/913b0182-2531-402f-a302-fcd9d2aeda6a&#34;
            }
        }
    ]
}
```


### Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;400&#34;,&#34;scimType&#34;: &#34;invalidValue&#34;,&#34;detail&#34;: &#34;{parameter} must be a number.&#34;` |
| 401 | `{&#34;returnCode&#34; : 1401 , &#34;message&#34; : &#34;Authentication failed.&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;Missing X-Tealium-Account header.&#34;}` |
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;Error processing json for extension - account {ACCOUNT}&#34;}`|
