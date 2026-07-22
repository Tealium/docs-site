---
title: Microsoft Azure Event Hubs Connector Setup Guide
description: Microsoft Azure Event Hubs is a cloud service for receiving and processing high volume of events. This article describes how to configure the service in your Customer Data Hub profile.
url: https://docs.tealium.com/server-side-connectors/microsoft-azure-event-hubs-connector/
---## Connector actions

|**Action Name**| **Trigger on Audience**| **Trigger on Streams**|
|---| ---| ---|
|Send Event Data to Event Hub| ✗| ✓|
|Send Visitor Data to Event Hub| ✓| ✗|
|Send Customized Data to Event Hub| ✓| ✓|

## Requirements

* A Microsoft Azure Account
* Service Bus Shared Access Policy credentials
* The name of an Event Hub to send data to

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

To configure your vendor, follow these steps:

1. In the **Configure** tab, provide a title for the connector instance.

1. Sign in to the Azure Portal and create an Event Hubs Namespace, Shared Access Policy Name and Key. Then create an Event Hub. For more information, see: [Create an Event Hubs namespace and an event hub using the Azure portal](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create).

1. Use the Event Hub namespace, Shared Access Policy and Shared Access Key to configure the connector.

1. Click **Test Connection** to verify API connectivity with the provided credentials.


<blockquote>
Shared Access Policies can claim three type of permissions: `Send`, `Listen` and `Manage`. Provided policy must claim at least `Send` permission.
</blockquote>


## Action settings — parameters and options

Click **Next** or go to the **Actions** tab. It's where you'll set up actions to trigger.

This section describes how to set up parameters and options for each action.

### Action — Send Event Data to Event Hub

#### Parameters

| Parameter | Description |
|---|---|
| Event Hub | (Required) Select an event hub from this list. These options are available only if your configured policy is granted the **Manage** permission. If the permission is not granted, you must manually enter an event hub as a custom value. |
| User Properties | Map attribute(s) to a message user property in the **To** dropdown (entered as a custom value). |
| Broker Properties | Map attribute(s) to the message broker property of choice in the **To** dropdown. See available options below. |
| Print Attribute Names | Checking this box will display names for each event data attribute in the message payload. |


<blockquote>
All actions support Message User and Broker properties. They provide useful and convenient information about a message using key-value pairs. But, they are set as HTTP headers and do not reside within the message body. For more information, see: [Message User &amp; Broker Properties](https://docs.microsoft.com/en-us/rest/api/servicebus/message-headers-and-properties).
</blockquote>


#### Options — Broker Properties

|**Option**| **Description**|
|---| ---|
|Content Type| Sets HTTP header `Content-Type` for message consumers|
|Correlation ID| Unique identifier of the correlation|
|Session ID| Can be used to partition and route messages to particular consumers|
|Message ID| Overrides default auto-generated Message ID|
|Label| Application label|
|Reply To| Can be used to specify where to send a response for message consumers|
|Time to Live in Seconds| Expire message after X number of seconds (overrides Event Hub level)|
|To| Send to address|
|Scheduled Enqueued Time| Scheduled date and time at which the message is enqueued|
|Reply to Session ID| Similar to Reply To but targets a session for a response|
|Partition Key| Unique identifier of the partitioned event hub|

### Action – Send Visitor Data to Event Hub

#### Parameters

| Parameter | Description |
|---|---|
| Event Hub | (Required) Select an event hub from this list. These options are available only if your configured policy is granted the **Manage** permission. If the permission is not granted, you must manually enter an event hub as a custom value. |
| User Properties | Map attribute(s) to a message user property in the **To** dropdown (entered as a custom value). |
| Broker Properties | Map attribute(s) to the message broker property of choice in the **To** dropdown. See available [Broker Properties](#options---broker-properties) options. |
| Include Current Visit Data With Visitor Data | Add the current visit data to the payload. This includes event visit data if Exclude Current Visit Event Data isn't selected. |
| Exclude Current Visit Event Data | Exclude event data from the current visit data. |
| Print Attribute Names | Checking this box will display names for each visitor data attribute in the message payload. |

### Action — Send Customized Data to Event Hub (Advanced)

#### Parameters

| Parameter | Description |
|---|---|
| Event Hub |(Required) Select an event hub from this list. These options are available only if your configured policy is granted the **Manage** permission. If the permission is not granted, you must manually enter an event hub as a custom value. |
| User Properties | Map attribute(s) to a message user property in the **To** dropdown (entered as a custom value). |
| Broker Properties | Map attribute(s) to the message broker property of choice in the **To** dropdown. See available [Broker Properties](#options---broker-properties) options. |
| Message Data | (Required) Construct a custom message body. Map attribute(s) to names for a simple one-level JSON format, or reference a template name (surrounded in double curly braces) and select the **Custom Message Definition** option. |
| Template Variables | Map attribute(s) to template variable names. Template variables are available for substitution and rendering of all templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/). |
| Templates | Provide one or more template to render. Typically, a single template is used to construct message data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).|


<blockquote>
If necessary, templates can also be referenced and injected in user and broker properties.
</blockquote>


## Vendor documentation

* [What is Azure Event Hubs?](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-what-is-event-hubs)
* [Create an Event Hubs namespace and an event hub using the Azure portal](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create)
* [Generate SAS token](https://docs.microsoft.com/en-us/rest/api/eventhub/generate-sas-token)
* [Common parameters and headers](https://docs.microsoft.com/en-us/rest/api/eventhub/event-hubs-runtime-rest)
* [Message User and Broker Properties](https://docs.microsoft.com/en-us/rest/api/servicebus/message-headers-and-properties)
* [List Event Hubs](https://docs.microsoft.com/en-us/rest/api/eventhub/list-event-hubs)
* [Send event to Event Hubs](https://docs.microsoft.com/en-us/rest/api/eventhub/send-event)