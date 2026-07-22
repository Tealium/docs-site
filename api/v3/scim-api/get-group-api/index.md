---
title: GET Group API
description: The GET Group API retrieves an existing group from the account.
url: https://docs.tealium.com/api/v3/scim-api/get-group-api/
---
## How it works

Use the GET method to retrieve an existing group:

```bash
GET /scim/v2/Groups/{id}
```

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication](https://docs.tealium.com/about-scim-api/#authentication).

## GET operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | URL-parameter | Required | The unique identifier for the group. This value is sent as part of the REST API call.|

### Example cURL request

```bash
curl --location --request GET 'https://developer.tealiumapis.com/scim/v2/Groups/eb987394-b2b0-4a21-a1d8-7915a91e06b' \
```

### Example response


```json
{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:Group"
    ],
    "id": "9d379d2c-2601-42d8-842c-579dc3c58612",
    "displayName": "Group 1",
    "members": [
        {
            "value": "298273b4-74a3-4150-aa0b-e308bbcbf06b",
            "type": "User",
            "display": "user1@example.com",
            "$ref": "/scim/v2/Users/298273b4-74a3-4150-aa0b-e308bbcbf06b"
        },
        {
            "value": "33ce4543-d35c-4441-a2b7-2dd3b9f7a4fb",
            "type": "User",
            "display": "user2@example.com",
            "$ref": "/scim/v2/Users/33ce4543-d35c-4441-a2b7-2dd3b9f7a4fb"
        }
    ],
    "meta": {
        "resourceType": "Group",
        "location": "/scim/v2/Groups/9d379d2c-2601-42d8-842c-579dc3c58612"
    }
}
```


### Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "Invalid ID format."` |
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 404 |` {"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "Group not found in account {ACCOUNT}."}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|