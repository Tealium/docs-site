---
title: POST Group API
description: The POST Group API creates a new group in the account.
url: https://docs.tealium.com/api/v3/scim-api/post-group-api/
---
## How it works

Use the POST method to create a custom group:

```bash
POST /scim/v2/Groups/
```

This creates a custom group and optionally adds members. The group is created without permissions. After creating the group, set the [group permissions](https://docs.tealium.com/permission-groups/) in the Tealium UI.

Built-in groups cannot be created through SCIM.

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication](https://docs.tealium.com/about-scim-api/#authentication).

## POST operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `displayName` | String | Required | The name of the group. Use only letters, digits, and spaces. The name cannot be longer than 63 characters. |
| `members` | Array | Optional | A list of members in the group. Each member can contain `value`, `type`, `display`, and `$ref`. |


<blockquote>
Built-in groups cannot be renamed and a custom group cannot have the same name as a built-in group. For more information, see .
</blockquote>


### Example cURL request

```bash
curl -X POST "https://developer.tealiumapis.com/scim/v2/Groups/" \
-H "Content-Type: application/scim+json" \
-H "Accept: application/scim+json" \
-d '{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:Group"
    ],
    "displayName": "Group 1",
    "members": [
        {
            "value": "aa3b970c-b459-4843-9f95-853a49b65f87",
            "type": "User",
            "display": "user1@example.com",
            "$ref": "/scim/v2/Users/aa3b970c-b459-4843-9f95-853a49b65f87"
        },
        {
            "value": "aa3b970c-b459-4843-9f95-853a49b65f88",
            "type": "User",
            "display": "user2@example.com",
            "$ref": "/scim/v2/Users/aa3b970c-b459-4843-9f95-853a49b65f88"
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
    "id": "c177ba78-88d9-43e0-8670-9f2d8c3cc83d",
    "displayName": "Group 1",
    "members": [
        {
            "value": "aa3b970c-b459-4843-9f95-853a49b65f87",
            "type": "User",
            "display": "user1@example.com",
            "$ref": "/scim/v2/Users/aa3b970c-b459-4843-9f95-853a49b65f87"
        },
        {
            "value": "aa3b970c-b459-4843-9f95-853a49b65f88",
            "type": "User",
            "display": "user2@example.com",
            "$ref": "/scim/v2/Users/aa3b970c-b459-4843-9f95-853a49b65f88"
        }
    ],
    "meta": {
        "resourceType": "Group",
        "location": "/scim/v2/Groups/c177ba78-88d9-43e0-8670-9f2d8c3cc83d"
    }
}
```


### Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "User payload is required."}` |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "Group name 'Standard User' is reserved and cannot be used."}`|
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 404 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "User UUID {uuid} not found in account {ACCOUNT}."}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, POST."}`|
| 409 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "409","scimType": "uniqueness","detail": "Group name 'group 1' already exists in the given account."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|