---
title: iQ Variables API
description: The iQ Variables API lets you programmatically create, update, and delete variables in an iQ Tag Management profile.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-variables-api/
---

To learn more about this API and available object fields, see [iQ Profiles API]() and [iQ Profiles Objects]().

## How it works

Use the `PATCH` method to create, update, and delete variables in the iQ Profile object.

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

When you use the PATCH method you are making changes to your profile variables programmatically using a save or save-as. After making changes with the API you must still log into the application to publish.

### Example cURL request

```bash
curl --location --request PATCH &#39;https://platform.tealiumapis.com/v3/tiq/accounts/{account}/profiles/{profile}&#39; \
  --header &#39;Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9&#39; \
  --header &#39;Content-Type: application/json&#39; \
  --data &#39;
```

## Authentication

The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.

To learn about generating a bearer token from the API key, see [Authentication]().

## Profile fields

Profile variables are JSON objects that contain the following possible fields:

|Field| Type| Required| Description|
|---| ---| ---| ---|
|`versionTitle`| String| Optional|  The title of the resulting saved version.&lt;br&gt; Default with `saveType` set to `saveAs` : `API \| {TIMESTAMP}`&lt;br&gt; Default with `saveType` set to `save`: Existing version title |
|`saveType`| String| Optional| The type of save to perform with the PATCH request: `save` or `saveAs`. Default is `saveAs`. |
|`notes`| String| Required| Additional notes about the publish version.|
|`operationList`| Array| Required| A list of operation objects. For example, multiple variables.|
|`op`| String| Required| The operation to perform: `add`, `replace`, or `remove`.|
|`path`| String| Required| The component type and ID to update, in the format:`/variables`.|
|`value.object`| String| Required| The object type being updated: `variable` or `extension`.|
|`value.name`| String| Required (for add/replace)| The variable title.|
|`value.alias`| String| Required| The variable name.|
|`value.type`| String| Required| A prefix representing the variable type.&lt;br&gt; `ls` - Local storage &lt;br&gt; `ss` - Session storage &lt;br&gt; `udo` - Universal Data Object&lt;br&gt; `qp` - Query string parameter&lt;br&gt; `cp` - Cookie&lt;br&gt; `js_page` - JavaScript  variable&lt;br&gt; `meta` - Meta data element&lt;br&gt; `va` - AudienceStream attribute (Read only. This type can be used in other iQ Profile API elements but cannot be created using the API.)|
|`value.notes`| String| Optional| Notes about the variable.|

### Example request

```json
{
  &#34;versionTitle&#34;:&#34;Version 2022.03.22.2108&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;add&#34;,
      &#34;path&#34;:&#34;/variables&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;variable&#34;,
        &#34;name&#34;: &#34;page_type&#34;,
        &#34;alias&#34;: &#34;Page Type&#34;,
        &#34;type&#34;: &#34;udo&#34;,
        &#34;notes&#34;:&#34;udo variable&#34;
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
&#34;op&#34; : &#34;add&#34;,
&#34;path&#34; : &#34;/variables&#34;

```

To update a specific variable, add the ID to the path:

```json
&#34;op&#34; : &#34;replace&#34;,
&#34;path&#34; : &#34;/variables/503&#34;
```

## Create variable

This PATCH method takes a profile variable object and additional variable fields.

### Example request

```json
{
  &#34;versionTitle&#34;:&#34;Version 2022.03.22.2108&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;add&#34;,
      &#34;path&#34;:&#34;/variables&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;variable&#34;,
        &#34;name&#34;: &#34;page_type&#34;,
        &#34;alias&#34;: &#34;Page Type&#34;,
        &#34;type&#34;: &#34;udo&#34;,
        &#34;notes&#34;:&#34;udo variable&#34;
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
  &#34;versionTitle&#34;:&#34;Version 2022.03.22.2108&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;replace&#34;,
      &#34;path&#34;:&#34;/variables/503&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;variable&#34;,
        &#34;name&#34;: &#34;page_type&#34;,
        &#34;alias&#34;: &#34;Page Type&#34;,
        &#34;type&#34;: &#34;udo&#34;,
        &#34;notes&#34;:&#34;udo variable&#34;
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
  &#34;versionTitle&#34;:&#34;Version 2022.03.22.2108&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;remove&#34;,
      &#34;path&#34;:&#34;/variables/503&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;variable&#34;
      }
    }
  ]
}
```

## Error messages

Potential error messages for this endpoint:

|Error Code| Error Message|
|---| ---|
|400|  `&#34;Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;  `&#34;Variable validation failed - variableId: {VARIABLE_ID} \| {ACCOUNT} \| profile: {PROFILE}. Cause: {CAUSE}&#34;` &lt;br&gt;  `&#34;patchProfile.arg2.notes: must not be empty&#34;` |
|404|  `&#34;Profile not found - account: {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;  `&#34;Profile library not found - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;   `&#34;Profile (legacy) not found - account: {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;  `&#34;Users are currently viewing the same account: {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;  `&#34;Latest version not found - {ACCOUNT} \| profile: {PROFILE}&#34;` |
|409|  `&#34;Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSION}&#34;` |
|500|  `&#34;Profile: {PROFILE} inherits from library profile&#34;`&lt;br&gt;   `&#34;Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;  `&#34;Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;  `&#34;Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}&#34;` |
