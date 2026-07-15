---
title: GET Groups API
description: The GET Groups API retrieves a list of groups from the account.
url: https://docs.tealium.com/api/v3/scim-api/get-groups-api/
---
## How it works

Use the GET method to retrieve a list of groups:

```bash
GET /scim/v2/Groups/
```

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication]().

## GET operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `count` | Number | Optional | The number of records to return. The maximum value is `100`. The default value is `20`. |
| `startIndex` | Number | Optional | The first record to return in the index. If count exceeds the number of records, this value is ignored. The minimum and default value is 1. |
| `filter` | String | Optional | Filter groups based on the `displayName`. Uses the `eq` operator to find equivalent values. For example: `filter=displayName eq &#34;Standard User&#34;`. |
| `excludedAttributes` | String | Optional | A comma-separated list of attributes to exclude from the response. Allowed values are `members`, `externalId`, `meta`, `meta.location`, `meta.resourceType`. |

Built-in groups such as &#34;Standard User&#34;, &#34;Account Admins&#34;, &#34;User Admins&#34;, &#34;Privacy Admins&#34;, &#34;Technical Admins&#34;, and &#34;Profile Admins&#34; are included in the response. The `id` field is the stable identifier for each group. For more information, see [Groups]().

### Example cURL requests

```bash
curl -H &#39;Authorization: Bearer {token}&#39; \
&#39;https://developer.tealiumapis.com/scim/v2/Groups&#39;

curl -H &#39;Authorization: Bearer {token}&#39; \
&#39;https://developer.tealiumapis.com/scim/v2/Groups?startIndex=1&amp;count=12&#39;

curl -H &#39;Authorization: Bearer {token}&#39; \
&#39;https://developer.tealiumapis.com/scim/v2/Groups?filter=displayName%20eq%20%22group_name%22&#39;

curl -H &#39;Authorization: Bearer {token}&#39; \
&#39;https://developer.tealiumapis.com/scim/v2/Groups?excludedAttributes=members%2Cmeta.resourceType&amp;count=21&#39;
```

### Example response



```json
{
    &#34;schemas&#34;: [
        &#34;urn:ietf:params:scim:api:messages:2.0:ListResponse&#34;
    ],
    &#34;totalResults&#34;: 150,
    &#34;startIndex&#34;: 27,
    &#34;itemsPerPage&#34;: 2,
    &#34;Resources&#34;: [
        {
            &#34;schemas&#34;: [
                &#34;urn:ietf:params:scim:schemas:core:2.0:Group&#34;
            ],
            &#34;id&#34;: &#34;cb869db7-42dd-4adf-a539-0bf2cac621bb&#34;,
            &#34;displayName&#34;: &#34;group1&#34;,
            &#34;members&#34;: [
                {
                    &#34;value&#34;: &#34;298273b4-74a3-4150-aa0b-e308bbcbf05b&#34;,
                    &#34;type&#34;: &#34;User&#34;,
                    &#34;display&#34;: &#34;user1@example.com&#34;,
                    &#34;$ref&#34;: &#34;/scim/v2/Users/298273b4-74a3-4150-aa0b-e308bbcbf05b&#34;
                },
                {
                    &#34;value&#34;: &#34;33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb&#34;,
                    &#34;type&#34;: &#34;User&#34;,
                    &#34;display&#34;: &#34;user2@example.com&#34;,
                    &#34;$ref&#34;: &#34;/scim/v2/Users/33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb&#34;
                },
                {
                    &#34;value&#34;: &#34;53bedf02-0324-471d-9a82-052694f91a60&#34;,
                    &#34;type&#34;: &#34;User&#34;,
                    &#34;display&#34;: &#34;user3@example.com&#34;,
                    &#34;$ref&#34;: &#34;/scim/v2/Users/53bedf02-0324-471d-9a82-052694f91a60&#34;
                }
            ],
            &#34;meta&#34;: {
                &#34;resourceType&#34;: &#34;Group&#34;,
                &#34;location&#34;: &#34;/scim/v2/Groups/cb869db7-42dd-4adf-a539-0bf2cac621bb&#34;
            }
        },
        {
            &#34;schemas&#34;: [
                &#34;urn:ietf:params:scim:schemas:core:2.0:Group&#34;
            ],
            &#34;id&#34;: &#34;d52f469b-3e8e-4126-8a91-e31f74c703b0&#34;,
            &#34;displayName&#34;: &#34;group2&#34;,
            &#34;members&#34;: [
                {
                    &#34;value&#34;: &#34;298273b4-74a3-4150-aa0b-e308bbcbf05b&#34;,
                    &#34;type&#34;: &#34;User&#34;,
                    &#34;display&#34;: &#34;user1@example.com&#34;,
                    &#34;$ref&#34;: &#34;/scim/v2/Users/298273b4-74a3-4150-aa0b-e308bbcbf05b&#34;
                },
                {
                    &#34;value&#34;: &#34;33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb&#34;,
                    &#34;type&#34;: &#34;User&#34;,
                    &#34;display&#34;: &#34;user2@example.com&#34;,
                    &#34;$ref&#34;: &#34;/scim/v2/Users/33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb&#34;
                },
                {
                    &#34;value&#34;: &#34;53bedf02-0324-471d-9a82-052694f91a60&#34;,
                    &#34;type&#34;: &#34;User&#34;,
                    &#34;display&#34;: &#34;user3@example.com&#34;,
                    &#34;$ref&#34;: &#34;/scim/v2/Users/53bedf02-0324-471d-9a82-052694f91a60&#34;
                }
            ],
            &#34;meta&#34;: {
                &#34;resourceType&#34;: &#34;Group&#34;,
                &#34;location&#34;: &#34;/scim/v2/Groups/d52f469b-3e8e-4126-8a91-e31f74c703b0&#34;
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
| 401 | `{&#34;returnCode&#34; : 401 , &#34;message&#34; : &#34;Authentication failed.&#34;}` |
| 403 | `{&#34;schemas&#34;: [ &#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;403&#34;,&#34;scimType&#34;: null,&#34;detail&#34;: &#34;Forbidden.&#34;}` |
| 405 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;405&#34;,&#34;scimType&#34;: &#34;invalidMethod&#34;,&#34;detail&#34;: &#34;Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH.&#34;}`|
| 500 | `{&#34;schemas&#34;: [&#34;urn:ietf:params:scim:api:messages:2.0:Error&#34;],&#34;status&#34;: &#34;500&#34;,&#34;scimType&#34;: &#34;internalServerError&#34;,&#34;detail&#34;: &#34;Error processing json for extension - account {ACCOUNT}&#34;}`|
