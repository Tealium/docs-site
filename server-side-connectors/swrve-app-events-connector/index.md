---
title: Swrve App Events Connector Setup Guide
description: This article describes how to set up the Swrve connector.
url: https://docs.tealium.com/server-side-connectors/swrve-app-events-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Event| ✓| ✓|
|Update User| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Application ID**
  * (Required) Can be viewed on the **Integration Settings** screen of your Swrve application.

* **API Key Type**
  * (Required) Select applicable API key type.
  * For more information, see: [Managing your API Keys](https://docs.swrve.com/getting-started/integrate-your-app/#Managing_your_API_keys).

* **API Key**
  * (Required) Provide API key-value.

* **Region**
  * (Required) Select applicable data center region.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|User ID|  <ul><li>(Required) Unique user identifier the event relates to.</li></ul> |
|Event Name|  <ul><li>(Required) String</li><li>The name of the event.</li><li>Example: `app_started`</li><li>The name can use dot notation to indicate a hierarchy.</li><li>The name must contain only letters, numbers, dashes, underscores, and dots.</li><li>The first string of valid characters is taken as the event name.</li><li>For example, if the name **level.start/** is supplied, it is interpreted as `level.start` .</li></ul> |
|App Version|  <ul><li>The version of the application that the user is currently using.</li></ul> |
|Custom Payload|  <ul><li>Map attributes to Custom Payload pairs.</li><li>For more information, see: [Custom Payload Guide](https://docs.swrve.com/swrves-apis/api-guides/events-api-payloads-guide/).</li></ul> |

### Action - Update User

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|User ID|  <ul><li>(Required) Unique user identifier the event relates to.</li></ul> |
|User Initiated|  <ul><li>If specified as `false`, then event does not count towards some performance indicators.</li><li>If property has any other value or is not specified, then event counts towards all performance indicators as normal.</li></ul> |
|App Version|  <ul><li>The version of the application that the user is currently using.</li></ul> |
|Custom Payload|  <ul><li>Map attributes to Custom Payload pairs.</li><li>For more information, see: [Custom Payload Guide](https://docs.swrve.com/swrves-apis/api-guides/events-api-payloads-guide/).</li></ul> |
