---
title: GET User API
description: The GET User API retrieves an existing user from the account.
url: https://docs.tealium.com/api/v3/scim-api/get-user-api/
---
## How it works

Use the GET method to retrieve an existing user:

```bash
GET /scim/v2/Users/{id}
```

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication](https://docs.tealium.com/about-scim-api/#authentication).

## GET operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | URL-parameter | Required | The unique identifier for the user. This value is sent as part of the REST API call.|

### Example cURL request

```bash
curl --location --request GET 'https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b' \
```

### Example response


```json
{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:User"
    ],
    "id": "913b0182-2531-402f-a302-fcd9d2aeda6a",
    "userName": "fullName@tealiumscimdev.onmicrosoft.com",
    "displayName": null,
    "externalId": null,
    "name": {
        "givenName": "Given",
        "familyName": "Family"
    },
    "emails": [
        {
            "value": "fullName@tealiumscimdev.onmicrosoft.com"
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
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "Invalid ID format."` |
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 404 |` {"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "User not found in account {ACCOUNT}."}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, PUT, DELETE, PATCH."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|