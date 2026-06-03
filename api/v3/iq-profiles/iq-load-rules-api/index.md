---
title: iQ Load Rules API
description: The iQ Variables API lets you programmatically create, update, and delete load rules in an iQ Tag Management profile.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-load-rules-api/
---
To learn more about this API and available object fields, see [iQ Profiles API]() and [iQ Profiles Objects]().

## How it works

Use the `PATCH` method to create, update, and delete load rules in the iQ Profile object.

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

When you use the PATCH method you are making changes to your profile load rules programmatically using a save or save-as. After making changes with the API you must still log into the application to publish.

### Example cURL request

```bash
curl --location --request PATCH &#39;https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}&#39; \
  --header &#39;Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9&#39; \
  --header &#39;Content-Type: application/json&#39; \
  --data &#39;
```

## Authentication

The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.

To learn about generating a bearer token from the API key, see [Authentication]().

## Profile fields

Profile load rules are JSON objects that contain the following possible fields:

|FIELD| TYPE| REQUIRED| DESCRIPTION|
|---| ---| ---| ---|
|`versionTitle`| String| Optional|  The title of the resulting saved version.&lt;br&gt; Default with `saveType` set to `saveAs` : `API \| {TIMESTAMP}`&lt;br&gt; Default with `saveType` set to `save`: Existing version title |
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
|`value.conditions`| Array[object]| Required|  An array of objects that include variable name, operator, and value. Each object within an array is associated by an `and`operator while each array within the array is associated by an `or` operator. The following operators do not accept a value:&lt;br&gt;`is defined`&lt;br&gt; `is badge assigned`&lt;br&gt; `is badge not assigned`&lt;br&gt; `is not defined`&lt;br&gt; `is not populated` |

### Example request

```json
{
  &#34;versionTitle&#34;: &#34;Adding Rule&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;, 
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;add&#34;,
      &#34;path&#34;: &#34;/loadRules&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;loadRule&#34;,
        &#34;name&#34;: &#34;new rule API Dom variable&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;notes&#34;: &#34;Load Rule notes here&#34;,
        &#34;startDate&#34;: &#34;202202020000&#34;,
        &#34;endDate&#34;: &#34;202202020000&#34;,
        &#34;conditions&#34;: [
          [
            {
              &#34;variable&#34;: &#34;udo.new_name&#34;,
              &#34;operator&#34;: &#34;does_not_equal&#34;,
              &#34;value&#34;: 10
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
&#34;op&#34; : &#34;add&#34;,
&#34;path&#34; : &#34;/loadRules&#34;
```

To update a specific load rule, add the ID to the path:

```json
&#34;op&#34; : &#34;replace&#34;,
&#34;path&#34; : &#34;/loadRules/503&#34;
```

## Create load rule

This PATCH method takes a profile load rule object and additional load rule fields.

### Example request

```json
{
  &#34;versionTitle&#34;: &#34;Adding Rule&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;, 
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;add&#34;,
      &#34;path&#34;: &#34;/loadRules&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;loadRule&#34;,
        &#34;name&#34;: &#34;new rule API Dom variable&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;notes&#34;: &#34;Load Rule notes here&#34;,
        &#34;startDate&#34;: &#34;202202020000&#34;,
        &#34;endDate&#34;: &#34;202202020000&#34;,
        &#34;conditions&#34;: [
          [
            {
              &#34;variable&#34;: &#34;udo.new_name&#34;,
              &#34;operator&#34;: &#34;does_not_equal&#34;,
              &#34;value&#34;: 10
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
  &#34;versionTitle&#34;: &#34;Adding Rule&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;, 
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;replace&#34;,
      &#34;path&#34;: &#34;/loadRules/49&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;loadRule&#34;,
        &#34;name&#34;: &#34;new rule API Dom variable&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;notes&#34;: &#34;Load Rule notes here&#34;,
        &#34;startDate&#34;: &#34;202202020000&#34;,
        &#34;endDate&#34;: &#34;202202020000&#34;,
        &#34;conditions&#34;: [
          [
            {
              &#34;variable&#34;: &#34;udo.new_name&#34;,
              &#34;operator&#34;: &#34;does_not_equal&#34;,
              &#34;value&#34;: 10
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
  &#34;versionTitle&#34;: &#34;Adding Rule&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;, 
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;remove&#34;,
      &#34;path&#34;: &#34;/loadRules/49&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;loadRule&#34;
      }
    }
  ]
}
```

## Error messages

Potential error messages for this endpoint:

|ERROR CODE| ERROR MESSAGE|
|---| ---|
|400|  `&#34;Validate patch request failed due to %s&#34;`&lt;br&gt;   `&#34;Cannot set tag scope extension with tags that do not exist, id: {ID} - {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;  `&#34;Cannot set extension scope to sync if the setting is not turned on - {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;   `&#34;Error in getting next extension id - {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;   `&#34;Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;  `&#34;Not Supported&#34;` &lt;br&gt; `&#34;patchProfile.arg2.notes: must not be empty&#34;` |
| 404 |    `&#34;Account: {ACCOUNT}, profile: {PROFILE} not found&#34;` |
| 409 |  `&#34;Users are currently viewing the same account: {ACCOUNT} profile: {PROFILE}&#34;` &lt;br&gt; `Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSIONS}` |
|500|  `&#34;An error occurred&#34;` &lt;br&gt;  `&#34;Profile: {PROFILE} inherits from library profile&#34;`&lt;br&gt;   `&#34;Unable to invoke request: unknown host, see logs for more detail.&#34;`&lt;br&gt;  `&#34;Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;   `&#34;Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;   `&#34;Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}&#34;` |
