---
title: XiTi by AT Internet Connector Setup Guide
description: XiTi is a web analytics tool provided by AT Internet that provides data and performance indicators, making it possible to have an overview of a website's traffic.
url: https://docs.tealium.com/server-side-connectors/xiti-by-at-internet-connector/
---
## Connector Actions

| **Action Name**  | **AudienceStream** | **EventStream** |
|:-----------------------|:-------------------|:----------------|
| Send Custom Page Hit | ✓  | ✓ |
| Send Media Play Hit  | ✓  | ✓ |
| Send Media Refresh Hit | ✓  | ✓ |
| Send Media Pause Hit | ✓  | ✓ |
| Send Media Stop Hit  | ✓  | ✓ |
| Send Media Move Hit  | ✓  | ✓ |

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **URL**
  * (Required) Provide your Collection server&#39;s full hit URL to submit request to.
  * For example, `https://logs.xiti.com/hit.xiti`
  * For more information, see [Craft your Hit](https://developers.atinternet-solutions.com/general-en/craft-your-hit/)

* **Site Number**
  * (Required) The site on which the data should be counted.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Custom Page Hit

#### Parameters

| **Parameter** | **Description**  |
|:--------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Comp  | &lt;ul&gt;&lt;li&gt;(Required) Must be unique for each visitor&lt;/li&gt;&lt;li&gt;See [XiTi by AT Internet&#39;s documentation](https://developers.atinternet-solutions.com/general-en/craft-your-hit/)&lt;/li&gt;&lt;/ul&gt; |
| Page  | &lt;ul&gt;&lt;li&gt;(Required) The name of the page accessed&lt;/li&gt;&lt;li&gt;No longer than 250 characters&lt;/li&gt;&lt;/ul&gt; |
| Chapters  | &lt;ul&gt;&lt;li&gt;One to three chapters&lt;/li&gt;&lt;li&gt;Configure using an array attribute type&lt;/li&gt;&lt;/ul&gt;  |
| Level 2 | &lt;ul&gt;&lt;li&gt;Must be configured ahead of time in the interface to retrieve the corresponding ID&lt;/li&gt;&lt;/ul&gt;  |
| Additional Hit Parameters | &lt;ul&gt;&lt;li&gt;Provide additional values if needed&lt;/li&gt;&lt;li&gt;Template Support: To use a template, configure templates and template variables sections below and then reference the template enclosing its name into double curly braces, for example: `{{MyTemplateName}}`&lt;/li&gt;&lt;/ul&gt;  |
| Template Variables  | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with dot notation.&lt;/li&gt;&lt;li&gt;For example, `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes&lt;/li&gt;&lt;/ul&gt; |
| Templates | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in message data&lt;/li&gt;&lt;li&gt;&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt;  |

### Action - Send Media Play Hit

#### Parameters

| **Parameter** | **Description**  |
|:------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Unique Visitor ID | &lt;ul&gt;&lt;li&gt;(Required) Must be unique for each visitor&lt;/li&gt;&lt;li&gt;See [XiTi by AT Internet&#39;s documentation](https://developers.atinternet-solutions.com/general-en/craft-your-hit/)&lt;/li&gt;&lt;/ul&gt; |
| Content Label | &lt;ul&gt;&lt;li&gt;One to three labels&lt;/li&gt;&lt;li&gt;Configure using an array attribute type, or a single label can be specified as a scalar value&lt;/li&gt;&lt;/ul&gt;  |
| Media Type  | &lt;ul&gt;&lt;li&gt;(Required) Select media type&lt;/li&gt;&lt;li&gt;Options are `Video`, `Audio`,` Pre-roll video`, `Mid-roll video`, `Post-roll video`&lt;/li&gt;&lt;/ul&gt; |
| Broadcast Type  | &lt;ul&gt;&lt;li&gt;(Required) Select broadcast type&lt;/li&gt;&lt;li&gt;Options are `Clip` or `Live`&lt;/li&gt;&lt;/ul&gt;  |
| Content Duration  | &lt;ul&gt;&lt;li&gt;Content duration in seconds is required for `Clip` Broadcast Type&lt;/li&gt;&lt;li&gt;Not applicable for live broadcast&lt;/li&gt;&lt;/ul&gt;  |
| Broadcast Location  | &lt;ul&gt;&lt;li&gt;(Required) Select broadcast type&lt;/li&gt;&lt;li&gt;Options are `internal` or `external`&lt;/li&gt;&lt;/ul&gt;  |
| Content Level | &lt;ul&gt;&lt;li&gt;(Optional) Must be configured ahead of time using XiTi website to retrieve the corresponding ID&lt;/li&gt;&lt;/ul&gt; |
| Content buffering | &lt;ul&gt;&lt;li&gt;(Optional) Set `1` while buffering,  at the end of the buffering&lt;/li&gt;&lt;/ul&gt; |
| Page Label  | &lt;ul&gt;&lt;li&gt;(Optional) Label of the page where the content is played (with optional tree structure)&lt;/li&gt;&lt;/ul&gt;  |
| Page Level 2  | &lt;ul&gt;&lt;li&gt;(Optional) Level 2 of the page where the content is played&lt;/li&gt;&lt;/ul&gt; |
| Player Identifier | &lt;ul&gt;&lt;li&gt;(Optional) Useful when there are multiple players on the same page&lt;/li&gt;&lt;/ul&gt; |
| Label of linked content | &lt;ul&gt;&lt;li&gt;(Optional) Includes tree structure if any; used in case of a pre/mid/post-roll content&lt;/li&gt;&lt;/ul&gt; |
| Broadcast Domain  | &lt;ul&gt;&lt;li&gt;Optional&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;Broadcast domain, in case of an external broadcast&lt;/li&gt;&lt;/ul&gt;  |
| Template Variables  | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with dot notation&lt;/li&gt;&lt;li&gt;For example, `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes&lt;/li&gt;&lt;/ul&gt; |
| Templates | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in message data&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt;  |

### Action - Send Media Refresh Hit

#### Parameters

| **Parameter** | **Description** |
|:----------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Unique Visitor ID | &lt;ul&gt;&lt;li&gt;(Required) Must be unique for each visitor&lt;/li&gt;&lt;li&gt;See [XiTi by AT Internet&#39;s documentation](https://developers.atinternet-solutions.com/general-en/craft-your-hit/)&lt;/li&gt;&lt;/ul&gt;  |
| Content Label | &lt;ul&gt;&lt;li&gt;One to three labels&lt;/li&gt;&lt;li&gt;Configure using an array attribute type or a single label can be specified as a scalar value&lt;/li&gt;&lt;/ul&gt;  |
| Media Type  | &lt;ul&gt;&lt;li&gt;(Required) Select media type&lt;/li&gt;&lt;li&gt;Options are `Video`, `Audio`, `Pre-roll video`, `Mid-roll video`, `Post-roll video`&lt;/li&gt;&lt;/ul&gt;  |
| Broadcast Type  | &lt;ul&gt;&lt;li&gt;(Required) Select broadcast type&lt;/li&gt;&lt;li&gt;Options are `Clip` or `Live`&lt;/li&gt;&lt;/ul&gt; |
| Content Duration  | &lt;ul&gt;&lt;li&gt;Content duration in seconds is required for `Clip` Broadcast Type&lt;/li&gt;&lt;li&gt;Not applicable for live broadcast&lt;/li&gt;&lt;/ul&gt; |
| Broadcast Location  | &lt;ul&gt;&lt;li&gt;(Required) Select broadcast type&lt;/li&gt;&lt;li&gt;Options are `internal` or `external`&lt;/li&gt;&lt;/ul&gt; |
| Content Level | &lt;ul&gt;&lt;li&gt;(Optional) Must be configured ahead of time using XiTi website to retrieve the corresponding ID&lt;/li&gt;&lt;/ul&gt;  |
| Content Buffering | &lt;ul&gt;&lt;li&gt;(Optional) Set `1` while buffering,  at the end of the buffering&lt;/li&gt;&lt;/ul&gt;  |
| Page Level 2  | &lt;ul&gt;&lt;li&gt;(Optional) Level 2 of the page where the content is played&lt;/li&gt;&lt;/ul&gt;  |
| Player Identifier | &lt;ul&gt;&lt;li&gt;(Optional) Useful when there are multiple players on the same page&lt;/li&gt;&lt;/ul&gt;  |
| Label of the Linked Content | &lt;ul&gt;&lt;li&gt;(Optional) Includes tree structure, if any&lt;/li&gt;&lt;li&gt;Used in case of a pre/mid/post-roll content&lt;/li&gt;&lt;/ul&gt;  |
| Broadcast Domain  | &lt;ul&gt;&lt;li&gt;(Optional) Broadcast domain, in case of an external broadcast&lt;/li&gt;&lt;/ul&gt; |
| Template Variables  | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with dot notation, for example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes&lt;/li&gt;&lt;/ul&gt; |
| Templates | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in message data&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |r

### Action - Send Media Pause Hit

#### Parameters

| **Parameter**  | **Description** |
|:-------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Unique Visitor ID  | &lt;ul&gt;&lt;li&gt;(Required) Must be unique for each visitor&lt;/li&gt;&lt;li&gt;See [XiTi by AT Internet&#39;s documentation](https://developers.atinternet-solutions.com/general-en/craft-your-hit/)&lt;/li&gt;&lt;/ul&gt;  |
| Content Label  | &lt;ul&gt;&lt;li&gt;One to three labels&lt;/li&gt;&lt;li&gt;Configure using an array attribute type or a single label can be specified as a scalar value&lt;/li&gt;&lt;/ul&gt;  |
| Media Type | &lt;ul&gt;&lt;li&gt;(Required) Select media type&lt;/li&gt;&lt;li&gt;Options are `Video`, `Audio`, `Pre-roll video`, `Mid-roll video`, `Post-roll video`&lt;/li&gt;&lt;/ul&gt;  |
| Broadcast Type | &lt;ul&gt;&lt;li&gt;(Required) Select broadcast type&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;Options are `Clip` or `Live`&lt;/li&gt;&lt;/ul&gt; |
| Content Duration | &lt;ul&gt;&lt;li&gt;Content duration in seconds is required for `Clip` Broadcast Type&lt;/li&gt;&lt;li&gt;Not applicable for live broadcast&lt;/li&gt;&lt;/ul&gt; |
| Broadcast Location | &lt;ul&gt;&lt;li&gt;(Required) Select broadcast type&lt;/li&gt;&lt;li&gt;Options are `internal` or `external`&lt;/li&gt;&lt;/ul&gt; |
| Content Level  | &lt;ul&gt;&lt;li&gt;(Optional) Must be configured ahead of time using XiTi website to retrieve the corresponding ID&lt;/li&gt;&lt;/ul&gt;  |
| Player identifier  | &lt;ul&gt;&lt;li&gt;(Optional) Useful when there are multiple players on the same page&lt;/li&gt;&lt;/ul&gt;  |
| Template Variables | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with dot notation, for example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes&lt;/li&gt;&lt;/ul&gt; |
| Templates  | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in message data&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Media Stop Hit

#### Parameters

| **Parameter**  | **Description**  |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Unique Visitor ID  | &lt;ul&gt;&lt;li&gt;(Required) Must be unique for each visitor&lt;/li&gt;&lt;li&gt;See [XiTi by AT Internet&#39;s documentation](https://developers.atinternet-solutions.com/general-en/craft-your-hit/)&lt;/li&gt;&lt;/ul&gt; |
| Content Label  | &lt;ul&gt;&lt;li&gt;One to three labels&lt;/li&gt;&lt;li&gt;Configure using an array attribute type or a single label can be specified as a scalar value&lt;/li&gt;&lt;/ul&gt; |
| Media Type | &lt;ul&gt;&lt;li&gt;(Required) Select media type&lt;/li&gt;&lt;li&gt;Options are `Video`, `Audio`, `Pre-roll video`, `Mid-roll video`, `Post-roll video`&lt;/li&gt;&lt;/ul&gt; |
| Broadcast Type | &lt;ul&gt;&lt;li&gt;(Required) Select broadcast type&lt;/li&gt;&lt;li&gt;Options are `Clip` or `Live`&lt;/li&gt;&lt;/ul&gt;  |
| Content Duration | &lt;ul&gt;&lt;li&gt;Content duration in seconds is required for `Clip` Broadcast Type&lt;/li&gt;&lt;li&gt;Not applicable for live broadcast&lt;/li&gt;&lt;/ul&gt;  |
| Broadcast Location | &lt;ul&gt;&lt;li&gt;(Required) Select broadcast type&lt;/li&gt;&lt;li&gt;Options are `internal` or `external`&lt;/li&gt;&lt;/ul&gt;  |
| Content Level  | &lt;ul&gt;&lt;li&gt;(Optional) Must be configured ahead of time using XiTi website to retrieve the corresponding ID&lt;/li&gt;&lt;/ul&gt; |
| Player identifier  | &lt;ul&gt;&lt;li&gt;(Optional) Useful when there are multiple players on the same page&lt;/li&gt;&lt;/ul&gt; |
| Template Variables | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with dot notation&lt;/li&gt;&lt;li&gt;For example, `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes&lt;/li&gt;&lt;/ul&gt; |
| Templates  | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in message data&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt;  |

### Action - Send Media Move Hit

#### Parameters

| **Parameter**  | **Description**  |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Unique Visitor ID  | &lt;ul&gt;&lt;li&gt;(Required) Must be unique for each visitor&lt;/li&gt;&lt;li&gt;See [XiTi by AT Internet&#39;s documentation](https://developers.atinternet-solutions.com/general-en/craft-your-hit/)&lt;/li&gt;&lt;/ul&gt; |
| Content Label  | &lt;ul&gt;&lt;li&gt;One to three labels&lt;/li&gt;&lt;li&gt;Configure using an array attribute type or a single label can be specified as a scalar value&lt;/li&gt;&lt;/ul&gt; |
| Media Type | &lt;ul&gt;&lt;li&gt;(Required) Select media type&lt;/li&gt;&lt;li&gt;Options are `Video`, `Audio`, Pre-roll video,` Mid-roll video`, `Post-roll video`&lt;/li&gt;&lt;/ul&gt; |
| Broadcast Type | &lt;ul&gt;&lt;li&gt;(Required) Select broadcast type&lt;/li&gt;&lt;li&gt;Options are `Clip` or `Live`&lt;/li&gt;&lt;/ul&gt;  |
| Content Duration | &lt;ul&gt;&lt;li&gt;Content duration in seconds is required for `Clip` Broadcast Type&lt;/li&gt;&lt;li&gt;Not applicable for live broadcast&lt;/li&gt;&lt;/ul&gt;  |
| Broadcast Location | &lt;ul&gt;&lt;li&gt;(Required) Select broadcast type&lt;/li&gt;&lt;li&gt;Options are `internal` or `external`&lt;/li&gt;&lt;/ul&gt;  |
| Content level  | &lt;ul&gt;&lt;li&gt;(Optional) Must be configured ahead of time using XiTi website to retrieve the corresponding ID&lt;/li&gt;&lt;/ul&gt; |
| Player identifier  | &lt;ul&gt;&lt;li&gt;(Optional) Useful when there are multiple players on the same page&lt;/li&gt;&lt;/ul&gt; |
| Template Variables | &lt;ul&gt;&lt;li(Optional) Provide template variables as data input for templates&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with dot notation For example: items.name&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes&lt;/li&gt;&lt;/ul&gt; |
| Templates  | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in message data&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt;  |