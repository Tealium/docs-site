---
title: Airship Connector Setup Guide
description: This article describes how to set up the Airship connector.
url: https://docs.tealium.com/server-side-connectors/airship-connector/
---
## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Create Custom Event| ✓| ✓|
|Add Tags| ✓| ✓|
|Remove Tags| ✓| ✓|
|Set Attributes| ✓| ✓|
|Remove Attributes| ✓| ✓|

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **Region**  
(Required) Select the region associated with your Airship project.
* **Access Token**  
(Required) Access Token is used to make API calls.
* **App Key**  
App Key is used to make API calls for the action &#34;Create Custom Event&#34;.

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Create Custom Event

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100
* Max time since oldest request: 5 minutes
* Max size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Named User Id| (Required) The named user associated with the event.|
|Event Name| (Required) The name for the event.|
|Interaction Id| The identifier defining where the event occurred. In a traditional website, which would be the path and query string from the URL. In a single page app that uses hash routing, it would be the path, query string, and fragment identifier.|
|Interaction Type| Describes the type of interaction that triggered the event. For example: ‘url’, ‘social’, ‘email’. This should almost always be ‘url’ for web events. Airship can separate events with the same name by interaction\_type, providing greater insight into custom events.|
|Occurred| The timestamp the event happened for the user in ISO 8601 UTC format &#39;YYYY-MM-DDThh:mm:ss&#39;. If no Timestamp is provided, the current timestamp will be used.|
|Session Id| The user session during which the event occurred.|
|Transaction| If the event is one in a series representing a single transaction, use the transaction field to tie events together.|
|Value| The Value field respects six digits of precision to the right of the decimal point.|
|Properties| Map properties as key-value pairs for top-level attributes.&lt;br&gt; Map and use a template for more complex data structures.|
|Template Variables| (Optional) Provide template variables for Properties object data. For more information, see .&lt;br&gt; Name nested template variables with the dot notation (Example: items.name).&lt;br&gt; Nested template variables are typically built from data layer list attributes.|
|Templates| (Optional) Provide template for properties object. For more information, see .&lt;br&gt; Map template name, wrapped in double curly braces, to Properties in Event Data mapping above. For example, `{{SomeTemplateName}}`.|

### Action - Add Tags

##### Parameters

|**Parameter**| **Description**|
|---| ---|
|Named User Id| The named user to associate tags with.|
|Tags| The list of tags to add to the named user. If the tags are already present, they are not modified.&lt;br&gt; Map an array of tag values when adding multiple tags to the same tag group.|

### Action - Remove Tags

##### Parameters

|**Parameter**| **Description**|
|---| ---|
|Named User Id| The named user to disassociate tags with.|
|Tags| The list of tags to remove from the named user. If the tags are not currently present, nothing happens.&lt;br&gt; Map an array of tag values when removing multiple tags from the same tag group.|

### Action - Set Attributes

##### Parameters

|**Parameter**| **Description**|
|---| ---|
|Named User Id| The named user to set attributes on.|
|Title, First Name, Last Name, Full Name, Gender, Zipcode, City, Region, Country, Birthdate, Age, Mobile Phone, Home Phone, Work Phone, Loyalty Tier, Company, Username, Account Creation, Email Address, Altitude, Latitude, Longitude, Advertising ID (IDFA)| Map to Airship predefined or custom attributes. Custom attributes must be added in the Airship UI before they can be mapped. |

### Action - Remove Attributes

##### Parameters

|**Parameter**| **Description**|
|---| ---|
|Named User Id| The named user to remove attributes from.|
|Attributes| The list of attributes to remove from the named user.|