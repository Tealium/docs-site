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

For more information, see [Authentication](https://docs.tealium.com/about-scim-api/#authentication).

## GET operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `count` | Number | Optional | The number of records to return. The maximum value is `100`. The default value is `20`. |
| `startIndex` | Number | Optional | The first record to return in the index. If count exceeds the number of records, this value is ignored. The minimum and default value is 1. |
| `filter` | String | Optional | Filter groups based on the `displayName`. Uses the `eq` operator to find equivalent values. For example: `filter=displayName eq "Standard User"`. |
| `excludedAttributes` | String | Optional | A comma-separated list of attributes to exclude from the response. Allowed values are `members`, `externalId`, `meta`, `meta.location`, `meta.resourceType`. |


<blockquote>
Built-in groups such as "Standard User", "Account Admins", "User Admins", "Privacy Admins", "Technical Admins", and "Profile Admins" are included in the response. The `id` field is the stable identifier for each group. For more information, see [Groups](https://docs.tealium.com/about-scim-api/#groups).
</blockquote>


### Example cURL requests

```bash
curl -H 'Authorization: Bearer {token}' \
'https://developer.tealiumapis.com/scim/v2/Groups'

curl -H 'Authorization: Bearer {token}' \
'https://developer.tealiumapis.com/scim/v2/Groups?startIndex=1&count=12'

curl -H 'Authorization: Bearer {token}' \
'https://developer.tealiumapis.com/scim/v2/Groups?filter=displayName%20eq%20%22group_name%22'

curl -H 'Authorization: Bearer {token}' \
'https://developer.tealiumapis.com/scim/v2/Groups?excludedAttributes=members%2Cmeta.resourceType&count=21'
```

### Example response



```json
{
    "schemas": [
        "urn:ietf:params:scim:api:messages:2.0:ListResponse"
    ],
    "totalResults": 150,
    "startIndex": 27,
    "itemsPerPage": 2,
    "Resources": [
        {
            "schemas": [
                "urn:ietf:params:scim:schemas:core:2.0:Group"
            ],
            "id": "cb869db7-42dd-4adf-a539-0bf2cac621bb",
            "displayName": "group1",
            "members": [
                {
                    "value": "298273b4-74a3-4150-aa0b-e308bbcbf05b",
                    "type": "User",
                    "display": "user1@example.com",
                    "$ref": "/scim/v2/Users/298273b4-74a3-4150-aa0b-e308bbcbf05b"
                },
                {
                    "value": "33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb",
                    "type": "User",
                    "display": "user2@example.com",
                    "$ref": "/scim/v2/Users/33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb"
                },
                {
                    "value": "53bedf02-0324-471d-9a82-052694f91a60",
                    "type": "User",
                    "display": "user3@example.com",
                    "$ref": "/scim/v2/Users/53bedf02-0324-471d-9a82-052694f91a60"
                }
            ],
            "meta": {
                "resourceType": "Group",
                "location": "/scim/v2/Groups/cb869db7-42dd-4adf-a539-0bf2cac621bb"
            }
        },
        {
            "schemas": [
                "urn:ietf:params:scim:schemas:core:2.0:Group"
            ],
            "id": "d52f469b-3e8e-4126-8a91-e31f74c703b0",
            "displayName": "group2",
            "members": [
                {
                    "value": "298273b4-74a3-4150-aa0b-e308bbcbf05b",
                    "type": "User",
                    "display": "user1@example.com",
                    "$ref": "/scim/v2/Users/298273b4-74a3-4150-aa0b-e308bbcbf05b"
                },
                {
                    "value": "33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb",
                    "type": "User",
                    "display": "user2@example.com",
                    "$ref": "/scim/v2/Users/33ce4543-d35c-4441-a2b7-2dd3b9f7a3fb"
                },
                {
                    "value": "53bedf02-0324-471d-9a82-052694f91a60",
                    "type": "User",
                    "display": "user3@example.com",
                    "$ref": "/scim/v2/Users/53bedf02-0324-471d-9a82-052694f91a60"
                }
            ],
            "meta": {
                "resourceType": "Group",
                "location": "/scim/v2/Groups/d52f469b-3e8e-4126-8a91-e31f74c703b0"
            }
        }
    ]
}
```


### Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "{parameter} must be a number."` |
| 401 | `{"returnCode" : 401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Forbidden."}` |
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|
