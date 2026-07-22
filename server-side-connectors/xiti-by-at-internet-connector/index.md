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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **URL**
  * (Required) Provide your Collection server's full hit URL to submit request to.
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
| Comp  | <ul><li>(Required) Must be unique for each visitor</li><li>See [XiTi by AT Internet's documentation](https://developers.atinternet-solutions.com/general-en/craft-your-hit/)</li></ul> |
| Page  | <ul><li>(Required) The name of the page accessed</li><li>No longer than 250 characters</li></ul> |
| Chapters  | <ul><li>One to three chapters</li><li>Configure using an array attribute type</li></ul>  |
| Level 2 | <ul><li>Must be configured ahead of time in the interface to retrieve the corresponding ID</li></ul>  |
| Additional Hit Parameters | <ul><li>Provide additional values if needed</li><li>Template Support: To use a template, configure templates and template variables sections below and then reference the template enclosing its name into double curly braces, for example: `{{MyTemplateName}}`</li></ul>  |
| Template Variables  | <ul><li>(Optional) Provide template variables as data input for templates</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with dot notation.</li><li>For example, `items.name`</li><li>Nested template variables are typically built from data layer list attributes</li></ul> |
| Templates | <ul><li>(Optional) Provide templates to be referenced in message data</li><li>>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.</li></ul>  |

### Action - Send Media Play Hit

#### Parameters

| **Parameter** | **Description**  |
|:------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Unique Visitor ID | <ul><li>(Required) Must be unique for each visitor</li><li>See [XiTi by AT Internet's documentation](https://developers.atinternet-solutions.com/general-en/craft-your-hit/)</li></ul> |
| Content Label | <ul><li>One to three labels</li><li>Configure using an array attribute type, or a single label can be specified as a scalar value</li></ul>  |
| Media Type  | <ul><li>(Required) Select media type</li><li>Options are `Video`, `Audio`,` Pre-roll video`, `Mid-roll video`, `Post-roll video`</li></ul> |
| Broadcast Type  | <ul><li>(Required) Select broadcast type</li><li>Options are `Clip` or `Live`</li></ul>  |
| Content Duration  | <ul><li>Content duration in seconds is required for `Clip` Broadcast Type</li><li>Not applicable for live broadcast</li></ul>  |
| Broadcast Location  | <ul><li>(Required) Select broadcast type</li><li>Options are `internal` or `external`</li></ul>  |
| Content Level | <ul><li>(Optional) Must be configured ahead of time using XiTi website to retrieve the corresponding ID</li></ul> |
| Content buffering | <ul><li>(Optional) Set `1` while buffering,  at the end of the buffering</li></ul> |
| Page Label  | <ul><li>(Optional) Label of the page where the content is played (with optional tree structure)</li></ul>  |
| Page Level 2  | <ul><li>(Optional) Level 2 of the page where the content is played</li></ul> |
| Player Identifier | <ul><li>(Optional) Useful when there are multiple players on the same page</li></ul> |
| Label of linked content | <ul><li>(Optional) Includes tree structure if any; used in case of a pre/mid/post-roll content</li></ul> |
| Broadcast Domain  | <ul><li>Optional</li></ul> <ul><li>Broadcast domain, in case of an external broadcast</li></ul>  |
| Template Variables  | <ul><li>(Optional) Provide template variables as data input for templates</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with dot notation</li><li>For example, `items.name`</li><li>Nested template variables are typically built from data layer list attributes</li></ul> |
| Templates | <ul><li>(Optional) Provide templates to be referenced in message data</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.</li></ul>  |

### Action - Send Media Refresh Hit

#### Parameters

| **Parameter** | **Description** |
|:----------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Unique Visitor ID | <ul><li>(Required) Must be unique for each visitor</li><li>See [XiTi by AT Internet's documentation](https://developers.atinternet-solutions.com/general-en/craft-your-hit/)</li></ul>  |
| Content Label | <ul><li>One to three labels</li><li>Configure using an array attribute type or a single label can be specified as a scalar value</li></ul>  |
| Media Type  | <ul><li>(Required) Select media type</li><li>Options are `Video`, `Audio`, `Pre-roll video`, `Mid-roll video`, `Post-roll video`</li></ul>  |
| Broadcast Type  | <ul><li>(Required) Select broadcast type</li><li>Options are `Clip` or `Live`</li></ul> |
| Content Duration  | <ul><li>Content duration in seconds is required for `Clip` Broadcast Type</li><li>Not applicable for live broadcast</li></ul> |
| Broadcast Location  | <ul><li>(Required) Select broadcast type</li><li>Options are `internal` or `external`</li></ul> |
| Content Level | <ul><li>(Optional) Must be configured ahead of time using XiTi website to retrieve the corresponding ID</li></ul>  |
| Content Buffering | <ul><li>(Optional) Set `1` while buffering,  at the end of the buffering</li></ul>  |
| Page Level 2  | <ul><li>(Optional) Level 2 of the page where the content is played</li></ul>  |
| Player Identifier | <ul><li>(Optional) Useful when there are multiple players on the same page</li></ul>  |
| Label of the Linked Content | <ul><li>(Optional) Includes tree structure, if any</li><li>Used in case of a pre/mid/post-roll content</li></ul>  |
| Broadcast Domain  | <ul><li>(Optional) Broadcast domain, in case of an external broadcast</li></ul> |
| Template Variables  | <ul><li>(Optional) Provide template variables as data input for templates</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with dot notation, for example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes</li></ul> |
| Templates | <ul><li>(Optional) Provide templates to be referenced in message data</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.</li></ul> |r

### Action - Send Media Pause Hit

#### Parameters

| **Parameter**  | **Description** |
|:-------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Unique Visitor ID  | <ul><li>(Required) Must be unique for each visitor</li><li>See [XiTi by AT Internet's documentation](https://developers.atinternet-solutions.com/general-en/craft-your-hit/)</li></ul>  |
| Content Label  | <ul><li>One to three labels</li><li>Configure using an array attribute type or a single label can be specified as a scalar value</li></ul>  |
| Media Type | <ul><li>(Required) Select media type</li><li>Options are `Video`, `Audio`, `Pre-roll video`, `Mid-roll video`, `Post-roll video`</li></ul>  |
| Broadcast Type | <ul><li>(Required) Select broadcast type</li></ul> <ul><li>Options are `Clip` or `Live`</li></ul> |
| Content Duration | <ul><li>Content duration in seconds is required for `Clip` Broadcast Type</li><li>Not applicable for live broadcast</li></ul> |
| Broadcast Location | <ul><li>(Required) Select broadcast type</li><li>Options are `internal` or `external`</li></ul> |
| Content Level  | <ul><li>(Optional) Must be configured ahead of time using XiTi website to retrieve the corresponding ID</li></ul>  |
| Player identifier  | <ul><li>(Optional) Useful when there are multiple players on the same page</li></ul>  |
| Template Variables | <ul><li>(Optional) Provide template variables as data input for templates.</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with dot notation, for example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes</li></ul> |
| Templates  | <ul><li>(Optional) Provide templates to be referenced in message data</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.</li></ul> |

### Action - Send Media Stop Hit

#### Parameters

| **Parameter**  | **Description**  |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Unique Visitor ID  | <ul><li>(Required) Must be unique for each visitor</li><li>See [XiTi by AT Internet's documentation](https://developers.atinternet-solutions.com/general-en/craft-your-hit/)</li></ul> |
| Content Label  | <ul><li>One to three labels</li><li>Configure using an array attribute type or a single label can be specified as a scalar value</li></ul> |
| Media Type | <ul><li>(Required) Select media type</li><li>Options are `Video`, `Audio`, `Pre-roll video`, `Mid-roll video`, `Post-roll video`</li></ul> |
| Broadcast Type | <ul><li>(Required) Select broadcast type</li><li>Options are `Clip` or `Live`</li></ul>  |
| Content Duration | <ul><li>Content duration in seconds is required for `Clip` Broadcast Type</li><li>Not applicable for live broadcast</li></ul>  |
| Broadcast Location | <ul><li>(Required) Select broadcast type</li><li>Options are `internal` or `external`</li></ul>  |
| Content Level  | <ul><li>(Optional) Must be configured ahead of time using XiTi website to retrieve the corresponding ID</li></ul> |
| Player identifier  | <ul><li>(Optional) Useful when there are multiple players on the same page</li></ul> |
| Template Variables | <ul><li>(Optional) Provide template variables as data input for templates</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with dot notation</li><li>For example, `items.name`</li><li>Nested template variables are typically built from data layer list attributes</li></ul> |
| Templates  | <ul><li>(Optional) Provide templates to be referenced in message data</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.</li></ul>  |

### Action - Send Media Move Hit

#### Parameters

| **Parameter**  | **Description**  |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Unique Visitor ID  | <ul><li>(Required) Must be unique for each visitor</li><li>See [XiTi by AT Internet's documentation](https://developers.atinternet-solutions.com/general-en/craft-your-hit/)</li></ul> |
| Content Label  | <ul><li>One to three labels</li><li>Configure using an array attribute type or a single label can be specified as a scalar value</li></ul> |
| Media Type | <ul><li>(Required) Select media type</li><li>Options are `Video`, `Audio`, Pre-roll video,` Mid-roll video`, `Post-roll video`</li></ul> |
| Broadcast Type | <ul><li>(Required) Select broadcast type</li><li>Options are `Clip` or `Live`</li></ul>  |
| Content Duration | <ul><li>Content duration in seconds is required for `Clip` Broadcast Type</li><li>Not applicable for live broadcast</li></ul>  |
| Broadcast Location | <ul><li>(Required) Select broadcast type</li><li>Options are `internal` or `external`</li></ul>  |
| Content level  | <ul><li>(Optional) Must be configured ahead of time using XiTi website to retrieve the corresponding ID</li></ul> |
| Player identifier  | <ul><li>(Optional) Useful when there are multiple players on the same page</li></ul> |
| Template Variables | <ul><li(Optional) Provide template variables as data input for templates</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with dot notation For example: items.name</li><li>Nested template variables are typically built from data layer list attributes</li></ul> |
| Templates  | <ul><li>(Optional) Provide templates to be referenced in message data</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.</li></ul>  |