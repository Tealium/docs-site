---
title: DELETE User API
description: The DELETE User API removes an existing user from the account.
url: https://docs.tealium.com/api/v3/scim-api/delete-user-api/
---
## How it works

Use the DELETE method to remove an existing user:

```bash
DELETE /scim/v2/Users/{id}
```


<blockquote>
If the user exists on multiple accounts, the user remains on the other accounts. If the user is removed from the only account they are on, the user remains without access to any accounts.
</blockquote>


## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication](https://docs.tealium.com/about-scim-api/#authentication).

## DELETE operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | URL-parameter | Required | The unique identifier for the user. This value is sent as part of the REST API call. |

### Example cURL request

```bash
curl --location --request DELETE 'https://developer.tealiumapis.com/scim/v2/Users/eb987394-b2b0-4a21-a1d8-7915a91e06b'
```

### Example response

This call returns a 204 status code.

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