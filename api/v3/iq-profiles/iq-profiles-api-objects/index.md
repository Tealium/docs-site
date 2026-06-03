---
title: iQ Profiles API Objects
description: This document describes the JSON structure of Tealium iQ profiles, detailing the fields, configurations, and relationships between variables, tags, load rules, extensions, and events within a profile.
url: https://docs.tealium.com/api/v3/iq-profiles/iq-profiles-api-objects/
---

## Available fields

|Object| Type| Description|
|---| ---| ---|
|`account`| String| The Tealium account name.|
|`profile`| String| The Tealium profile name.|
|`versionTitle`| String| The title of this version of the iQ profile. If not specified, the `versionTitle` will be formatted as `API \| {TIMESTAMP}`.|
|`version`| String| The version ID of this iQ profile.|
|`minorVersion`| String| The version ID that is updated after you save a profile whether published or not. If you save and then publish, the `minorVersion` and `version` will not match. They will match only if you perform a Save As.|
|`parentVersion`| String | The originating profile version for `save` or `saveAs` operations. |
|`creation`| Date| Date of profile creation.|
|`customTargets`| String|  List of user-defined custom target environments. |
|`versionDetails`| Object| Details about the current version including: location of where the current profile version is published to, the email of the user who published the profile, and notes about the profile.|
|`environmentVersions`| Object| List of the current published profile version for each environment. |
|`dataCloudLinkedProfiles`| String| The linked server-side profile name.|
|`libraryType`| String|  The type of library being inherited. If no library is inherited, the value is `NONE`.&lt;br&gt; `Required` - All profiles include this library automatically.&lt;br&gt; `Optional` - You specify which profiles include this library.&lt;br&gt;`NONE` - Indicates the given profile is not a library. |
|`linkedProfiles`|  Array[object]| For libraries, this field lists the values that the profiles inherit from this library. For profiles, this value is `null`.|
|`linkedLibraries`| Array[object]| For profiles, this field represents the libraries linked to the profile. For libraries this value is `null`.|
|`variables`| Array of variables| Array of variable objects in the profile.|
|`tags`| Array of tags| Array of tags objects in the profile.|
|`loadRules`| Array of load rules| Array of load rules objects in the profile.|
|`extensions`| Array of extensions| Array of extensions objects in the profile.|
|`events`| Array of events| Array of event objects in the profile.|
|`versionIds` | Array |List of previous versions. |
 |`templateList`|--| Lists all the tag templates associated with the profile.|

**Example**

```json
{
    &#34;account&#34;: &#34;my_account&#34;,
    &#34;profile&#34;: &#34;main&#34;,
    &#34;versionTitle&#34;: &#34;Version 2022.03.22.2108&#34;,
    &#34;version&#34;: &#34;202203222108&#34;,
    &#34;minorVersion&#34;: &#34;202203222108&#34;,
    &#34;parentVersion&#34;: &#34;202309191127&#34;,
    &#34;creation&#34;: &#34;202201131654&#34;,
    &#34;customTargets&#34;: null,
    &#34;versionDetails&#34;: {},
    &#34;environmentVersions&#34;: {},
    &#34;dataCloudLinkedProfiles&#34;: &#34;{}&#34;,
    &#34;libraryType&#34;: &#34;NONE&#34;,
    &#34;linkedProfiles&#34;: null,
    &#34;linkedLibraries&#34;: [],
    &#34;variables&#34;: null,
    &#34;extensions&#34;: null,
    &#34;loadRules&#34;: null,
    &#34;tags&#34;: null,
    &#34;events&#34;: null,
    &#34;templateList&#34;: null,
    &#34;versionIds&#34;: null
}
```

## Variables

