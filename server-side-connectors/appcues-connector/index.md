---
title: Appcues Connector Setup Guide
description: This article describes how to set up the Appcues connector.
url: https://docs.tealium.com/server-side-connectors/appcues-connector/
---## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Update User Profile| ✓| ✗|
|Record User Event| ✗| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Account ID**
  * Your Appcues Account ID.
  * Found on the account settings page.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Update User Profile

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|User ID|  <ul><li>The end user ID of the profile to update.</li></ul> |
|Properties|  <ul><li>Object containing arbitrary key-value data to update in the user's stored profile.</li><li>For more information, see: [Appcues HTTP API (Developer)](http://docs.appcues.com/article/254-http-api).</li></ul> |

### Action - Record User Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|User ID|  <ul><li>The end user ID of the profile to update.</li></ul> |
|Event Name|  <ul><li>Event name.</li><li>Maximum of 127 characters.</li><li>This is the main mechanism for grouping and targeting on specific events.</li><li>For more information, see: [Appcues HTTP API (Developer)](http://docs.appcues.com/article/254-http-api).</li></ul> |
|Timestamp|  <ul><li>Time at which the event occurred.</li><li>Either integer format (as Unix time) or string format (as ISO 8601 compliant date, for example **2016-01-13T13:05:22.000Z**).</li></ul> |
|Event Attributes|  <ul><li>Event attributes</li></ul> |
