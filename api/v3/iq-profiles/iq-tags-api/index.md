---
title: iQ Tags API
description: The iQ Tags API lets you programmatically create, update, and delete tag configurations in an iQ Tag Management profile.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-tags-api/
---
To learn more about this API and available object fields, see [iQ Profiles API]() and [iQ Profiles Objects]().

## How it works

Use the `PATCH` method to create, update, and delete components in the iQ Profile object.

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

When you use the PATCH method, you are making changes to your profile tags programmatically using a save or save-as. After making changes with the API, you must still log into the application to publish.

### Example cURL request

```bash
curl --location --request PATCH &#39;https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}&#39; \
  --header &#39;Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9&#39;  \
  --header &#39;Content-Type: application/json&#39; \
  --data &#39;
```

## Authentication

The bearer token is used to authenticate all API calls and not the API key. The API key is only used in the authentication call. In addition to the bearer token, the authentication response includes a region-specific hostname that must be used in subsequent server-side API calls.

To learn about generating a bearer token from the API key, see [Authentication]().

## Profile fields

Profile tags are JSON objects that contain the following possible fields:

| OBJECT | TYPE | REQUIRED | DESCRIPTION |
| --- | --- | --- | --- |
| `versionTitle` | String | Optional| The title of the resulting saved version.&lt;br&gt;Default with `saveType` set to `saveAs` : `API \| {TIMESTAMP}`&lt;br&gt;Default with `saveType` set to `save`: Existing version title |
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
|`value.selectedTargets`| Map &amp;lt;string, Boolean&amp;gt;|  Optional |  An object of environments to publish the component to. `{   &#34;prod&#34; : true\|false,   &#34;qa&#34; : true\|false,   &#34;dev&#34; : true\|false }` &lt;br&gt;Default: All environments set to `true`. |
| `value.configuration` |Map &amp;lt;String, Object&amp;gt; |Optional | A String and Object Map of tag configurations made available by the vendor. Configurations are specific to each tag. For more information, see the documentation for your tag.|
|`value.advancedConfiguration`| Object |Optional |  A set of advanced configurations corresponding to the tag configuration settings. &lt;br&gt;`advConfigBundle` — **True** or **False**&lt;br&gt; `advConfigLoadType` — **True** or **False**&lt;br&gt; `advConfigOptOut` — **True**&lt;br&gt; `advConfigSend`— **True** or **False** &lt;br&gt; `advConfigSrc` — Text field&lt;br&gt; `tagTiming` — **DOM Ready** or **Prioritized** |
|`value.rules`| Object |Optional | The load rules to apply or exclude from the tag.|
|`value.dataMappings`| Map &amp;lt;String, String&amp;gt; |Optional | An object that contains the Tealium IQ variable and its corresponding mapped destination, the variable name, and the data type. You can verify the specific format for the mapped variable triggers in the **Data Mappings** screen in your tag configuration.|
|`value.dataMappings.variable`| String |Optional | The name of the variable to be mapped.|
|`value.dataMappings.type`| String |Optional | The data type of the variable to be mapped. This field supports the following variable types:&lt;br&gt;`ls` - Local storage&lt;br&gt;`ss` - Session storage&lt;br&gt;`udo` - Universal Data Object&lt;br&gt;`qp` - Query string parameter&lt;br&gt;`cp` - Cookie&lt;br&gt;`js_page` - JavaScript  variable&lt;br&gt;`dom` - DOM variable&lt;br&gt;`meta` - Meta data element&lt;br&gt;`static.text` - Static text&lt;br&gt;`static.js` - JavaScript code|
|`value.dataMappings.mappings`| String or Array of Strings |Optional | The mapped destination for the variable.|

### Example request

```json
{
  &#34;versionTitle&#34;: &#34;version title&#34;,
  &#34;notes&#34;: &#34;notes&#34;,
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;add&#34;,
      &#34;path&#34;: &#34;/tags&#34;,
      &#34;value&#34;: {
        &#34;object&#34;: &#34;tag&#34;,
        &#34;tagId&#34;: &#34;7133&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;notes&#34;: &#34;adding tag&#34;,
        &#34;name&#34;: &#34;7133 tag Google Analytics&#34;,
        &#34;dataMappings&#34;: [
          {
            &#34;variable&#34;: &#34;variable_name&#34;,
            &#34;type&#34;: &#34;udo&#34;,
            &#34;mappings&#34;: [&#34;a1&#34;, &#34;a2&#34;]
          }
        ],
        &#34;selectedTargets&#34;: {
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;advancedConfiguration&#34;: {
          &#34;bundleFlag&#34;: true,
          &#34;syncLoadType&#34;: false,
          &#34;optout&#34;: true,
          &#34;scriptSource&#34;: &#34;&#34;,
          &#34;sendFlag&#34;: false,
          &#34;tagTiming&#34;: &#34;Dom Ready&#34;
        },
        &#34;configuration&#34;: {
          &#34;tracking_id&#34;: &#34;123&#34;
        },
        &#34;rules&#34;: {
          &#34;apply&#34;: [{&#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: &#34;2&#34;, &#34;type&#34;: &#34;loadRule&#34;}]}]}],
          &#34;exclude&#34;: [{&#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: &#34;3&#34;, &#34;type&#34;: &#34;loadRule&#34;}, {&#34;uid&#34;: &#34;2&#34;, &#34;type&#34;: &#34;loadRule&#34;}]}]}]
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
&#34;op&#34; : &#34;add&#34;,
&#34;path&#34; : &#34;/tags&#34;
```

