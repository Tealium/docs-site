---
title: POST User API
description: The POST User API creates a new user in the account.
url: https://docs.tealium.com/api/v3/scim-api/post-user-api/
---
## How it works

Use the POST method to create a new user:

```bash
POST /scim/v2/Users/
```

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication](https://docs.tealium.com/about-scim-api/#authentication).

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
curl -X POST "https://developer.tealiumapis.com/scim/v2/Users/" \
-H "Content-Type: application/scim+json" \
-H "Accept: application/scim+json" \
-d '{
  "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User"],
  "userName": "user@example.com",
  "name": {
    "givenName": "New",
    "familyName": "User"
  },
  "emails": [{
    "value": "user@example.com"
  }],
  "active": true
}'
```

### Example response


```json
{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:User"
    ],
    "id": "913b0182-2531-402f-a302-fcd9d2aeda6a",
    "userName": "user@example.com",
    "displayName": null,
    "externalId": null,
    "name": {
        "givenName": "New",
        "familyName": "User"
    },
    "emails": [
        {
            "value": "user@example.com"
        }
    ],
    "active": true,
    "meta": {
        "resourceType": "User",
        "location": "/scim/v2/Users/913b0182-2531-402f-a302-fcd9d2aeda6a"
    }
}
```


### Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "User payload is required."` |
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH."}`|
| 409 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "409","scimType": "uniqueness","detail": "User already exists in the given account."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|
