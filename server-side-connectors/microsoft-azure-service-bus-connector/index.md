---
title: Microsoft Azure Service Bus Connector Setup Guide
description: Microsoft Azure Service Bus is a cloud messaging service between applications and services. This article describes how to configure the service in the Customer Data Hub.
url: https://docs.tealium.com/server-side-connectors/microsoft-azure-service-bus-connector/
---
## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Event Data to Queue or Topic| ✗| ✓|
|Send Visitor Data to Queue or Topic| ✓| ✗|
|Send Customized Data to Queue or Topic| ✓| ✓|

## Requirements

* Microsoft Azure Account
* Service Bus Shared Access Policy Credentials
* Queue or Topic to send data to


## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

To configure your vendor, follow these steps:

1. In the Configure tab, provide a title for the Connector instance.

1. Enter Service Bus Namespace, Shared Access Policy Name and Key. For more information, see [Namespace &amp; Shared Access Policies](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-create-namespace-portal).

1. Click **Test Connection** to verify API connectivity with the provided credentials.


<blockquote>
Shared Access Policies can claim three type of permissions: `Send`, `Listen` and `Manage`. Provided policy must claim at least `Send` permission.
</blockquote>


## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. It's where you'll set up Actions to trigger.

This section describes how to set up Parameters and Options for each Action.

### Action - Send Event Data to Queue or Topic

#### Parameters

| Parameter | Description |
|---|---|
| Queue or Topic | (Required) Select a queue or topic option from this list. These options are available only if your configured policy is granted the **Manage** permission. If the permission is not granted, you must manually enter a queue/topic as a Custom Value. |
| User Properties | Map Attribute(s) to a message user property in the **To** dropdown (entered as a Custom Value). |
| Broker Properties | Map Attribute(s) to the message broker property of choice in the **To** dropdown. See available options below. |
| Print Attribute Names | Checking this box will display names for each event data Attribute in the message payload. |


<blockquote>
All Actions support Message User and Broker properties. They provide useful and convenient information about a message using key-value pairs. But they are set as HTTP headers and do not reside within the message body. For more information see [Message User & Broker Properties](https://docs.microsoft.com/en-us/rest/api/servicebus/message-headers-and-properties)
</blockquote>


#### Options - Broker Properties

|**Option**| **Description**|
|---| ---|
|Content Type| Sets HTTP header `Content-Type` for message consumers|
|Correlation ID| Unique identifier of the correlation|
|Session ID| Can be used to partition and route messages to particular consumers|
|Message ID| Overrides default auto-generated Message ID|
|Label| Application label|
|Reply To| Can be used to specify where to send a response for message consumers|
|Time to Live in Seconds| Expire message after X number of seconds (overrides queue/topic level)|
|To| Send to address|
|Scheduled Enqueued Time| Scheduled date and time at which the message is enqueued|
|Reply to Session ID| Similar to Reply To but targets a session for a response|
|Partition Key| Unique identifier of the partitioned queue or topic|

### Action - Send Visitor Data to Queue or Topic

#### Parameters

| Parameter | Description |
|---|---|
| Queue or Topic | (Required) Select a queue or topic option from this list. These options are available only if your configured policy is granted the **Manage** permission. If the permission is not granted, you must manually enter a queue/topic as a Custom Value. |
| User Properties | Map Attribute(s) to a message user property in the **To** dropdown (entered as a Custom Value). |
| Broker Properties | Map Attribute(s) to the message broker property of choice in the **To** dropdown. See available [Broker Properties](#options---broker-properties) options. |
| Include Current Visit Data With Visitor Data | Add the current visit data to the payload. This includes event visit data if Exclude Current Visit Event Data isn't selected. |
| Exclude Current Visit Event Data | Exclude event data from the current visit data. |
| Print Attribute Names | Checking this box will display names for each visitor data Attribute in the message payload. |

### Action - Send Customized Data to Queue or Topic (Advanced)

#### Parameters

| Parameter | Description |
|---|---|
| Queue or Topic | (Required) Select a queue or topic option from this list. These options are available only if your configured policy is granted the **Manage** permission. If the permission is not granted, you must manually enter a queue/topic as a Custom Value. |
| User Properties | Map Attribute(s) to a message user property in the **To** dropdown (entered as a Custom Value). |
| Broker Properties | Map Attribute(s) to the message broker property of choice in the **To** dropdown. See available [Broker Properties](#options---broker-properties) options. |
| Message Data | (Required) Construct a custom message body. Map Attribute(s) to names for simple one level JSON format, or reference a template name (surrounded in double curly braces) and select the **Custom Message Definition** option. |
| Template Variables | Map Attribute(s) to template variable names. Template variables are available for substitution and rendering of all templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/). |
| Templates | Provide one or more template to render. Typically, a single template is used to construct a message data. Refer to our [Templates Guide](https://docs.tealium.com/about-connector-templates/) for common syntax and extensions.For more information about common syntax and extensions, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/). |


<blockquote>
If necessary, templates can also be referenced and injected in user and broker properties.
</blockquote>


## Vendor Documentation

* [Namespace &amp; Shared Access Policies](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-create-namespace-portal)
* [Message User &amp; Broker Properties](https://docs.microsoft.com/en-us/rest/api/servicebus/message-headers-and-properties)