To update a specific tag, add the ID to the path:

```json
&#34;op&#34; : &#34;replace&#34;,
&#34;path&#34; : &#34;/tags/503&#34;
```

## Create tag

This PATCH method takes a profile object and additional tag fields.

### Example request

```json
{
  &#34;versionTitle&#34;: &#34;version title&#34;,
  &#34;notes&#34;: &#34;notes&#34;,
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;add&#34;,
      &#34;path&#34;: &#34;/tags&#34;,
      &#34;value&#34;: {
        &#34;object&#34;: &#34;tag&#34;,
        &#34;tagId&#34;: &#34;7133&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;notes&#34;: &#34;adding tag&#34;,
        &#34;name&#34;: &#34;7133 tag Google Analytics&#34;,
        &#34;dataMappings&#34;: [
          {
            &#34;variable&#34;: &#34;variable_name&#34;,
            &#34;type&#34;: &#34;udo&#34;,
            &#34;mappings&#34;: [&#34;a1&#34;, &#34;a2&#34;]
          }
        ],
        &#34;selectedTargets&#34;: {
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;advancedConfiguration&#34;: {
          &#34;bundleFlag&#34;: true,
          &#34;syncLoadType&#34;: false,
          &#34;optout&#34;: true,
          &#34;scriptSource&#34;: &#34;&#34;,
          &#34;sendFlag&#34;: false,
          &#34;tagTiming&#34;: &#34;Dom Ready&#34;
        },
        &#34;Configuration&#34;: {
          &#34;tracking_id&#34;: &#34;123&#34;
        },
        &#34;rules&#34;: {
          &#34;apply&#34;: [{&#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: &#34;2&#34;, &#34;type&#34;: &#34;loadRule&#34;}]}]}],
          &#34;exclude&#34;: [{&#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: &#34;3&#34;, &#34;type&#34;: &#34;loadRule&#34;}, {&#34;uid&#34;: &#34;2&#34;, &#34;type&#34;: &#34;loadRule&#34;}]}]}]
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
  &#34;versionTitle&#34;: &#34;version title&#34;,
  &#34;notes&#34;: &#34;notes&#34;,
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;replace&#34;,
      &#34;path&#34;: &#34;/tags/21&#34;,
      &#34;value&#34;: {
        &#34;object&#34;: &#34;tag&#34;,
        &#34;tagId&#34;: &#34;7133&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;notes&#34;: &#34;adding tag&#34;,
        &#34;name&#34;: &#34;Replace name by API Google Analytics&#34;,
        &#34;dataMappings&#34;: [
          {
            &#34;variable&#34;: &#34;variable_name&#34;,
            &#34;type&#34;: &#34;udo&#34;,
            &#34;mappings&#34;: [&#34;a1&#34;, &#34;a2&#34;]
          }
        ],
        &#34;selectedTargets&#34;: {
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;advancedConfiguration&#34;: {
          &#34;bundleFlag&#34;: true,
          &#34;syncLoadType&#34;: false,
          &#34;optout&#34;: true,
          &#34;scriptSource&#34;: &#34;&#34;,
          &#34;sendFlag&#34;: false,
          &#34;tagTiming&#34;: &#34;Dom Ready&#34;
        },
        &#34;Configuration&#34;: {
          &#34;tracking_id&#34;: &#34;123&#34;
        },
        &#34;rules&#34;: {
          &#34;apply&#34;: [{&#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: &#34;2&#34;, &#34;type&#34;: &#34;loadRule&#34;}]}]}],
          &#34;exclude&#34;: [{&#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: &#34;3&#34;, &#34;type&#34;: &#34;loadRule&#34;}, {&#34;uid&#34;: &#34;2&#34;, &#34;type&#34;: &#34;loadRule&#34;}]}]}]
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
  &#34;versionTitle&#34;: &#34;Version 2022.03.22.2108&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;:&#34;&#34;,
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;remove&#34;,
      &#34;path&#34;: &#34;/tags/230&#34;,
      &#34;value&#34;:{
        &#34;object&#34;:&#34;tag&#34;
      }
    }
  ]
}
```
## Error messages

Potential error messages for this endpoint:

| ERROR CODE | ERROR MESSAGE |
| --- | --- |
| 400 | `&#34;Profile libraries are out of date, merge changes before patching profile - {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;patchProfile.arg2.notes: must not be empty&#34;`|
| 404 | `&#34;Profile not found - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Profile library not found - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Profile (legacy) not found - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Users are currently viewing the same account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Latest version not found - {ACCOUNT} \| profile: {PROFILE}&#34;` |
| 409 | `&#34;Error saving profile: {PROFILE} for account: {ACCOUNT}, duplicate versions: {VERSION}&#34;` |
| 500 | `&#34;Profile: {PROFILE} inherits from library profile&#34;`&lt;br&gt;`&#34;Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}&#34;`|