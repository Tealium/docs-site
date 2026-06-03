---
title: iQ JavaScript Extension API
description: The iQ JavaScript Extension API lets you programmatically create, update, and delete JavaScript Code extensions in an Tag Management profile.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-javascript-extension-api/
---
To learn more about this API and available object fields, see [iQ Profiles API]() and [iQ Profiles Objects]().

## How it works

iQ Profiles uses JSON objects to retrieve data from a Tag Management account profile and update [JavaScript Code extensions](). Use this endpoint for custom code deployments through your Tag Management profiles.

Only [JavaScript Code extensions]() are supported. You cannot manage Advanced Javascript Code extensions or any other type of extension with this endpoint.

Use the `PATCH` method to create, update, and delete components in the iQ Profile object.

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

When you use the PATCH method you are making changes to your profile configuration programmatically using a save or save-as. After making changes with the API you must still log into the application to publish.

### Example cURL Request

```bash
curl --location --request PATCH &#39;https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}&#39; \
--header &#39;Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9&#39; \
--header &#39;Content-Type: application/json&#39; \
--data-raw
```

## Authentication

The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.

To learn about generating a bearer token from the API key, see [Authentication]().

## Profile fields

Profiles are JSON objects that contain the following possible fields:

|Field| Type| Required| Description|
|---| ---| ---| ---|
|`versionTitle`| String| Optional|  The title of the resulting saved version.&lt;br&gt; Default with `saveType` set to `saveAs` : `API \| {TIMESTAMP}`&lt;br&gt; Default with `saveType` set to `save`: Existing version title. |
|`saveType`| String| Optional| The type of save to perform with the PATCH request: `save` or `saveAs`. Default is `saveAs`. |
|`notes`| String| Required| Additional notes about the publish version.|
|`operationList`| Array| Required| A list of operation objects. For example, multiple JavaScript Code extensions.|
|`op`| String| Required| The operation to perform: `add`, `replace`, or `remove`.|
|`path`| String| Required| The component type to add or the type and ID to update, in the format:`/{TYPE}/{ID}`. For example, `/extensions/12` or `/extensions`.|
|`value.object`| String| Required| The object type being updated: `variable` or `extension`.|
|`value.name`| String| Required (for add/replace)| Title of the component.|
|`value.notes`| String| Optional| Additional notes about the component.|
|`value.type`| String| Required&lt;br&gt; (for extensions)| The type of extension to add. Only [JavaScript Code extensions]() are supported. This value must be `Javascript Code`.|
|`value.scope`| String| Optional|  The name of the extension scope or, for tag-scoped extensions, a comma-separated list of tag IDs.&lt;br&gt; `Before Load Rules`&lt;br&gt; `After Load Rules`&lt;br&gt; `DOM Ready`&lt;br&gt; `Tag Scoped Extensions`&lt;br&gt; `After Tag Extensions` |
|`value.occurrence`| String| Optional|  Determines the number of times the JavaScript code extension runs per page load. Values: `Run Once` or `Run Always`. Default: `Run Always`. |
|`value.status`| String| Optional| The on/off status of the component: `active` or `inactive`.&lt;br&gt; Default: `active`|
|`value.selectedTargets`| Map &amp;lt;string, Boolean&amp;gt;|  Optional |  An object of environments to publish the component to:&lt;br&gt; `{   &#34;prod&#34; : true\|false,   &#34;qa&#34; : true\|false,   &#34;dev&#34; : true\|false }` Default: All environments set to `true`. |
|`value.conditions`| Array[object]| Optional | The conditions object for the extension that includes the variable, operator, and value. If you do not include conditions in your PATCH request, but they exist in the profile, the request will be seen as a `remove` action.|
| `value.configuration` | Array[object]|  Required |  The configuration object for the component. This object varies for each type of component. Only one object is allowed in this array field. For example: `{   name: “code”   value: “JSON-escaped JavaScript code here” }` |

### Example request

```json
{
  &#34;versionTitle&#34;:&#34;Version 2023.09.19.1127&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;add&#34;,
      &#34;path&#34;:&#34;/extensions&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;extension&#34;,
        &#34;name&#34;: &#34;My extension&#34;,
        &#34;notes&#34;: &#34;extension notes here&#34;,
        &#34;type&#34;: &#34;Javascript Code&#34;,
        &#34;scope&#34;: &#34;After Load Rules&#34;,
        &#34;occurence&#34;: &#34;Run Always&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;selectedTargets&#34;:{
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;conditions&#34;: [
          [
            {
              &#34;variable&#34;: &#34;va.badges.30&#34;,
              &#34;operator&#34;: &#34;is_badge_assigned&#34;,
              &#34;value&#34;: &#34;&#34;
            }
          ]
        ],
        &#34;configuration&#34;: [
          {
            &#34;name&#34;: &#34;code&#34;,
            &#34;value&#34;: &#34;b.page_name ||= \&#34;Generic Page\&#34;!!;&#34;
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
&#34;op&#34; : &#34;add&#34;,
&#34;path&#34; : &#34;/extensions&#34;

```

