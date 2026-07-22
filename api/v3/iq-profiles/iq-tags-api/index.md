---
title: iQ Tags API
description: The iQ Tags API lets you programmatically create, update, and delete tag configurations in an iQ Tag Management profile.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-tags-api/
---
To learn more about this API and available object fields, see [iQ Profiles API](https://docs.tealium.com/iq-profiles-v3-api/) and [iQ Profiles Objects](https://docs.tealium.com/iq-profiles-api-objects/).

## How it works

Use the `PATCH` method to create, update, and delete components in the iQ Profile object.

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

When you use the PATCH method, you are making changes to your profile tags programmatically using a save or save-as. After making changes with the API, you must still log into the application to publish.

### Example cURL request

```bash
curl --location --request PATCH 'https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}' \
  --header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9'  \
  --header 'Content-Type: application/json' \
  --data '
```

## Authentication


<blockquote>
The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.
</blockquote>


To learn about generating a bearer token from the API key, see [Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/).

## Profile fields

Profile tags are JSON objects that contain the following possible fields:

| OBJECT | TYPE | REQUIRED | DESCRIPTION |
| --- | --- | --- | --- |
| `versionTitle` | String | Optional| The title of the resulting saved version.<br>Default with `saveType` set to `saveAs` : `API \| {TIMESTAMP}`<br>Default with `saveType` set to `save`: Existing version title |
| `saveType` | String | Optional | The type of save to perform with the PATCH request: `save` or `saveAs`. Default is `saveAs`. |
| `notes` | String| Required | Additional notes about the publish version. |
| `operationList` | Array | Required| A list of operation objects. For example, multiple tags.|
| `op` | String | Required | The operation to perform: `add`, `replace`, or `remove`. |
| `path` | String | Required| The component type and ID to update, in the format:`/{TYPE}/{ID}`. |
| `value.object` | String | Required| The object type being updated: `variable`, `extension`, `event`, or `tag`.|
|`value.tagID`| String |Required | The unique tag template ID. Use a GET request to retrieve the tag ID. Note that this value is different from the tag UID.|
| `value.status` | String | Optional | The on/off status: `active` or `inactive`. |
| `value.notes` | String | Optional | Notes about the tag. |
| `value.name` | String | Required (for add/replace)| Name of the tag. |
|`value.selectedTargets`| Map &lt;string, Boolean&gt;|  Optional |  An object of environments to publish the component to. `{   "prod" : true\|false,   "qa" : true\|false,   "dev" : true\|false }` <br>Default: All environments set to `true`. |
| `value.configuration` |Map &lt;String, Object&gt; |Optional | A String and Object Map of tag configurations made available by the vendor. Configurations are specific to each tag. For more information, see the documentation for your tag.|
|`value.advancedConfiguration`| Object |Optional |  A set of advanced configurations corresponding to the tag configuration settings. <br>`advConfigBundle` — **True** or **False**<br> `advConfigLoadType` — **True** or **False**<br> `advConfigOptOut` — **True**<br> `advConfigSend`— **True** or **False** <br> `advConfigSrc` — Text field<br> `tagTiming` — **DOM Ready** or **Prioritized** |
|`value.rules`| Object |Optional | The load rules to apply or exclude from the tag.|
|`value.dataMappings`| Map &lt;String, String&gt; |Optional | An object that contains the Tealium IQ variable and its corresponding mapped destination, the variable name, and the data type. You can verify the specific format for the mapped variable triggers in the **Data Mappings** screen in your tag configuration.|
|`value.dataMappings.variable`| String |Optional | The name of the variable to be mapped.|
|`value.dataMappings.type`| String |Optional | The data type of the variable to be mapped. This field supports the following variable types:<br>`ls` - Local storage<br>`ss` - Session storage<br>`udo` - Universal Data Object<br>`qp` - Query string parameter<br>`cp` - Cookie<br>`js_page` - JavaScript  variable<br>`dom` - DOM variable<br>`meta` - Meta data element<br>`static.text` - Static text<br>`static.js` - JavaScript code|
|`value.dataMappings.mappings`| String or Array of Strings |Optional | The mapped destination for the variable.|

### Example request

```json
{
  "versionTitle": "version title",
  "notes": "notes",
  "operationList": [
    {
      "op": "add",
      "path": "/tags",
      "value": {
        "object": "tag",
        "tagId": "7133",
        "status": "active",
        "notes": "adding tag",
        "name": "7133 tag Google Analytics",
        "dataMappings": [
          {
            "variable": "variable_name",
            "type": "udo",
            "mappings": ["a1", "a2"]
          }
        ],
        "selectedTargets": {
          "qa": true,
          "dev": true,
          "prod": true
        },
        "advancedConfiguration": {
          "bundleFlag": true,
          "syncLoadType": false,
          "optout": true,
          "scriptSource": "",
          "sendFlag": false,
          "tagTiming": "Dom Ready"
        },
        "configuration": {
          "tracking_id": "123"
        },
        "rules": {
          "apply": [{"and": [{"or": [{"uid": "2", "type": "loadRule"}]}]}],
          "exclude": [{"and": [{"or": [{"uid": "3", "type": "loadRule"}, {"uid": "2", "type": "loadRule"}]}]}]
        }
      }
    }
  ]
}
```

## PATCH operation parameters

Instead of `POST`, `PUT`, and `DELETE` methods, the `PATCH` method uses the `op` parameter to specify the action to perform.

The `op` parameter supports the following values:

*   `add` - Create the component.
*   `replace` - Update the component.
*   `remove` - Delete the component.

To specify the type and ID of the component, use the `path` parameter. The `path` parameter format is `/{TYPE}/{ID}`.

For example, to add a tag use:

```json
"op" : "add",
"path" : "/tags"
```

To update a specific tag, add the ID to the path:

```json
"op" : "replace",
"path" : "/tags/503"
```

## Create tag

This PATCH method takes a profile object and additional tag fields.

### Example request

```json
{
  "versionTitle": "version title",
  "notes": "notes",
  "operationList": [
    {
      "op": "add",
      "path": "/tags",
      "value": {
        "object": "tag",
        "tagId": "7133",
        "status": "active",
        "notes": "adding tag",
        "name": "7133 tag Google Analytics",
        "dataMappings": [
          {
            "variable": "variable_name",
            "type": "udo",
            "mappings": ["a1", "a2"]
          }
        ],
        "selectedTargets": {
          "qa": true,
          "dev": true,
          "prod": true
        },
        "advancedConfiguration": {
          "bundleFlag": true,
          "syncLoadType": false,
          "optout": true,
          "scriptSource": "",
          "sendFlag": false,
          "tagTiming": "Dom Ready"
        },
        "Configuration": {
          "tracking_id": "123"
        },
        "rules": {
          "apply": [{"and": [{"or": [{"uid": "2", "type": "loadRule"}]}]}],
          "exclude": [{"and": [{"or": [{"uid": "3", "type": "loadRule"}, {"uid": "2", "type": "loadRule"}]}]}]
        }
      }
    }
  ]
}
```

## Update tag

This PATCH method takes a profile object and additional tag fields.

### Example request

```json
{
  "versionTitle": "version title",
  "notes": "notes",
  "operationList": [
    {
      "op": "replace",
      "path": "/tags/21",
      "value": {
        "object": "tag",
        "tagId": "7133",
        "status": "active",
        "notes": "adding tag",
        "name": "Replace name by API Google Analytics",
        "dataMappings": [
          {
            "variable": "variable_name",
            "type": "udo",
            "mappings": ["a1", "a2"]
          }
        ],
        "selectedTargets": {
          "qa": true,
          "dev": true,
          "prod": true
        },
        "advancedConfiguration": {
          "bundleFlag": true,
          "syncLoadType": false,
          "optout": true,
          "scriptSource": "",
          "sendFlag": false,
          "tagTiming": "Dom Ready"
        },
        "Configuration": {
          "tracking_id": "123"
        },
        "rules": {
          "apply": [{"and": [{"or": [{"uid": "2", "type": "loadRule"}]}]}],
          "exclude": [{"and": [{"or": [{"uid": "3", "type": "loadRule"}, {"uid": "2", "type": "loadRule"}]}]}]
        }
      }
    }
  ]
}
```


## Delete tag

This PATCH method takes a profile object and additional tag fields.

### Example request

```json
{
  "versionTitle": "Version 2022.03.22.2108",
  "saveType": "saveAs",
  "notes":"",
  "operationList": [
    {
      "op": "remove",
      "path": "/tags/230",
      "value":{
        "object":"tag"
      }
    }
  ]
}
```
## Error messages

Potential error messages for this endpoint:

| ERROR CODE | ERROR MESSAGE |
| --- | --- |
| 400 | `"Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}"`<br>`"patchProfile.arg2.notes: must not be empty"`|
| 404 | `"Profile not found - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Profile library not found - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Profile (legacy) not found - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Users are currently viewing the same account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Latest version not found - {ACCOUNT} \| profile: {PROFILE}"` |
| 409 | `"Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSION}"` |
| 500 | `"Profile: {PROFILE} inherits from library profile"`<br>`"Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}"`|