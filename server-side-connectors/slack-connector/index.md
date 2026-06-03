---
title: Slack Connector Setup Guide
description: Slack brings all your communication together in one place. With this integration, automated messages can be posted to any conversation. This article describes how to set up the Slack connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/slack-connector/
---
### Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Post Channel Message| ✓| ✓|
|Post Enhanced Message in Channel| ✓| ✓|

### Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](/server-side/connectors/manage/) article.

After adding the connector, there are no settings to configure. Click **Done** to proceed to the next step.

### Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

#### Action — Post Channel Message

##### Parameters

|**Parameter**| **Description**|
|---| ---|
|Webhook URL from App| Your Webhook URL generated through the App.&lt;br&gt; For more information, see: [Getting started with Incoming Webhooks](https://api.slack.com/messaging/webhooks#getting_started).|
|Message| The message to send to the channel associated with the webhook URL specified above. Learn more about [Slack message formatting](https://api.slack.com/docs/message-formatting).|

#### Action — Post Enhanced Message in Channel

##### Parameters

|**Parameter**| **Description**|
|---| ---|
|Webhook URL from App| Your Webhook URL generated through the App.&lt;br&gt; For more information, see: [Getting started with Incoming Webhooks](https://api.slack.com/messaging/webhooks#getting_started).|
|Blocks Template Variables| Provide template variables as data input for Blocks. For more information, see .&lt;br&gt; Name nested template variables with the dot notation (For example, `items.name`).&lt;br&gt; Nested template variables are typically built from data layer list attributes.|
|Blocks| Block Kit visual components to enhance message.&lt;br&gt; Provide an array template for the **blocks** array to be sent.&lt;br&gt; You can use template variables. For more information, see .|
|Message| The message to send to the channel associated with the webhook URL specified above. Learn more about [Slack message formatting](https://api.slack.com/docs/message-formatting).|