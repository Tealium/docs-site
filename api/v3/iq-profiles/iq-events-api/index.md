---
title: iQ Events API
description: The iQ Events API lets you programmatically create, update, and delete event listeners in an iQ Tag Management profile.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-events-api/
---
To learn more about this API and available object fields, see [iQ Profiles API](https://docs.tealium.com/iq-profiles-v3-api/) and [iQ Profiles Objects](https://docs.tealium.com/iq-profiles-api-objects/).

## How it works

Use the `PATCH` method to create, update, and delete components in the iQ Profile object.

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

When you use the PATCH method, you are making changes to your profile events programmatically using a save or save-as. After making changes with the API, you must still log into the application to publish.

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

Profile events are JSON objects that contain the following possible fields:

| OBJECT | TYPE | REQUIRED | DESCRIPTION |
| --- | --- | --- | --- |
| `versionTitle` | String | Optional| The title of the resulting saved version.<br>Default with `saveType` set to `saveAs` : `API \| {TIMESTAMP}`<br>Default with `saveType` set to `save`: Existing version title |
| `saveType` | String| Optional| The type of save to perform with the PATCH request: `save` or `saveAs`. Default is `saveAs`. |
| `notes` | String| Required | Additional notes about the publish version. |
| `operationList` | Array | Required | A list of operation objects. For example, multiple events.<br> |
| `op` | String | Required | The operation to perform: `add`, `replace`, or `remove`.<br> |
| `path` | String | Required | The component type and ID to update, in the format:`/{TYPE}/{ID}`.<br> |
| `value.object` | String | Required | The object type being updated: `variable`, `extension`, or `event`.<br> |
| `value.name` | String | Required (for add/replace)| Name of the event. |
| `value.notes` | String | Optional | Notes about the event. |
| `value.status` | String | Required | The on/off status: `active` or `inactive`. |
|`value.occurrence`| String| Optional|  Determines the number of  times the event trigger will result in a tracking call. Values: `Run Once` or `Run Always`. Default: `Run Always`. |
| `value.type` | String | Required | Type of event being tracked. Type of event being tracked. <ul><li>[`mouseEvents`](https://docs.tealium.com/click-event/)\- Includes the following user actions:<ul><li>`click` \- When a visitor clicks their mouse on a page.</li><li>`mousedown` \- When a visitor moves their mouse down.</li><li>`mouseup` \- When a visitor moves their mouse down.</li></ul><li>[`mouseOver`](https://docs.tealium.com/mouseover-event/) \- When a visitor hovers their mouse over a specific element on a page.</li><li> [`formSubmit`](https://docs.tealium.com/form-submission-event/) \- When a visitor submits a form on a page.</li><li>[`youtubeVideo`](https://docs.tealium.com/youtube-event/) \- When a visitor interacts with an embedded YouTube video on a page.</li><li>[`vimeoVideo`](https://docs.tealium.com/vimeo-event/) \- When a visitor interacts with an embedded Vimeo video on a page.</li><li>[`html5Video`](https://docs.tealium.com/html5-video-event/) \- When a visitor interacts with an embedded HTML5 video on a page.</li><li>[`pageView`](https://docs.tealium.com/page-view-event/) \- When a visitor views a page.</li><li>[`scroll`](https://docs.tealium.com/scroll-event/) \- When a visitor scrolls through a page, vertically or horizontally.</li><li>[`elementVisibility`](https://docs.tealium.com/element-visibility-event/) \- When the page displays a screen element to a visitor.</li></li></ul>|
|`value.scope`| String| Optional|  The name of the event scope. <br>`DOM Ready`<br> `After Load Rules` |
| `value.trackingEvent` | String | Required |The tracking event for the event listener: <br>`link` <br> `view`<br>`custom-event-of-anytype `|
|`value.selectedTargets`| Map &lt;string, Boolean&gt;|  Optional |  An object of environments to publish the component to: <br> `{   "prod" : true\|false,   "qa" : true\|false,   "dev" : true\|false }` <br>Default: All environments set to `true`. |
| `value.eventTriggers` | Object | Required | Configurations specific to each event type. Values are of the format: `"object": "[value.Type]"` and are followed by configurations for the event. |
|  `value.eventVariables` | Array | Required| Variables specific to each event type. |
| `value.bufferingEventVariables` | Array | Required | Variables that indicate if a buffering event has taken place. |
| `value.rules` | Object | Required | Rules that dictate when an event listener is loaded on the page.  |

### Example request

```json
{
  "versionTitle": "Adding Events",
  "saveType": "saveAs",
  "notes": "added a new event", 
  "operationList": [
    {
      "op": "add",
      "path": "/events",
      "value":{
        "object": "event",
        "name": "new API event",
        "notes": "event notes",
        "status": "active",
        "occurence": "Run Always",
        "type": "youtubeVideo",
        "scope": "After Load Rules",
        "trackingEvent": "link",
        "selectedTargets":{
          "qa": true,
          "dev": true,
          "prod": true
        },
        "eventTriggers": {
          "object": "youtubeVideo",
           "enabledVideoEventsList": [
            "play", "pause", "buffering", "milestones"
          ],
           "cssSelector": "mycss.selector",
           "milestoneOption": "percentageComplete",
           "milestonesList": [25,50,75,100],
         },
         "eventVariables":
         [
          {
            "variable": "tealium_event",
            "type": "text",
            "value": "youTube_video"
          }
        ],
         "bufferingEventVariables": [
          {
            "variable": "buffering",
            "type": "text",
            "value": "true"
          }
        ],
         "rules": {
          "apply": [ 
            {
              "and": [{"or": [{"uid": 52, "type": "loadRule"}]}]}
            ],
          "exclude": []
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
"op" : "add",
"path" : "/events"
```

To update a specific event, add the ID to the path:

```json
"op" : "replace",
"path" : "/events/503"
```

## Create event

This PATCH method takes a profile object and additional event fields.

### Example request

```json
{
  "versionTitle": "Adding Events",
  "saveType": "saveAs",
  "notes": "added a new event", 
  "operationList": [
    {
      "op": "add",
      "path": "/events",
      "value":{
        "object": "event",
        "name": "new API event",
        "status": "active",
        "occurence": "Run Always",
        "type": "youtubeVideo",
        "scope": "After Load Rules",
        "trackingEvent": "link",
        "selectedTargets":{
          "qa": true,
          "dev": true,
          "prod": true
        },
        "eventTriggers": {
          "object": "youtubeVideo",
           "enabledVideoEventsList": [
            "play", "pause", "buffering", "milestones"
          ],
           "cssSelector": "mycss.selector",
           "milestoneOption": "percentageComplete",
           "milestonesList": [25,50,75,100],
         },
         "eventVariables":
         [
          {
            "variable": "tealium_event",
            "type": "text",
            "value": "youTube_video"
          }
        ],
         "bufferingEventVariables": [
          {
            "variable": "buffering",
            "type": "text",
            "value": "true"
          }
        ],
         "rules": {
          "apply": [ 
            {
              "and": [{"or": [{"uid": 52, "type": "loadRule"}]}]}
            ],
          "exclude": []
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
  "versionTitle": "Adding Events",
  "saveType": "saveAs",
  "notes": "added a new event", 
  "operationList": [
    {
      "op": "replace",
      "path": "/events/503",
     "value":{
        "object": "event",
        "name": "new API event",
        "status": "active",
        "occurence": "Run Always",
        "type": "youtubeVideo",
        "scope": "After Load Rules",
        "trackingEvent": "link",
        "selectedTargets":{
          "qa": true,
          "dev": true,
          "prod": true
        },
        "eventTriggers": {
          "object": "youtubeVideo",
           "enabledVideoEventsList": [
            "play", "pause", "buffering", "milestones"
          ],
           "cssSelector": "mycss.selector",
           "milestoneOption": "percentageComplete",
           "milestonesList": [25,50,75,100],
         },
         "eventVariables":
         [
          {
            "variable": "tealium_event",
            "type": "text",
            "value": "youTube_video"
          }
        ],
         "bufferingEventVariables": [
          {
            "variable": "buffering",
            "type": "text",
            "value": "true"
          }
        ],
         "rules": {
          "apply": [ 
            {
              "and": [{"or": [{"uid": 52, "type": "loadRule"}]}]}
            ],
          "exclude": []
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
  "versionTitle": "Adding Events",
  "saveType": "saveAs",
  "notes": "added a new event", 
  "operationList": [
    {
      "op": "remove",
      "path": "/events/503",
      "value":{
        "object": "event"
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
| 404 | `"Profile not found - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Profile library not found - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Profile (legacy) not found - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Latest version not found - {ACCOUNT} \| profile: {PROFILE}"` |
| 409 |  `"Users are currently viewing the same account: {ACCOUNT} \| profile: {PROFILE}"` |
| 500 | `"Profile: {PROFILE} inherits from library profile"`<br>`"Error saving profile metadata - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Error saving profile - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"Error saving profile(legacy) - {ACCOUNT} \| profile: {PROFILE}"`|