|Object| Type| Description|
|---| ---| ---|
|`id`| Number| Variable ID.|
|`uniqueIdentifier`| String| Variable identifier used to refer to the variable from extension `conditions`, tag `dataMappings`, and load rule `conditions`.|
|`name`| String| The variable title.|
|`alias`| String| The variable name.|
|`type`| String| A prefix representing the variable type.&lt;br&gt;  `ls` - Local storage &lt;br&gt; `ss` - Session storage &lt;br&gt; `udo` - Universal Data Object&lt;br&gt; `qp` - Query string parameter&lt;br&gt; `cp` - Cookie&lt;br&gt; `js` - JavaScript  variable&lt;br&gt; `meta` - Meta data element&lt;br&gt; `va` - AudienceStream attribute |
|`notes`| String| Notes about the variable.|
|`context`| Array| The scope for attributes imported from AudienceStream.&lt;br&gt; Values: `current_visit` or `visitor`|
|`library`| String| Name of the library from which the variable is inherited.|
|`imported`| String| The source of an imported variable. This is set to `AudienceStream` for all AudienceStream attributes.|
|`usedIn`| Object| The list of IDs where this variable is used.|

## Tags

|Object| Type| Description|
|---| ---| ---|
|`id`| Number| The unique ID of the tag.|
|`tagID`| Number| The system ID for this tag type. This value is the same for all tags of the same type. For example, `6037` for the Facebook Pixel tag.|
|`name`| String| The user generated tag name from the tag configuration.|
|`library`| String| Name of the library from which the tag is inherited.|
|`status`| String| The on/off status: `active` or `inactive`.|
|`notes`| String| Notes about the tag.|
|`dataMappings`| Map &amp;lt;String, String&amp;gt;|  Returns Tealium IQ variable and its corresponding mapped destination. |
|`selectedTargets`| Map&amp;lt;String, Boolean&amp;gt;|  An object of environments where the tag is allowed to be published. |
|`environmentVersions`| Map&amp;lt;String, Boolean&amp;gt;| An array of the environments where this tag was last published.|
|`advancedConfiguration`| Object|  A set of advanced configurations corresponding to the tag configuration settings.&lt;br&gt; `advConfigBundle` — **True** or **False**&lt;br&gt; `advConfigLoadType` — **True** or **False**&lt;br&gt; `advConfigOptOut` — **True**&lt;br&gt; `advConfigSend`— **True** or **False** `advConfigSrc` — Text field&lt;br&gt; `tagTiming` — **DOM Ready** or **Prioritized** |
| `configuration` |  Map &amp;lt;String, Object&amp;gt; |  A String and Object Map of tag configurations made available by the vendor. |
|`rules`| Object| The load rules to apply or exclude from the tag.|
 | `template` |  Object |  Returns the full tag template. Requires `includes = tags.template` in the request. |

## Load rules

|Object| Type| Description|
|---| ---| ---|
|`id`| Number| The unique ID of the load rule.|
|`name`| String| The name of the load rule.|
|`status`| String| The on/off status: `active` or `inactive`.|
|`library`| String| The name of the associated library.|
|`notes`| String| Notes about the load rules.|
|`startDate`| Date| For scheduled load rules, the start date.|
|`endDate`| Date| For scheduled load rules, the end date.|
|`environmentVersions`| Map&amp;lt;String, Boolean&amp;gt;| List of the current published load rule version for each environment. |
|`usedIn`| Object| The list of IDs where this load rule is used.|
|`conditions`| Array[object]| An array of objects that include variable name, operator, and value. Each object within an array is associated by an `and` operator while each array within the array is associated by an `or` operator.|

## Extensions

