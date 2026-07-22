---
title: PATCH Group API
description: The PATCH Group API updates an existing group in the account.
url: https://docs.tealium.com/api/v3/scim-api/patch-group-api/
---
## How it works

Use the PATCH method to update group membership or rename a custom group:

```bash
PATCH /scim/v2/Groups/{id}
```

PATCH applies to both custom groups and built-in groups for membership changes. Built-in groups cannot be renamed. SCIM cannot change group permissions. Set [group permissions](https://docs.tealium.com/permission-groups/) in the Tealium UI.

## Authentication

The OAuth bearer token is used to authenticate all API calls, not the API key.

For more information, see [Authentication](https://docs.tealium.com/about-scim-api/#authentication).

## PATCH operation parameters

This command takes the following parameters:

| Object | Type | Required | Description |
| --- | --- | --- | --- |
| `id` | URL-parameter | Required | The unique identifier for the user. This value is sent as part of the REST API call.|
| `op` | String | Optional | The operation to perform. Supported values are `add`, `replace`, and `remove`. |
| `path` | String | Optional | The attribute path that specifies the target of the operation. If omitted, the operation is performed on the entire resource. |
| `value` | Array | Optional | An array of user IDs. |

### Example cURL request

#### Microsoft Entra ID

```bash
curl -X PATCH "https://developer.tealiumapis.com/scim/v2/Groups/eb987394-b2b0-4a21-a1d8-7915a91e06b" \
-H "Content-Type: application/scim+json" \
-H "Accept: application/scim+json" \
-d '{
    "schemas": [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"
    ],
    "Operations": [
        {
            "op": "replace",
            "path": "members",
            "value": [
               {
                   "value": "cb300cb6-9702-45a9-a909-f8b7c972ab7e"
               }
           ]
        }
    ]
}'
```

#### Okta

```bash
curl -X PATCH "https://developer.tealiumapis.com/scim/v2/Groups/eb987394-b2b0-4a21-a1d8-7915a91e06b" \
-H "Content-Type: application/scim+json" \
-H "Accept: application/scim+json" \
-d '{
    "schemas": [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"
    ],
    "Operations": [
        {
            "op": "replace",
            "value": {
                "members": [
                   {
                       "value": "cb300cb6-9702-45a9-a909-f8b7c972ab7e"
                   }
               ]
            }
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
    "id": "eb987394-b2b0-4a21-a1d8-7915a91e06b",
    "displayName": "example group",
    "members": [
        {
            "value": "cb300cb6-9702-45a9-a909-f8b7c972ab7e",
            "type": "User",
            "display": "exampleuser@example.onmicrosoft.com",
            "$ref": "/scim/v2/Users/cb300cb6-9702-45a9-a909-f8b7c972ab7e"
        },
        {
            "value": "3bfa1b1f-5f1f-45c1-bcb8-25a70b1a4bb2",
            "type": "User",
            "display": "exampleuser@okta.com",
            "$ref": "/scim/v2/Users/3bfa1b1f-5f1f-45c1-bcb8-25a70b1a4bb2"
        }
    ],
    "meta": {
        "resourceType": "Group",
        "location": "/scim/v2/Groups/7987a965-411b-4816-b485-29fd81ca81ac"
    }
}
```


## Error messages

Potential error messages for this endpoint:

| Error code | Error message |
| --- | --- |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "User payload is required."}` |
| 400 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "400","scimType": "invalidValue","detail": "Cannot rename built-in group 'Account Admins'. Built-in group names are immutable."}`|
| 401 | `{"returnCode" : 1401 , "message" : "Authentication failed."}` |
| 403 | `{"schemas": [ "urn:ietf:params:scim:api:messages:2.0:Error"],"status": "403","scimType": null,"detail": "Missing X-Tealium-Account header."}` |
| 404 |` {"schemas":["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404", "scimType": "noTarget", "detail":"Group uuid 1987a965-411b-4816-b485-29fd81ca81ac not found in account testaccount"}`|
| 404 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "404","scimType": "noTarget","detail": "User UUID {uuid} not found in account {ACCOUNT}."}`|
| 405 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"], "status": "405", "scimType": "invalidMethod", "detail": "Method is not allowed on this endpoint. Allowed methods: GET, POST."}`|
| 500 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "500","scimType": "internalServerError","detail": "Error processing json for extension - account {ACCOUNT}"}`|
| 501 | `{"schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],"status": "501","scimType": "unsupported","detail": "The operation {operation} is not supported."}`|