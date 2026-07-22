---
title: DELETE Group API
description: The DELETE Group API removes an existing group from the account.
url: https://docs.tealium.com/api/v3/scim-api/delete-group-api/
---
## How it works

Use the DELETE method to delete a custom group:

```bash
DELETE /scim/v2/Groups/{id}
```

Built-in groups cannot be deleted.

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication](https://docs.tealium.com/about-scim-api/#authentication).

## DELETE operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | URL-parameter | Required | The unique identifier for the group. This value is sent as part of the REST API call. |


<blockquote>
Built-in groups (Standard User, Account Admins, User Admins, Privacy Admins, Technical Admins, Profile Admins) cannot be deleted. Attempts to delete built-in groups return an HTTP 400 error. For more information, see [Built-in group protection](https://docs.tealium.com/about-scim-api/#built-in-group-protection).
</blockquote>


### Example cURL request

```bash
curl --location --request DELETE 'https://developer.tealiumapis.com/scim/v2/Groups/9d379d2c-2601-42d8-842c-579dc3c58612' \
--header 'Accept: application/scim+json' \
--header 'Authorization: ••••••' \
--header 'Cookie: JSESSIONID=0f9b099a-1284-4e41-89ac-38f72bbff66c'

```

### Example response

This call returns a 204 status code.

### Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "Invalid ID format."}` |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "Group {uuid} is a built-in group which is ineligible for deletion."}`|
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 404 |` {"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "Group not found in account {ACCOUNT}."}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "405","scimType": "invalidMethod","detail": "Method is not allowed on this endpoint. Allowed methods: GET, POST."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|