|Object| Type| Description|
|---| ---| ---|
|`id`| Number| The unique ID of the extension.|
|`extensionId`| Number| The system ID for this extension type. This value is the same for all extensions of the same type. For example, `100036` for the JavaScript Code extension.|
|`extensionType`| String| The system name for this extension type. This value is the same for all extensions of the same type. For example, `Javascript Code` for the JavaScript Code extension.|
|`name`| String| The name of the extension.|
|`library`| String| The name of the associated library.|
|`notes`| String| The notes entered for the extension.|
|`loadRule`| Mixed| A comma-separated list of load rule IDs, or `all` for All Pages.|
|`scope`| String|  The name of the extension scope or, for tag-scoped extensions, a comma-separated list of tag IDs. &lt;br&gt; `utag Sync`&lt;br&gt; `Pre Loader`&lt;br&gt; `Before Load Rules`&lt;br&gt; `After Load Rules`&lt;br&gt; `DOM Ready`&lt;br&gt; `Tag Scoped Extensions`&lt;br&gt; `After Tag Extensions` For more information about tag-scoped extensions and how they work with `occurrence`, see [Understanding Scope](). |
|`occurrence`| String|  Determines the number of times the JavaScript code extension runs per page load. Values: `Run Once` or `Run Always`. |
|`status`| String| The on/off status: `active` or `inactive`.|
|`selectedTargets`| Map&amp;lt;String, Boolean&amp;gt;| Environments where the extension is allowed to be published.|
|`environmentVersions`| Map&amp;lt;String, Boolean&amp;gt;| An array of the environments where the extension is published.|
|`conditions`| Array[object]| The conditions set for the specific extension.|
|`configuration`| Map &amp;lt;String, Object&amp;gt;| A Map of configurations for each extension.|

## Events

| OBJECT | TYPE | DESCRIPTION |
| --- | --- | --- |
| `id` | Number | The unique ID of the event. |
| `eventID` | Number | The system ID for this event type. This value is the same for all events of the same type.  |
| `name` | String | Name of the event. |
| `status` | String | The on/off status: `active` or `inactive`. |
| `eventType` | String | Type of event being tracked. &lt;ul&gt;&lt;li&gt;[`mouseEvents`]()\- Includes the following user actions:&lt;ul&gt;&lt;li&gt;`click` \- When a visitor clicks their mouse on a page.&lt;/li&gt;&lt;li&gt;`mousedown` \- When a visitor moves their mouse down.&lt;/li&gt;&lt;li&gt;`mouseup` \- When a visitor moves their mouse down.&lt;/li&gt;&lt;/ul&gt;&lt;li&gt;[`mouseOver`]() \- When a visitor hovers their mouse over a specific element on a page.&lt;/li&gt;&lt;li&gt; [`formSubmit`]() \- When a visitor submits a form on a page.&lt;/li&gt;&lt;li&gt;[`youtubeVideo`]() \- When a visitor interacts with an embedded YouTube video on a page.&lt;/li&gt;&lt;li&gt;[`vimeoVideo`]() \- When a visitor interacts with an embedded Vimeo video on a page.&lt;/li&gt;&lt;li&gt;[`html5Video`]() \- When a visitor interacts with an embedded HTML5 video on a page.&lt;/li&gt;&lt;li&gt;[`pageView`]() \- When a visitor views a page.&lt;/li&gt;&lt;li&gt;[`scroll`]() \- When a visitor scrolls through a page, vertically or horizontally.&lt;/li&gt;&lt;li&gt;[`elementVisibility`]() \- When the page displays a screen element to a visitor.&lt;/li&gt;&lt;/li&gt;&lt;/ul&gt;|
| `scope` | String | The name of the extension scope or, for tag-scoped extensions, a comma-separated list of tag IDs.&lt;br&gt;`After Load Rules`&lt;br&gt;`DOM Ready`&lt;br&gt;For more information about tag-scoped events, see [Scope](). |
| `trackingEvent` | String | The event call made when the event takes place. |
| `notes` | String | Notes about the event. |
| `library` | String | The name of the associated library. |
| `eventLoadRulesList` | String | A list of all load rules used in the event. |
| `eventTrigger` | Object | Configurations specific to each event type. For more information about event triggers, see [Events &gt; Event Triggers](). |
| `selectedTargets` | Map\&lt;String, Boolean&gt; | Environments where the event is allowed to be published. |
| `environmentVersions` | Map\&lt;String, Boolean&gt; | An array of the environments where the event is published. |
| `eventVariables` | Object | Variables specific to each event type. |
| `rules` | Object | Rules that dictate when an event listener is loaded on the page.  |
| `usedIn` | Object | The list of IDs where this event is used. |
