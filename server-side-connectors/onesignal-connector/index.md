---
title: OneSignal Connector Setup Guide
description: This article describes how to set up the OneSignal connector.
url: https://docs.tealium.com/server-side-connectors/onesignal-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Push Notification Based on Player ID| ✓| ✗|
|Send Email Based on Player ID| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **REST API Key**
  * Your REST API key for app-specific operations (getting users of an app, modifying users, getting notifications, sending notifications) listed in the Keys &amp; IDs section.
  * For more information, see: [OneSignal Team and Keys](https://documentation.onesignal.com/docs/accounts-and-keys#section-keys-ids).

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Push Notification Based on Player ID

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|App ID|  <ul><li>Your OneSignal application ID, which can be found in Keys &amp; IDs.</li><li>For more information, see: [create notification](https://documentation.onesignal.com/reference#create-notification).</li></ul> |
|Player ID| Specific player to send your notification to.|
|Template ID| ID of the Push template in your OneSignal account.|

### Action - Send Email Based on Player ID

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|App ID|  <ul><li>Your OneSignal application ID, which can be found in Keys &amp; IDs.</li><li>For more information, see: [create notification](https://documentation.onesignal.com/reference#create-notification).</li></ul> |
|Player ID| Specific player to send your notification to.|
|Email Subject| Subject of the email.|
|Email Body| Body of the email.|
