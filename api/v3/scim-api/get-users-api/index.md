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

For more information, see [Authentication](https://docs.tealium.com/about-scim-api/#authentication).

## GET operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `count` | Number | Optional | The number of records to return. The maximum value is `100`. |
| `startIndex` | Number | Optional | The first record to return in the index. If count exceeds the number of records, this value is ignored. |
| `filter` | String | Optional | Filter the users based on the username. Uses the `eq` operator to find equivalent values. |

### Example cURL request

```bash
curl -H 'Authorization: Bearer {token}' \
https://developer.tealiumapis.com/scim/v2/Users?startIndex=1&count=10&filter=userName%20eq%20%22user@example.com%22
```

### Example response



```json
{
    "schemas": [
        "urn:ietf:params:scim:api:messages:2.0:ListResponse"
    ],
    "totalResults": 1,
    "startIndex": 1,
    "itemsPerPage": 1,
    "Resources": [
        {
            "schemas": [
                "urn:ietf:params:scim:schemas:core:2.0:User"
            ],
            "id": "913b0182-2531-402f-a302-fcd9d2aeda6a",
            "userName": "test.userxz1@example.com",
            "displayName": null,
            "externalId": null,
            "name": {
                "givenName": "Test",
                "familyName": "User"
            },
            "emails": [
                {
                    "value": "test.userxz1@example.com"
                }
            ],
            "active": true,
            "meta": {
                "resourceType": "User",
                "location": "/scim/v2/Users/913b0182-2531-402f-a302-fcd9d2aeda6a"
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
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|
