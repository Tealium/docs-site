---
title: iQ Load Rules API
description: The iQ Variables API lets you programmatically create, update, and delete load rules in an iQ Tag Management profile.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-load-rules-api/
---
To learn more about this API and available object fields, see [iQ Profiles API](https://docs.tealium.com/iq-profiles-v3-api/) and [iQ Profiles Objects](https://docs.tealium.com/iq-profiles-api-objects/).

## How it works

Use the `PATCH` method to create, update, and delete load rules in the iQ Profile object.

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

When you use the PATCH method you are making changes to your profile load rules programmatically using a save or save-as. After making changes with the API you must still log into the application to publish.

### Example cURL request

```bash
curl --location --request PATCH 'https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}' \
  --header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9' \
  --header 'Content-Type: application/json' \
  --data '
```

## Authentication


<blockquote>
The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.
</blockquote>


To learn about generating a bearer token from the API key, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/).

## Profile fields

Profile load rules are JSON objects that contain the following possible fields:

|FIELD| TYPE| REQUIRED| DESCRIPTION|
|---| ---| ---| ---|
|`versionTitle`| String| Optional|  The title of the resulting saved version.<br> Default with `saveType` set to `saveAs` : `API \| {TIMESTAMP}`<br> Default with `saveType` set to `save`: Existing version title |
|`saveType`| String| Optional| The type of save to perform with the PATCH request: `save` or `saveAs`. Default is `saveAs`. |
|`notes`| String| Required| Additional notes about the publish version.|
|`op`| String| Required| The operation to perform: `add`, `replace`, or `remove`.|
|`path`| String| Required| The component type and ID to update, in the format:`/loadRules`.|
|`value.object`| String| Required| The object type being updated: `variable`, `loadRule`, or `extension`.|
|`value.name`| String| Required (for add/replace)| The name of load rule.|
|`value.status`| String| Required| The on/off status: `active` or `inactive`.|
|`value.notes`| String| Optional| Notes about the load rule.|
|`value.startDate`| Date| Optional if `value.endDate` is empty. | For scheduled load rules, the start date. Date format must be `yyyyMMddHHmm`.|
|`value.endDate`| Date| Optional| For scheduled load rules, the end date. Date format must be `yyyyMMddHHmm`.|
|`value.conditions`| Array[object]| Required|  An array of objects that include variable name, operator, and value. Each object within an array is associated by an `and`operator while each array within the array is associated by an `or` operator. The following operators do not accept a value:<br>`is defined`<br> `is badge assigned`<br> `is badge not assigned`<br> `is not defined`<br> `is not populated` |

### Example request

```json
{
  "versionTitle": "Adding Rule",
  "saveType": "saveAs",
  "notes": "version notes here", 
  "operationList": [
    {
      "op": "add",
      "path": "/loadRules",
      "value":{
        "object": "loadRule",
        "name": "new rule API Dom variable",
        "status": "active",
        "notes": "Load Rule notes here",
        "startDate": "202202020000",
        "endDate": "202202020000",
        "conditions": [
          [
            {
              "variable": "udo.new_name",
              "operator": "does_not_equal",
              "value": 10
            }
          ]
        ]   
      }
    }
  ] 
}
```

## PATCH Operation Parameters

Instead of `POST`, `PUT`, and `DELETE` methods, the `PATCH` method uses the `op` parameter to specify the action to perform.

The `op` parameter supports the following values:

* `add` - Create the component.
* `replace` - Update the component.
* `remove` - Delete the component.

To specify the type and ID of the component, use the `path` parameter. The `path` parameter format is `/{TYPE}/{ID}`.

For example, to add a load rule use:

```json
"op" : "add",
"path" : "/loadRules"
```

To update a specific load rule, add the ID to the path:

```json
"op" : "replace",
"path" : "/loadRules/503"
```

## Create load rule

This PATCH method takes a profile load rule object and additional load rule fields.

### Example request

```json
{
  "versionTitle": "Adding Rule",
  "saveType": "saveAs",
  "notes": "version notes here", 
  "operationList": [
    {
      "op": "add",
      "path": "/loadRules",
      "value":{
        "object": "loadRule",
        "name": "new rule API Dom variable",
        "status": "active",
        "notes": "Load Rule notes here",
        "startDate": "202202020000",
        "endDate": "202202020000",
        "conditions": [
          [
            {
              "variable": "udo.new_name",
              "operator": "does_not_equal",
              "value": 10
            }
          ]
        ]   
      }
    }
  ] 
}
```

## Update load rule

This PATCH method takes a profile load rule object and additional load rule fields.

### Example request

```json
{
  "versionTitle": "Adding Rule",
  "saveType": "saveAs",
  "notes": "version notes here", 
  "operationList": [
    {
      "op": "replace",
      "path": "/loadRules/49",
      "value":{
        "object": "loadRule",
        "name": "new rule API Dom variable",
        "status": "active",
        "notes": "Load Rule notes here",
        "startDate": "202202020000",
        "endDate": "202202020000",
        "conditions": [
          [
            {
              "variable": "udo.new_name",
              "operator": "does_not_equal",
              "value": 10
            }
          ]
        ]   
      }
    }
  ] 
}
```

## Delete load rule

This PATCH method takes a profile load rules object and additional load rules fields.

### Example request

```json
{
  "versionTitle": "Adding Rule",
  "saveType": "saveAs",
  "notes": "version notes here", 
  "operationList": [
    {
      "op": "remove",
      "path": "/loadRules/49",
      "value":{
        "object": "loadRule"
      }
    }
  ]
}
```

## Error messages

Potential error messages for this endpoint:

|ERROR CODE| ERROR MESSAGE|
|---| ---|
|400|  `"Validate patch request failed due to %s"`<br>   `"Cannot set tag scope extension with tags that do not exist, id: {ID} - {ACCOUNT} \| profile: {PROFILE}"` <br>  `"Cannot set extension scope to sync if the setting is not turned on - {ACCOUNT} \| profile: {PROFILE}"`<br>   `"Error in getting next extension id - {ACCOUNT} \| profile: {PROFILE}"`<br>   `"Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}"` <br>  `"Not Supported"` <br> `"patchProfile.arg2.notes: must not be empty"` |
| 404 |    `"Account: {ACCOUNT}, profile: {PROFILE} not found"` |
| 409 |  `"Users are currently viewing the same account: {ACCOUNT} profile: {PROFILE}"` <br> `Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSIONS}` |
|500|  `"An error occurred"` <br>  `"Profile: {PROFILE} inherits from library profile"`<br>   `"Unable to invoke request: unknown host, see logs for more detail."`<br>  `"Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}"`<br>   `"Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}"`<br>   `"Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}"` |
