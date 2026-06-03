---
title: Datadog Connector Setup Guide
description: This article describes how to set up the Datadog connector.
url: https://docs.tealium.com/server-side-connectors/datadog-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **API Key**  
  Datadog API Key. To manage your API keys, [log in to Datadog](https://app.datadoghq.com/organization-settings/).
* **Host**  
  Set the Datadog host from which your Datadog API clients consume the APIs.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event | ✗ | ✓ |
| Send Log | ✗ | ✓ |
| Send Log (Batched) | ✗ | ✓ |
| Send Log Event | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Event

#### Event Parameters

Required parameters: 

| **Parameter** | **Description** |
| --- | --- |
| Text | The body of the event. Limited to 4000 characters. To use markdown in the event text, start the text block with `%%%` and end the text block with `%%%.` |
| Title | The event title. |
| Aggregation Key | An arbitrary string of up to 100 characters to use for aggregation. If you specify a key, all events using that key are grouped together in EventStream. |
| Alert Type | If an alert event is enabled, set its type. Allowed values: `error`, `warning`, `info`, `success`, `user_update`, `recommendation`, `snapshot`. |
| Date Happened | The POSIX timestamp of the event. Must be sent as an integer and limited to events no older than 18 hours. |
| Device Name | The device name. |
| Host | The hostname to associate with the event. Any tags associated with the host are also applied to this event. |
| Priority | The priority of the event. Allowed values: `normal` or `low`. |
| Related Event ID | The ID of the parent event. Must be sent as an integer. |
| Source Type Name | The type of event being posted. Option examples include: `nagios`, `hudson`, `jenkins`, `my_apps`, `chef`, `puppet`, `git`, `bitbucket`. For a complete list, see [Datadog: API Source Attributes](https://docs.datadoghq.com/integrations/faq/list-of-api-source-attribute-value/). |
| Tags | A list of tags to apply to the event. |

### Send Log

#### Log Parameters

Required Fields: 

| **Parameter** | **Description** |
| --- | --- |
| DD Source | The integration name associated with your log. When Datadog matches an integration name, it automatically installs the corresponding parsers and facets. For more information, see [Datadog: Reserved attributes](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes). |
| DD Tags | The tags associated with your log. |
| Hostname | The originating hostname of the log. |
| Service | The name of the application or service generating the log events. Used to switch from `Logs` to `APM`, so make sure you define the same value when you use both products. For more information, see [Datadog: Reserved attributes](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes). |

#### Log Message Parameters

The message [reserved attributes](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes) of your log. By default, Datadog ingests the value of the message attribute as the body of the log entry. That value is then highlighted and displayed in the log stream, where it is indexed for full text search.

The message is built based on the following format: `[TIMESTAMP] [SEVERITY] [SUBJECT] [CONTENT]`. To ignore this format, use the **Message Override** parameter.

| **Parameter** | **Description** |
| --- | --- |
| Message Override | Map this attribute to pass the entire message. This would override the `message` attribute. |
| Timestamp | The timestamp of the log. If this field is not populated, the current timestamp is used in the message. |
| Severity | The severity of the log, used in the message. |
| Subject | The subject of the log, used in the message. |
| Content | A shortened summary of the message body. |

### Send Log (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1,000
* Max time since oldest request: 15 minutes
* Max size of requests: 5 MB

#### Log Parameters

Required Fields: 

| **Parameter** | **Description** |
| --- | --- |
| DD Source | The integration name associated with your log. When Datadog matches an integration name, it automatically installs the corresponding parsers and facets. For more information, see [Datadog: Reserved attributes](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes). |
| DD Tags | The tags associated with your log. |
| Hostname | The originating hostname of the log. |
| Service | The name of the application or service generating the log events. Used to switch from `Logs` to `APM`, so make sure you define the same value when you use both products. For more information, see [Datadog: Reserved attributes](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes). |

#### Log Message Parameters

The message [reserved attributes](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes) of your log. By default, Datadog ingests the value of the message attribute as the body of the log entry. That value is then highlighted and displayed in the log stream, where it is indexed for full text search.

The message is built based on the following format: `[TIMESTAMP] [SEVERITY] [SUBJECT] [CONTENT]`. To ignore this format, use the **Message Override** parameter.

| **Parameter** | **Description** |
| --- | --- |
| Message Override | Map this attribute to pass the entire message. This would override the `message` attribute. |
| Timestamp | The timestamp of the log. If this field is not populated, the current timestamp is used in the message. |
| Severity | The severity of the log, used in the message. |
| Subject | The subject of the log, used in the message. |
| Content | A shortened summary of the message body. |

### Send Log Event

#### Log Parameters

Required Fields: 

| **Parameter** | **Description** |
| --- | --- |
| DD Source | The integration name associated with your log. When Datadog matches an integration name, it automatically installs the corresponding parsers and facets. For more information, see [Datadog: Reserved attributes](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes). |
| DD Tags | The tags associated with your log. |
| Hostname | The originating hostname of the log. |
| Service | The name of the application or service generating the log events. Used to switch from `Logs` to `APM`, so make sure you define the same value when you use both products. For more information, see [Datadog: Reserved attributes](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes). |

#### Log Message Parameters

The message [reserved attributes](https://docs.datadoghq.com/logs/log_configuration/attributes_naming_convention/#reserved-attributes) of your log. By default, Datadog ingests the value of the message attribute as the body of the log entry. That value is then highlighted and displayed in the log stream, where it is indexed for full text search.

The message is built based on the following format: `[TIMESTAMP] [SEVERITY] [SUBJECT] [CONTENT]`. To ignore this format, use the **Message Override** parameter.

| **Parameter** | **Description** |
| --- | --- |
| Message Override | Map this attribute to pass the entire message. This would override the `message` attribute. |
| Timestamp | The timestamp of the log. If this field is not populated, the current timestamp is used in the message. |
| Severity | The severity of the log, used in the message. |
| Subject | The subject of the log, used in the message. |
| Content | A shortened summary of the message body. |