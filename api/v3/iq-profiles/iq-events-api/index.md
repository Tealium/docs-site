---
title: iQ Events API
description: The iQ Events API lets you programmatically create, update, and delete event listeners in an iQ Tag Management profile.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-events-api/
---
To learn more about this API and available object fields, see [iQ Profiles API]() and [iQ Profiles Objects]().

## How it works

Use the `PATCH` method to create, update, and delete components in the iQ Profile object.

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

When you use the PATCH method, you are making changes to your profile events programmatically using a save or save-as. After making changes with the API, you must still log into the application to publish.

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

Profile events are JSON objects that contain the following possible fields:

| OBJECT | TYPE | REQUIRED | DESCRIPTION |
| --- | --- | --- | --- |
| `versionTitle` | String | Optional| The title of the resulting saved version.&lt;br&gt;Default with `saveType` set to `saveAs` : `API \| {TIMESTAMP}`&lt;br&gt;Default with `saveType` set to `save`: Existing version title |
| `saveType` | String| Optional| The type of save to perform with the PATCH request: `save` or `saveAs`. Default is `saveAs`. |
| `notes` | String| Required | Additional notes about the publish version. |
| `operationList` | Array | Required | A list of operation objects. For example, multiple events.&lt;br&gt; |
| `op` | String | Required | The operation to perform: `add`, `replace`, or `remove`.&lt;br&gt; |
| `path` | String | Required | The component type and ID to update, in the format:`/{TYPE}/{ID}`.&lt;br&gt; |
| `value.object` | String | Required | The object type being updated: `variable`, `extension`, or `event`.&lt;br&gt; |
| `value.name` | String | Required (for add/replace)| Name of the event. |
| `value.notes` | String | Optional | Notes about the event. |
| `value.status` | String | Required | The on/off status: `active` or `inactive`. |
|`value.occurrence`| String| Optional|  Determines the number of  times the event trigger will result in a tracking call. Values: `Run Once` or `Run Always`. Default: `Run Always`. |
| `value.type` | String | Required | Type of event being tracked. Type of event being tracked. &lt;ul&gt;&lt;li&gt;[`mouseEvents`]()\- Includes the following user actions:&lt;ul&gt;&lt;li&gt;`click` \- When a visitor clicks their mouse on a page.&lt;/li&gt;&lt;li&gt;`mousedown` \- When a visitor moves their mouse down.&lt;/li&gt;&lt;li&gt;`mouseup` \- When a visitor moves their mouse down.&lt;/li&gt;&lt;/ul&gt;&lt;li&gt;[`mouseOver`]() \- When a visitor hovers their mouse over a specific element on a page.&lt;/li&gt;&lt;li&gt; [`formSubmit`]() \- When a visitor submits a form on a page.&lt;/li&gt;&lt;li&gt;[`youtubeVideo`]() \- When a visitor interacts with an embedded YouTube video on a page.&lt;/li&gt;&lt;li&gt;[`vimeoVideo`]() \- When a visitor interacts with an embedded Vimeo video on a page.&lt;/li&gt;&lt;li&gt;[`html5Video`]() \- When a visitor interacts with an embedded HTML5 video on a page.&lt;/li&gt;&lt;li&gt;[`pageView`]() \- When a visitor views a page.&lt;/li&gt;&lt;li&gt;[`scroll`]() \- When a visitor scrolls through a page, vertically or horizontally.&lt;/li&gt;&lt;li&gt;[`elementVisibility`]() \- When the page displays a screen element to a visitor.&lt;/li&gt;&lt;/li&gt;&lt;/ul&gt;|
|`value.scope`| String| Optional|  The name of the event scope. &lt;br&gt;`DOM Ready`&lt;br&gt; `After Load Rules` |
| `value.trackingEvent` | String | Required |The tracking event for the event listener: &lt;br&gt;`link` &lt;br&gt; `view`&lt;br&gt;`custom-event-of-anytype `|
|`value.selectedTargets`| Map &amp;lt;string, Boolean&amp;gt;|  Optional |  An object of environments to publish the component to: &lt;br&gt; `{   &#34;prod&#34; : true\|false,   &#34;qa&#34; : true\|false,   &#34;dev&#34; : true\|false }` &lt;br&gt;Default: All environments set to `true`. |
| `value.eventTriggers` | Object | Required | Configurations specific to each event type. Values are of the format: `&#34;object&#34;: &#34;[value.Type]&#34;` and are followed by configurations for the event. |
|  `value.eventVariables` | Array | Required| Variables specific to each event type. |
| `value.bufferingEventVariables` | Array | Required | Variables that indicate if a buffering event has taken place. |
| `value.rules` | Object | Required | Rules that dictate when an event listener is loaded on the page.  |

