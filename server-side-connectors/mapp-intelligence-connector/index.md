---
title: Mapp Intelligence Connector (previously called Webtrekk) Setup Guide
description: This article describes how to set up the Mapp Intelligence connector.
url: https://docs.tealium.com/server-side-connectors/mapp-intelligence-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Pixel| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Track Domain**
  * (Required) Defined by Mapp, for example: ` track.webtrekk.net`

* **Mapp Intelligence Tracking ID**
  * (Required) Defined by Mapp, for example: `111111111111111`

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Pixel

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Client Time|
|Color Depth|
|Content ID|
|Cookies Activated|
|Java Activated|
|Javascript Enabled|
|Monitor Resolution|
|Referrer URL|
|Version|
|Window Size|
|Custom Ever-ID|
|Ever-ID|
|Referer|
|User Agent|
|User IP|
|E-Commerce Product Parameters|  <ul><li>Map array and list values to keys to be passed to Mapp.</li><li>All arrays and lists should be of equal length.</li><li>Single value attributes will be expanded to an array which is the same length as all other arrays, repeating the value.</li><li>For a list of parameters that can be sent to Webtrekk, see [Overview Tracking Parameters and JavaScript Keys](https://docs.mapp.com/docs/which-parameters-can-be-sent-to-mapp-intelligence)</li></ul> |
|Template Variables|  <ul><li>Provide template variables for message data.</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation, for example: `items.name`.</li><li>Nested template variables are typically built from data layer list attributes</li></ul> |
|Templates|  <ul><li>(Optional) Provide templates to be referenced in query parameters.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/)./li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li></ul> |