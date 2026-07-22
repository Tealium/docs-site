---
title: PUT User API
description: The PUT User API replaces an existing user in the account.
url: https://docs.tealium.com/api/v3/scim-api/put-user-api/
---
## How it works

Use the PUT method to replace an existing user:

```bash
PUT /scim/v2/Users/{id}
```

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication](https://docs.tealium.com/about-scim-api/#authentication).

## PUT operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | URL-parameter | Required | The unique identifier for the user. This value is sent as part of the REST API call. |
| `userName` | Object | Required | The username of the user in email address format. This must be a valid email address. You cannot change the `userName` through the API.|
| `name` | Object | Optional | A list that contains the user’s name. Each name can contain `givenName` and `familyName`. Null and empty values are allowed. |
| `emails` | Array | Optional | This value is automatically populated by the `userName`. |
| `active` | Boolean | Optional | Indicates whether the user is active.. If you are trying to delete or deactivate a user, use the [DELETE method](https://docs.tealium.com/delete-user-api/). |

### Example cURL request

```bash
curl -X PUT "https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b" \
-H "Content-Type: application/scim+json" \
-H "Accept: application/scim+json" \
-d '{
  "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User"],
  "userName": "updated.user@example.com",
  "name": {
    "givenName": "Updated",
    "familyName": "User"
  },
  "emails": [{
    "value": "updated.user@example.com"
  }],
  "active": true
}'
```

### Example response



```json
{
  "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User"],
  "id": "eb987394-b2b0-4a21-a1d8-7915a91e06b",
  "userName": "updated.user@example.com",
  "name": {
    "givenName": "Updated",
    "familyName": "User"
  },
  "emails": [{
    "value": "updated.user@example.com"
  }],
  "active": true,
  "meta": {
    "resourceType": "User",
    "location": "/scim/v2/Users/913b0182-2531-402f-a302-fcd9d2aeda6ab"
  }
}
```


### Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "userName must be a valid email address."` |
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 404 |` {"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "User not found in account {ACCOUNT}."}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|