### Example request

```json
{
  &#34;versionTitle&#34;: &#34;Adding Events&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;added a new event&#34;, 
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;add&#34;,
      &#34;path&#34;: &#34;/events&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;event&#34;,
        &#34;name&#34;: &#34;new API event&#34;,
        &#34;notes&#34;: &#34;event notes&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;occurence&#34;: &#34;Run Always&#34;,
        &#34;type&#34;: &#34;youtubeVideo&#34;,
        &#34;scope&#34;: &#34;After Load Rules&#34;,
        &#34;trackingEvent&#34;: &#34;link&#34;,
        &#34;selectedTargets&#34;:{
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;eventTriggers&#34;: {
          &#34;object&#34;: &#34;youtubeVideo&#34;,
           &#34;enabledVideoEventsList&#34;: [
            &#34;play&#34;, &#34;pause&#34;, &#34;buffering&#34;, &#34;milestones&#34;
          ],
           &#34;cssSelector&#34;: &#34;mycss.selector&#34;,
           &#34;milestoneOption&#34;: &#34;percentageComplete&#34;,
           &#34;milestonesList&#34;: [25,50,75,100],
         },
         &#34;eventVariables&#34;:
         [
          {
            &#34;variable&#34;: &#34;tealium_event&#34;,
            &#34;type&#34;: &#34;text&#34;,
            &#34;value&#34;: &#34;youTube_video&#34;
          }
        ],
         &#34;bufferingEventVariables&#34;: [
          {
            &#34;variable&#34;: &#34;buffering&#34;,
            &#34;type&#34;: &#34;text&#34;,
            &#34;value&#34;: &#34;true&#34;
          }
        ],
         &#34;rules&#34;: {
          &#34;apply&#34;: [ 
            {
              &#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: 52, &#34;type&#34;: &#34;loadRule&#34;}]}]}
            ],
          &#34;exclude&#34;: []
        }
      }
    } 
  ] 
}
```

## PATCH operation parameters

Instead of `POST`, `PUT`, and `DELETE` methods, the `PATCH` method uses the `op` parameter to specify the action to perform.

The `op` parameter supports the following values:

*   `add` \- Create the component.
*   `replace` \- Update the component.
*   `remove` \- Delete the component.

To specify the type and ID of the component, use the `path` parameter. The `path` parameter format is `/{TYPE}/{ID}`.

For example, to add an event use:

```json
&#34;op&#34; : &#34;add&#34;,
&#34;path&#34; : &#34;/events&#34;
```

To update a specific event, add the ID to the path:

```json
&#34;op&#34; : &#34;replace&#34;,
&#34;path&#34; : &#34;/events/503&#34;
```

## Create event

This PATCH method takes a profile object and additional event fields.

### Example request

