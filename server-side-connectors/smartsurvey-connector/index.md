---
title: SmartSurvey Connector Setup Guide
description: This article describes how to set up the SmartSurvey connector.
url: https://docs.tealium.com/server-side-connectors/smartsurvey-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add Contact to List| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/server-side/connectors/manage/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Token**
  * The API token and token secret must be passed with each request. \\
  * For more information, see: [SmartSurvey: Getting Started](https://docs.smartsurvey.io/docs)

* **API Token Secret**
  * The API token and token secret must be passed with each request.
  * For more information, see: [SmartSurvey: Getting Started](https://docs.smartsurvey.io/docs)

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Add Contact to List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact list ID|  <ul><li>The unique ID for the contact list.</li><li>For more information, see: [SmartSurvey's documentation](https://docs.smartsurvey.io/v1/reference#contactlists_contacts_insert)</li></ul> |
|Email|  <ul><li>The email address for the contact.</li></ul> |
|Name|  <ul><li>The name of the contact.</li></ul> |
|Custom Fields|  <ul><li>Custom data fields pertaining to the contact.</li></ul> |
