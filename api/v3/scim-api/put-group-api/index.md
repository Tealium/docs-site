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

PUT applies to both custom groups and built-in groups for membership changes. Built-in groups cannot be renamed. SCIM cannot change group permissions. Set [group permissions](https://docs.tealium.com/permission-groups/) in the Tealium UI.

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication](https://docs.tealium.com/about-scim-api/#authentication).

## PUT operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | URL-parameter | Required | The unique identifier for the group. This value is sent as part of the REST API call. |
| `displayName` | String | Required | The name of the group. Use only letters, digits, and spaces. The name cannot be longer than 63 characters. |
| `members` | Array | Optional | A list of members in the group. Each member can contain `value`, `type`, `display`, and `$ref`. |


<blockquote>
Built-in groups cannot be renamed and a custom group cannot have the same name as a built-in group. For more information, see .
</blockquote>


### Example cURL request

```bash
curl -X PUT "https://developer.tealiumapis.com/scim/v2/Groups/eb987394-b2b0-4a21-a1d8-7915a91e06b" \
-H "Content-Type: application/scim+json" \
-H "Accept: application/scim+json" \
-d '{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:Group"
    ],
    "displayName": "Group 1",
    "id": "3268d9ce-54a2-4758-a19c-beb2b47059d3",
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
    ]
}'
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
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "Group name (%very long name with symbols%) can not include any special characters, be longer than 63 characters."}` |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "Cannot rename built-in group 'Standard User'. Built-in group names are immutable."}`|
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 404 |` {"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "Group not found in account {ACCOUNT}."}`|
| 404 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "User UUID {uuid} not found in account {ACCOUNT}."}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH."}`|
| 409 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "409","scimType": "uniqueness","detail": "Group name 'grouptest' already exists in account accounttest."}` |
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|