To update a specific extension, add the ID to the path:

```json
&#34;op&#34; : &#34;replace&#34;,
&#34;path&#34; : &#34;/extensions/503&#34;
```

## Create extension

This PATCH method takes a profile object and additional extension fields.

### Example request

```json
{
  &#34;versionTitle&#34;:&#34;Version 2023.09.19.1127&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;add&#34;,
      &#34;path&#34;:&#34;/extensions&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;extension&#34;,
        &#34;name&#34;: &#34;Javscript Code extension&#34;,
        &#34;notes&#34;: &#34;extension notes here&#34;,
        &#34;type&#34;: &#34;Javascript Code&#34;,
        &#34;scope&#34;: &#34;After Load Rules&#34;,
        &#34;occurence&#34;: &#34;Run Always&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;selectedTargets&#34;:{
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;configuration&#34;:[
          {
           &#34;name&#34;: &#34;code&#34;,
            &#34;value&#34;: &#34;b.page_name ||= \&#34;Generic Page\&#34;!!;&#34;
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
  &#34;versionTitle&#34;:&#34;Version 2023.09.19.1127&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;replace&#34;,
      &#34;path&#34;:&#34;/extensions&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;extension/86&#34;,
        &#34;name&#34;: &#34;Javscript Code extension&#34;,
        &#34;notes&#34;: &#34;extension notes here&#34;,
        &#34;type&#34;: &#34;Javascript Code&#34;,
        &#34;scope&#34;: &#34;After Load Rules&#34;,
        &#34;occurence&#34;: &#34;Run Always&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;selectedTargets&#34;:{
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;configuration&#34;:[
          {
           &#34;name&#34;: &#34;code&#34;,
            &#34;value&#34;: &#34;b.page_name ||= \&#34;Generic Page\&#34;!!;&#34;
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
  &#34;versionTitle&#34;:&#34;Version 2023.09.19.1127&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes here&#34;,
  &#34;operationList&#34;:[
    {
      &#34;op&#34;:&#34;remove&#34;,
      &#34;path&#34;:&#34;/extensions/86&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;extension&#34;,
      }
    }
  ]
}
```

## Error messages

Potential error messages for this endpoint:

|Error Code| Error Message|
|---| ---|
|400| `&#34;Validate patch request failed due to unsupported extension type {TYPE}&#34;`&lt;br&gt;    `&#34;Unsupported extension type {TYPE}&#34;`&lt;br&gt;    `&#34;Validate patch request failed due to %s&#34;`&lt;br&gt;    `&#34;Cannot set tag scope extension with tags that do not exist, id: {ID} - {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;    `&#34;Cannot set extension scope to sync if the setting is not turned on - {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;   `&#34;Error in getting next extension id - {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;    `&#34;Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;  `&#34;patchProfile.arg2.notes: must not be empty&#34;` |
| 404 |  `&#34;Extension validation failed - extensionId: {ID} \| account: {ACCOUNT} \| profile: {PROFILE}. Cause: not found&#34;` &lt;br&gt;    `&#34;Extension ID {ID} not found in the profile {PROFILE}&#34;`&lt;br&gt;    `&#34;Account: {ACCOUNT}, profile: {PROFILE} not found&#34;` |
| 409 |  `&#34;Conflict with profile extension: _id: {ID}, extType: {EXT_TYPE}, title: {TITLE}&#34;` &lt;br&gt;  `&#34;Users are currently viewing the same account: {ACCOUNT} profile: {PROFILE}&#34;`&lt;br&gt;   `&#34;Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSIONS}&#34;`  |
|500|  `&#34;An error occurred&#34;` &lt;br&gt;   `&#34;Profile: {PROFILE} inherits from library profile&#34;`&lt;br&gt;    `&#34;Unable to invoke request: unknown host, see logs for more detail.&#34;`&lt;br&gt;    `&#34;Error processing json for extension - account: {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;   `&#34;Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;    `&#34;Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}&#34;` &lt;br&gt;   `&#34;Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}&#34;` |
