---
title: Confluent Kafka Connect Connector Setup Guide
description: This article describes how to set up the Confluent Kafka Connect connector.
url: https://docs.tealium.com/server-side-connectors/confluent-kafka-connect-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Confluent REST Proxy for Kafka
* API Version: v3
* API Endpoint: `https://github.com/confluentinc/kafka-rest`

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **API Key**: (Required) Your Confluent Cloud API key.
* **API Secret**: (Required) Your Confluent Cloud API secret.
* **Bootstrap Server**: (Required) The hostname of your Confluent Cloud Kafka REST endpoint, without the protocol or port. For example, if your endpoint is `https://pkc-12345.us-west4.gcp.confluent.cloud:443`, enter `pkc-12345.us-west4.gcp.confluent.cloud`.
* **Cluster ID**: (Required) Your Confluent Cloud cluster ID (for example, `lkc-12345`).

For more information on these settings, see:
* [Confluent Cloud: Use API Keys to Authenticate to Confluent Cloud](https://docs.confluent.io/cloud/current/security/authenticate/workload-identities/service-accounts/api-keys/overview.html)
* [Confluent Cloud Clusters: How do I view cluster details with Cloud Console?](https://docs.confluent.io/cloud/current/clusters/cluster-faq.html#how-do-i-view-cluster-details-with-ccloud-console-short)

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Entire Event Data | ✗ | ✓ |
| Send Custom Event Data | ✗ | ✓ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Custom Visitor Data | ✓ | ✗ |
| Send Log Event | ✗ | ✓ |
| Send Entire Log Event | ✗ | ✓ |

Enter a name for the action and select the action type.

The following section describes how to set up parameters and options for each action.

### Send Entire Event Data

#### Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100
* Max time since oldest request: 60 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Topic ID | Select the topic or enter the Topic ID. |
| Partition ID | Select the Partition ID. |
| Data format | Specify the format for data delivery. Possible values: `JSON`, `STRING`, or `BINARY`. |
| Headers | Optional parameters. A set of key-value pairs listing the header properties and values. |
| Message key | Specify the raw message key. If you chose `BINARY` as the data format, Tealium encodes this value before sending it. |
| Timestamp | The topic timestamp in ISO 8601 UTC format. For example, `YYYY-MM-DDThh:mm:ssZ`. If no timestamp is provided, the current timestamp will be used. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between 1 and 60 minutes. The default value is 60 minutes. |
| Print Attribute Names | By default, the attribute IDs are used as key names. If you want to use the attribute names as key names instead, enable this checkbox. If the attribute names are updated, the key names in the payload will be updated. |
| Enable Streaming Mode | Enable this option to use the Confluent streaming API when sending records, which can improve efficiency for high-volume traffic but does not change when events are sent to Confluent. |

### Send Custom Event Data

#### Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100
* Max time since oldest request: 60 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Topic ID | Select the topic or enter the Topic ID. |
| Partition ID | Select the Partition ID. |
| Data format | Specify the format for data delivery. Possible values: `JSON`, `STRING`, or `BINARY`. |
| Headers | Optional parameters. A set of key-value pairs listing the header properties and values. |
| Message key | Specify the raw message key. If you chose `BINARY` as the data format, Tealium encodes this value before sending it. |
| Timestamp | The topic timestamp in ISO 8601 UTC format. For example, `YYYY-MM-DDThh:mm:ssZ`. If no timestamp is provided, the current timestamp will be used. |

#### Message data

| **Parameter** | **Description** |
| --- | --- |
| Template Variables | Provide template variables as data input for templates.<br>For more information and usage examples, see [Template Variables Guide](https://docs.tealium.com/server-side/connectors/webhook-connectors/template-variables/).<br>Name nested template variables with the dot notation. For example: `items.name.`<br>Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in message data. For more information, see [Templates Guide](https://docs.tealium.com/server-side/connectors/webhook-connectors/trimou-templating-engine/).<br>Templates are injected by name with double curly braces into supported fields. For example: `{{SomeTemplateName}}`. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `60` minutes. |
| Enable Streaming Mode | Enable this option to use the Confluent streaming API when sending records, which can improve efficiency for high-volume traffic but does not change when events are sent to Confluent. |

### Send Entire Visitor Data

#### Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100
* Max time since oldest request: 60 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Topic ID | Select the topic or enter the Topic ID. |
| Partition ID | Select the Partition ID. |
| Data format | Specify the format for data delivery. Possible values: `JSON`, `STRING`, or `BINARY`. |
| Headers | Optional parameters. A set of key-value pairs listing the header properties and values. |
| Message key | Specify the raw message key. If you chose `BINARY` as the data format, Tealium encodes this value before sending it. |
| Timestamp | The topic timestamp in ISO 8601 UTC format. For example, `YYYY-MM-DDThh:mm:ssZ`. If no timestamp is provided, the current timestamp will be used. |
| Print Attribute Names | By default, the attribute IDs are used as key names. If you want to use the attribute names as key names instead, enable this checkbox. If the attribute names are updated, the key names in the payload will be updated. |
| Include Current Visit Data With Visitor Data | Add the current visit data to the payload. This includes event visit data, unless Exclude Current Visit Event Data is checked. |
| Exclude Current Visit Event Data | Exclude event data from the current visit data. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `60` minutes. |

### Send Custom Visitor Data

#### Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100
* Max time since oldest request: 60 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Topic ID | Select the topic or enter the Topic ID. |
| Partition ID | Select the Partition ID. |
| Data format | Specify the format for data delivery. Possible values: `JSON`, `STRING`, or `BINARY`. |
| Headers | Optional parameters. A set of key-value pairs listing the header properties and values. |
| Message key | Specify the raw message key. If you chose `BINARY` as the data format, Tealium encodes this value before sending it. |
| Timestamp | The topic timestamp in ISO 8601 UTC format. For example, `YYYY-MM-DDThh:mm:ssZ`. If no timestamp is provided, the current timestamp will be used. |

#### Message data

| **Parameter** | **Description** |
| --- | --- |
| Template Variables | Provide template variables as data input for templates.<br>For more information and usage examples, see [Template Variables Guide](https://docs.tealium.com/server-side/connectors/webhook-connectors/template-variables/).<br>Name nested template variables with the dot notation. For example: `items.name.`<br>Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in message data. For more information, see [Templates Guide](https://docs.tealium.com/server-side/connectors/webhook-connectors/trimou-templating-engine/).<br>Templates are injected by name with double curly braces into supported fields. For example: `{{SomeTemplateName}}`. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `60` minutes. |

### Send Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Topic ID | Select the topic or enter the Topic ID. |
| Partition ID | Select the Partition ID. |
| Data format | Specify the format for data delivery. Possible values: `JSON`, `STRING`, or `BINARY`. |
| Headers | Optional parameters. A set of key-value pairs listing the header properties and values. |
| Message key | Specify the raw message key. If you chose `BINARY` as the data format, Tealium encodes this value before sending it. |
| Timestamp | The topic timestamp in ISO 8601 UTC format. For example, `YYYY-MM-DDThh:mm:ssZ`. If no timestamp is provided, the current timestamp will be used. |

#### Message data

| **Parameter** | **Description** |
| --- | --- |
| Template Variables | Provide template variables as data input for templates.<br>For more information and usage examples, see [Template Variables Guide](https://docs.tealium.com/server-side/connectors/webhook-connectors/template-variables/).<br>Name nested template variables with the dot notation. For example: `items.name.`<br>Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in message data. For more information, see [Templates Guide](https://docs.tealium.com/server-side/connectors/webhook-connectors/trimou-templating-engine/).<br>Templates are injected by name with double curly braces into supported fields. For example: `{{SomeTemplateName}}`. |

### Send Entire Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Topic ID | Select the topic or enter the Topic ID. |
| Partition ID | Select the Partition ID. |
| Data format | Specify the format for data delivery. Possible values: `JSON`, `STRING`, or `BINARY`. |
| Headers | Optional parameters. A set of key-value pairs listing the header properties and values. |
| Message key | Specify the raw message key. If you chose `BINARY` as the data format, Tealium encodes this value before sending it. |
| Timestamp | The topic timestamp in ISO 8601 UTC format. For example, `YYYY-MM-DDThh:mm:ssZ`. If no timestamp is provided, the current timestamp will be used. |