---
title: iQ JavaScript Extension API
description: The iQ JavaScript Extension API lets you programmatically create, update, and delete JavaScript Code extensions in an Tag Management profile.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-javascript-extension-api/
---
To learn more about this API and available object fields, see [iQ Profiles API](https://docs.tealium.com/iq-profiles-v3-api/) and [iQ Profiles Objects](https://docs.tealium.com/iq-profiles-api-objects/).

## How it works

iQ Profiles uses JSON objects to retrieve data from a Tag Management account profile and update [JavaScript Code extensions](https://docs.tealium.com/javascript-code-extension/). Use this endpoint for custom code deployments through your Tag Management profiles.


<blockquote>
Only [JavaScript Code extensions](https://docs.tealium.com/javascript-code-extension/) are supported. You cannot manage Advanced Javascript Code extensions or any other type of extension with this endpoint.
</blockquote>


Use the `PATCH` method to create, update, and delete components in the iQ Profile object.

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

When you use the PATCH method you are making changes to your profile configuration programmatically using a save or save-as. After making changes with the API you must still log into the application to publish.

### Example cURL Request

```bash
curl --location --request PATCH 'https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}' \
--header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9' \
--header 'Content-Type: application/json' \
--data-raw
```

## Authentication


<blockquote>
The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.
</blockquote>


To learn about generating a bearer token from the API key, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/).

## Profile fields

Profiles are JSON objects that contain the following possible fields:

|Field| Type| Required| Description|
|---| ---| ---| ---|
|`versionTitle`| String| Optional|  The title of the resulting saved version.<br> Default with `saveType` set to `saveAs` : `API \| {TIMESTAMP}`<br> Default with `saveType` set to `save`: Existing version title. |
|`saveType`| String| Optional| The type of save to perform with the PATCH request: `save` or `saveAs`. Default is `saveAs`. |
|`notes`| String| Required| Additional notes about the publish version.|
|`operationList`| Array| Required| A list of operation objects. For example, multiple JavaScript Code extensions.|
|`op`| String| Required| The operation to perform: `add`, `replace`, or `remove`.|
|`path`| String| Required| The component type to add or the type and ID to update, in the format:`/{TYPE}/{ID}`. For example, `/extensions/12` or `/extensions`.|
|`value.object`| String| Required| The object type being updated: `variable` or `extension`.|
|`value.name`| String| Required (for add/replace)| Title of the component.|
|`value.notes`| String| Optional| Additional notes about the component.|
|`value.type`| String| Required<br> (for extensions)| The type of extension to add. Only [JavaScript Code extensions](https://docs.tealium.com/javascript-code-extension/) are supported. This value must be `Javascript Code`.|
|`value.scope`| String| Optional|  The name of the extension scope or, for tag-scoped extensions, a comma-separated list of tag IDs.<br> `Before Load Rules`<br> `After Load Rules`<br> `DOM Ready`<br> `Tag Scoped Extensions`<br> `After Tag Extensions` |
|`value.occurrence`| String| Optional|  Determines the number of times the JavaScript code extension runs per page load. Values: `Run Once` or `Run Always`. Default: `Run Always`. |
|`value.status`| String| Optional| The on/off status of the component: `active` or `inactive`.<br> Default: `active`|
|`value.selectedTargets`| Map &lt;string, Boolean&gt;|  Optional |  An object of environments to publish the component to:<br> `{   "prod" : true\|false,   "qa" : true\|false,   "dev" : true\|false }` Default: All environments set to `true`. |
|`value.conditions`| Array[object]| Optional | The conditions object for the extension that includes the variable, operator, and value. If you do not include conditions in your PATCH request, but they exist in the profile, the request will be seen as a `remove` action.|
| `value.configuration` | Array[object]|  Required |  The configuration object for the component. This object varies for each type of component. Only one object is allowed in this array field. For example: `{   name: “code”   value: “JSON-escaped JavaScript code here” }` |

### Example request

```json
{
  "versionTitle":"Version 2023.09.19.1127",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"add",
      "path":"/extensions",
      "value":{
        "object": "extension",
        "name": "My extension",
        "notes": "extension notes here",
        "type": "Javascript Code",
        "scope": "After Load Rules",
        "occurence": "Run Always",
        "status": "active",
        "selectedTargets":{
          "qa": true,
          "dev": true,
          "prod": true
        },
        "conditions": [
          [
            {
              "variable": "va.badges.30",
              "operator": "is_badge_assigned",
              "value": ""
            }
          ]
        ],
        "configuration": [
          {
            "name": "code",
            "value": "b.page_name ||= \"Generic Page\"!!;"
          }
        ]
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

For example, to add an extension use:

```json
"op" : "add",
"path" : "/extensions"

```

To update a specific extension, add the ID to the path:

```json
"op" : "replace",
"path" : "/extensions/503"
```

## Create extension

This PATCH method takes a profile object and additional extension fields.

### Example request

```json
{
  "versionTitle":"Version 2023.09.19.1127",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"add",
      "path":"/extensions",
      "value":{
        "object": "extension",
        "name": "Javscript Code extension",
        "notes": "extension notes here",
        "type": "Javascript Code",
        "scope": "After Load Rules",
        "occurence": "Run Always",
        "status": "active",
        "selectedTargets":{
          "qa": true,
          "dev": true,
          "prod": true
        },
        "configuration":[
          {
           "name": "code",
            "value": "b.page_name ||= \"Generic Page\"!!;"
          }
        ]
      }
    }
  ]
}
```

## Update extension

This PATCH method takes a profile object and additional extension fields.

### Example request

```json
{
  "versionTitle":"Version 2023.09.19.1127",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"replace",
      "path":"/extensions",
      "value":{
        "object": "extension/86",
        "name": "Javscript Code extension",
        "notes": "extension notes here",
        "type": "Javascript Code",
        "scope": "After Load Rules",
        "occurence": "Run Always",
        "status": "active",
        "selectedTargets":{
          "qa": true,
          "dev": true,
          "prod": true
        },
        "configuration":[
          {
           "name": "code",
            "value": "b.page_name ||= \"Generic Page\"!!;"
          }
        ]
      }
    }
  ]
}
```

## Delete extension

This PATCH method takes a profile object and additional extension fields.

### Example request

```json
{
  "versionTitle":"Version 2023.09.19.1127",
  "saveType": "saveAs",
  "notes": "version notes here",
  "operationList":[
    {
      "op":"remove",
      "path":"/extensions/86",
      "value":{
        "object": "extension",
      }
    }
  ]
}
```

## Error messages

Potential error messages for this endpoint:

|Error Code| Error Message|
|---| ---|
|400| `"Validate patch request failed due to unsupported extension type {TYPE}"`<br>    `"Unsupported extension type {TYPE}"`<br>    `"Validate patch request failed due to %s"`<br>    `"Cannot set tag scope extension with tags that do not exist, id: {ID} - {ACCOUNT} \| profile: {PROFILE}"`<br>    `"Cannot set extension scope to sync if the setting is not turned on - {ACCOUNT} \| profile: {PROFILE}"` <br>   `"Error in getting next extension id - {ACCOUNT} \| profile: {PROFILE}"`<br>    `"Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}"` <br>  `"patchProfile.arg2.notes: must not be empty"` |
| 404 |  `"Extension validation failed - extensionId: {ID} \| account: {ACCOUNT} \| profile: {PROFILE}. Cause: not found"` <br>    `"Extension ID {ID} not found in the profile {PROFILE}"`<br>    `"Account: {ACCOUNT}, profile: {PROFILE} not found"` |
| 409 |  `"Conflict with profile extension: _id: {ID}, extType: {EXT_TYPE}, title: {TITLE}"` <br>  `"Users are currently viewing the same account: {ACCOUNT} profile: {PROFILE}"`<br>   `"Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSIONS}"`  |
|500|  `"An error occurred"` <br>   `"Profile: {PROFILE} inherits from library profile"`<br>    `"Unable to invoke request: unknown host, see logs for more detail."`<br>    `"Error processing json for extension - account: {ACCOUNT} \| profile: {PROFILE}"` <br>   `"Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}"`<br>    `"Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}"` <br>   `"Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}"` |