```json
{
  &#34;versionTitle&#34;: &#34;Adding Events&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;added a new event&#34;, 
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;add&#34;,
      &#34;path&#34;: &#34;/events&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;event&#34;,
        &#34;name&#34;: &#34;new API event&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;occurence&#34;: &#34;Run Always&#34;,
        &#34;type&#34;: &#34;youtubeVideo&#34;,
        &#34;scope&#34;: &#34;After Load Rules&#34;,
        &#34;trackingEvent&#34;: &#34;link&#34;,
        &#34;selectedTargets&#34;:{
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;eventTriggers&#34;: {
          &#34;object&#34;: &#34;youtubeVideo&#34;,
           &#34;enabledVideoEventsList&#34;: [
            &#34;play&#34;, &#34;pause&#34;, &#34;buffering&#34;, &#34;milestones&#34;
          ],
           &#34;cssSelector&#34;: &#34;mycss.selector&#34;,
           &#34;milestoneOption&#34;: &#34;percentageComplete&#34;,
           &#34;milestonesList&#34;: [25,50,75,100],
         },
         &#34;eventVariables&#34;:
         [
          {
            &#34;variable&#34;: &#34;tealium_event&#34;,
            &#34;type&#34;: &#34;text&#34;,
            &#34;value&#34;: &#34;youTube_video&#34;
          }
        ],
         &#34;bufferingEventVariables&#34;: [
          {
            &#34;variable&#34;: &#34;buffering&#34;,
            &#34;type&#34;: &#34;text&#34;,
            &#34;value&#34;: &#34;true&#34;
          }
        ],
         &#34;rules&#34;: {
          &#34;apply&#34;: [ 
            {
              &#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: 52, &#34;type&#34;: &#34;loadRule&#34;}]}]}
            ],
          &#34;exclude&#34;: []
        }
      }
    } 
  ] 
}
```

## Update event

This PATCH method takes a profile object and additional event fields.

### Example request

```json
{
  &#34;versionTitle&#34;: &#34;Adding Events&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;added a new event&#34;, 
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;replace&#34;,
      &#34;path&#34;: &#34;/events/503&#34;,
     &#34;value&#34;:{
        &#34;object&#34;: &#34;event&#34;,
        &#34;name&#34;: &#34;new API event&#34;,
        &#34;status&#34;: &#34;active&#34;,
        &#34;occurence&#34;: &#34;Run Always&#34;,
        &#34;type&#34;: &#34;youtubeVideo&#34;,
        &#34;scope&#34;: &#34;After Load Rules&#34;,
        &#34;trackingEvent&#34;: &#34;link&#34;,
        &#34;selectedTargets&#34;:{
          &#34;qa&#34;: true,
          &#34;dev&#34;: true,
          &#34;prod&#34;: true
        },
        &#34;eventTriggers&#34;: {
          &#34;object&#34;: &#34;youtubeVideo&#34;,
           &#34;enabledVideoEventsList&#34;: [
            &#34;play&#34;, &#34;pause&#34;, &#34;buffering&#34;, &#34;milestones&#34;
          ],
           &#34;cssSelector&#34;: &#34;mycss.selector&#34;,
           &#34;milestoneOption&#34;: &#34;percentageComplete&#34;,
           &#34;milestonesList&#34;: [25,50,75,100],
         },
         &#34;eventVariables&#34;:
         [
          {
            &#34;variable&#34;: &#34;tealium_event&#34;,
            &#34;type&#34;: &#34;text&#34;,
            &#34;value&#34;: &#34;youTube_video&#34;
          }
        ],
         &#34;bufferingEventVariables&#34;: [
          {
            &#34;variable&#34;: &#34;buffering&#34;,
            &#34;type&#34;: &#34;text&#34;,
            &#34;value&#34;: &#34;true&#34;
          }
        ],
         &#34;rules&#34;: {
          &#34;apply&#34;: [ 
            {
              &#34;and&#34;: [{&#34;or&#34;: [{&#34;uid&#34;: 52, &#34;type&#34;: &#34;loadRule&#34;}]}]}
            ],
          &#34;exclude&#34;: []
        }
      }
    } 
  ] 
}
```

## Delete event

This PATCH method takes a profile object and additional event fields.

### Example request

```json
{
  &#34;versionTitle&#34;: &#34;Adding Events&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;added a new event&#34;, 
  &#34;operationList&#34;: [
    {
      &#34;op&#34;: &#34;remove&#34;,
      &#34;path&#34;: &#34;/events/503&#34;,
      &#34;value&#34;:{
        &#34;object&#34;: &#34;event&#34;
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
| 404 | `&#34;Profile not found - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Profile library not found - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Profile (legacy) not found - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Latest version not found - {ACCOUNT} \| profile: {PROFILE}&#34;` |
| 409 |  `&#34;Users are currently viewing the same account: {ACCOUNT} \| profile: {PROFILE}&#34;` |
| 500 | `&#34;Profile: {PROFILE} inherits from library profile&#34;`&lt;br&gt;`&#34;Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}&#34;`|