---
title: iQ Variables API
description: The iQ Variables API lets you programmatically create, update, and delete variables in an iQ Tag Management profile.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-variables-api/
---

To learn more about this API and available object fields, see [iQ Profiles API](https://docs.tealium.com/iq-profiles-v3-api/) and [iQ Profiles Objects](https://docs.tealium.com/iq-profiles-api-objects/).

## How it works

Use the `PATCH` method to create, update, and delete variables in the iQ Profile object.

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

When you use the PATCH method you are making changes to your profile variables programmatically using a save or save-as. After making changes with the API you must still log into the application to publish.

### Example cURL request

```bash
curl --location --request PATCH 'https://platform.tealiumapis.com/v3/tiq/accounts/{account}/profiles/{profile}' \
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

Profile variables are JSON objects that contain the following possible fields:

|Field| Type| Required| Description|
|---| ---| ---| ---|
|`versionTitle`| String| Optional|  The title of the resulting saved version.<br> Default with `saveType` set to `saveAs` : `API \| {TIMESTAMP}`<br> Default with `saveType` set to `save`: Existing version title |
|`saveType`| String| Optional| The type of save to perform with the PATCH request: `save` or `saveAs`. Default is `saveAs`. |
|`notes`| String| Required| Additional notes about the publish version.|
|`operationList`| Array| Required| A list of operation objects. For example, multiple variables.|
|`op`| String| Required| The operation to perform: `add`, `replace`, or `remove`.|
|`path`| String| Required| The component type and ID to update, in the format:`/variables`.|
|`value.object`| String| Required| The object type being updated: `variable` or `extension`.|
|`value.name`| String| Required (for add/replace)| The variable title.|
|`value.alias`| String| Required| The variable name.|
|`value.type`| String| Required| A prefix representing the variable type.<br> `ls` - Local storage <br> `ss` - Session storage <br> `udo` - Universal Data Object<br> `qp` - Query string parameter<br> `cp` - Cookie<br> `js_page` - JavaScript  variable<br> `meta` - Meta data element<br> `va` - AudienceStream attribute (Read only. This type can be used in other iQ Profile API elements but cannot be created using the API.)|
|`value.notes`| String| Optional| Notes about the variable.|

### Example request

```json
{
  "versionTitle":"Version 2022.03.22.2108",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"add",
      "path":"/variables",
      "value":{
        "object": "variable",
        "name": "page_type",
        "alias": "Page Type",
        "type": "udo",
        "notes":"udo variable"
      }
    }
  ]
}
```

## PATCH operation parameters

Instead of `POST`, `PUT`, and `DELETE` methods, the `PATCH` method uses the `op` parameter to specify the action to perform.

The `op` parameter supports the following values:

* `add` - Create the component.
* `replace` - Update the component.
* `remove` - Delete the component.

To specify the type and ID of the component, use the `path` parameter. The `path` parameter format is `/{TYPE}/{ID}`.

For example, to add a variable use:

```json
"op" : "add",
"path" : "/variables"

```

To update a specific variable, add the ID to the path:

```json
"op" : "replace",
"path" : "/variables/503"
```

## Create variable

This PATCH method takes a profile variable object and additional variable fields.

### Example request

```json
{
  "versionTitle":"Version 2022.03.22.2108",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"add",
      "path":"/variables",
      "value":{
        "object": "variable",
        "name": "page_type",
        "alias": "Page Type",
        "type": "udo",
        "notes":"udo variable"
      }
    }
  ]
}
```

## Update variable

This PATCH method takes a profile variable object and additional variable fields.

### Example request

```json
{
  "versionTitle":"Version 2022.03.22.2108",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"replace",
      "path":"/variables/503",
      "value":{
        "object": "variable",
        "name": "page_type",
        "alias": "Page Type",
        "type": "udo",
        "notes":"udo variable"
      }
    }
  ,]
}
```

## Delete variable

This PATCH method takes a profile variable object and additional variable fields.

### Example request

```json
{
  "versionTitle":"Version 2022.03.22.2108",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"remove",
      "path":"/variables/503",
      "value":{
        "object": "variable"
      }
    }
  ]
}
```

## Error messages

Potential error messages for this endpoint:

|Error Code| Error Message|
|---| ---|
|400|  `"Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}"` <br>  `"Variable validation failed - variableId: {VARIABLE_ID} \| {ACCOUNT} \| profile: {PROFILE}. Cause: {CAUSE}"` <br>  `"patchProfile.arg2.notes: must not be empty"` |
|404|  `"Profile not found - account: {ACCOUNT} \| profile: {PROFILE}"` <br>  `"Profile library not found - account: {ACCOUNT} \| profile: {PROFILE}"`<br>   `"Profile (legacy) not found - account: {ACCOUNT} \| profile: {PROFILE}"` <br>  `"Users are currently viewing the same account: {ACCOUNT} \| profile: {PROFILE}"` <br>  `"Latest version not found - {ACCOUNT} \| profile: {PROFILE}"` |
|409|  `"Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSION}"` |
|500|  `"Profile: {PROFILE} inherits from library profile"`<br>   `"Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}"` <br>  `"Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}"` <br>  `"Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}"` |
