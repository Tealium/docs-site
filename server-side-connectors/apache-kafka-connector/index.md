---
title: Apache Kafka Connector Setup Guide
description: This article describes how to set up the Apache Kafka connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/apache-kafka-connector/
---
## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Bootstrap Server**
  * (Required) Kafka bootstrap server for your endpoint (for example, a Conduktor Gateway host or direct Kafka broker: `gateway.customer-domain.com:6969`). This must point to an endpoint reachable from Tealium, typically via PrivateLink, VPN, or peering.
* **CA Certificate (PEM)**
  * Trust anchor to validate the TLS certificate presented by the Kafka broker or Gateway. PEM-encoded CA chain. Required only for internal PKI, private CA, or self-signed certificates.
* **Disable Hostname Verification**
  * Toggle Kafka client hostname verification. Disable this setting if you use SNI or non-standard hostnames. Default: verification enabled.
* **Confluent Schema Registry URL**
  * (Optional) The URL of the Schema Registry (for example, `https://schema-registry.example.com:8081`). Required when using schema validation with custom actions.
* **Confluent Schema Registry Username**
  * (Optional) The username used to authenticate with the Schema Registry via HTTP Basic authentication. Required if your Schema Registry enforces authentication.
* **Confluent Schema Registry Password**
  * (Optional) The password or API secret used to authenticate with the Schema Registry via HTTP Basic authentication. Required if your Schema Registry enforces authentication.
* **Service Account Username**
  * (Required) Kafka principal used to authenticate with SASL/PLAIN.
* **Service Account Token / Password**
  * (Required) JWT token or equivalent credential for the service account principal.
* **Compression Type**
  * Compression algorithm for messages sent to Kafka. Reduces bandwidth and storage costs. If left blank, GZIP is used.
* **Maximum Message Size (bytes)**
  * The maximum size in bytes of a single message or batch sent in one request. Raise this value to accommodate large visitor profiles, but ensure it matches the broker&#39;s configuration. Default: 1,048,576 (1 MB). Maximum: 2,097,152 (2 MB). Must not exceed your Kafka broker&#39;s `message.max.bytes` setting.
* **Client ID**
  * A string identifier sent to the broker with every request for logging, monitoring attribution, and quota enforcement. If left blank, an auto-generated identifier in the format `tealium-{account}-{profile}-{connectorId}` is used. Allowed characters: letters, numbers, dots, hyphens, underscores.
* **Acknowledgments (acks)**
  * How many broker replicas must confirm receipt of a message. **1** (leader only) is fastest. **All** waits for all in-sync replicas, adding 50-100ms latency but eliminating data loss risk. **0** provides no acknowledgment, which is fastest but risks silent data loss.
* **Partitioner Strategy**
  * Controls how the producer assigns messages to partitions when no partition is specified. **Default** uses sticky batching for optimal throughput. **Round Robin** distributes messages evenly across all partitions. When a message key is set, messages are always partitioned by key hash regardless of this setting.
* **Producer - Reconnect Backoff**
  * Time in milliseconds to wait before attempting to reconnect to a broker after a connection failure. If left blank, the Kafka client default of 50ms is used.
* **Producer - Retries**
  * Maximum number of retry attempts for failed send operations. If left blank, the Kafka client default is used.
* **Producer - Retries Backoff**
  * Time in milliseconds to wait between successive send retries for the same record. If left blank, the Kafka client default of 100ms is used.

## Actions

| Action Name | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Send Entire Event Data | ✗ | ✓ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Custom Event Data | ✗ | ✓ |
| Send Custom Visitor Data | ✓ | ✗ |
| Send Entire Log Event | ✗ | ✓ |
| Send Log Event | ✗ | ✓ |

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

The following sections describe how to set up parameters and options for each action.

### Send Entire Event Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Topic | Select the topic or type the Topic ID. |
| Data Format | Specify the format for data delivery: `JSON`, `STRING`, or `BINARY`. |
| Partition ID | (Optional) Select the Partition ID. If left blank, Kafka&#39;s default partitioner is used based on the message key or round-robin. |
| Headers | (Optional) A set of key-value pairs added to the Kafka record headers. |
| Message Key | (Optional) Specify the raw message key. When the data format is set to `BINARY`, this value is encoded before it&#39;s sent. |
| Timestamp | (Optional) The message timestamp in ISO 8601 UTC format `YYYY-MM-DDThh:mm:ssZ`. If not provided, the current timestamp is used. |
| Print Attribute Names | By default, attribute keys are used. Enable this option to use attribute names as keys instead. |
| Batch time to live | Time to live in minutes for the batch (between 1 and 60). Default: 10. |

### Send Entire Visitor Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Topic | Select the topic or type the Topic ID. |
| Data Format | Specify the format for data delivery: `JSON`, `STRING`, or `BINARY`. |
| Partition ID | (Optional) Select the Partition ID. If left blank, Kafka&#39;s default partitioner is used based on the message key or round-robin. |
| Headers | (Optional) A set of key-value pairs added to the Kafka record headers. |
| Message Key | (Optional) Specify the raw message key. If you chose **BINARY** as the data format, Tealium encodes this value before sending it. |
| Timestamp | (Optional) The message timestamp in ISO 8601 UTC format `YYYY-MM-DDThh:mm:ssZ`. If not provided, the current timestamp is used. |
| Print Attribute Names | By default, attribute keys are used. Enable this option to use attribute names as keys instead. |
| Include Current Visit Data with Visitor Data | Include current visit data with the visitor data payload. |
| Batch time to live | Time to live in minutes for the batch (between 1 and 60). Default: 10. |

### Send Custom Event Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Topic | Select the topic or type the Topic ID. |
| Data Format | Specify the format for data delivery: `JSON`, `STRING`, or `BINARY`. |
| Schema | (Optional) Select a schema subject from the Schema Registry. Requires Schema Registry URL to be configured. |
| Message Data | Provide values to construct message data. To use a template, reference the template name and map it to Custom Message Definition. Any other key-value pairs are ignored when a template is used. |
| Partition ID | (Optional) Select the Partition ID. If left blank, Kafka&#39;s default partitioner is used based on the message key or round-robin. |
| Headers | (Optional) A set of key-value pairs added to the Kafka record headers. |
| Message Key | (Optional) Specify the raw message key. If you chose **BINARY** as the data format, Tealium encodes this value before sending it. |
| Timestamp | (Optional) The message timestamp in ISO 8601 UTC format `YYYY-MM-DDThh:mm:ssZ`. If not provided, the current timestamp is used. |
| Batch time to live | Time to live in minutes for the batch (between 1 and 60). Default: 10. |

### Send Custom Visitor Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Topic | Select the topic or type the Topic ID. |
| Data Format | Specify the format for data delivery: `JSON`, `STRING`, or `BINARY`. |
| Schema | (Optional) Select a schema subject from the Schema Registry. Requires Schema Registry URL to be configured. |
| Message Data | Provide values to construct message data. To use a template, reference the template name and map it to Custom Message Definition. Any other key-value pairs are ignored when a template is used. |
| Partition ID | (Optional) Select the Partition ID. If left blank, Kafka&#39;s default partitioner is used based on the message key or round-robin. |
| Headers | (Optional) A set of key-value pairs added to the Kafka record headers. |
| Message Key | (Optional) Specify the raw message key. If you chose **BINARY** as the data format, Tealium encodes this value before sending it. |
| Timestamp | (Optional) The message timestamp in ISO 8601 UTC format `YYYY-MM-DDThh:mm:ssZ`. If not provided, the current timestamp is used. |
| Batch time to live | Time to live in minutes for the batch (between 1 and 60). Default: 10. |

### Send Entire Log Event

#### Parameters

| Parameter | Description |
| --- | --- |
| Topic | Select the topic or type the Topic ID. |
| Data Format | Specify the format for data delivery: `JSON`, `STRING`, or `BINARY`. |
| Partition ID | (Optional) Select the Partition ID. If left blank, Kafka&#39;s default partitioner is used based on the message key or round-robin. |
| Headers | (Optional) A set of key-value pairs added to the Kafka record headers. |
| Message Key | (Optional) Specify the raw message key. If you chose **BINARY** as the data format, Tealium encodes this value before sending it. |
| Timestamp | (Optional) The message timestamp in ISO 8601 UTC format `YYYY-MM-DDThh:mm:ssZ`. If not provided, the current timestamp is used. |
| Batch time to live | Time to live in minutes for the batch (between 1 and 60). Default: 10. |

### Send Log Event

#### Parameters

| Parameter | Description |
| --- | --- |
| Topic | Select the topic or type the Topic ID. |
| Data Format | Specify the format for data delivery: `JSON`, `STRING`, or `BINARY`. |
| Partition ID | (Optional) Select the Partition ID. If left blank, Kafka&#39;s default partitioner is used based on the message key or round-robin. |
| Headers | (Optional) A set of key-value pairs added to the Kafka record headers. |
| Message Key | (Optional) Specify the raw message key. If you chose **BINARY** as the data format, Tealium encodes this value before sending it. |
| Timestamp | (Optional) The message timestamp in ISO 8601 UTC format `YYYY-MM-DDThh:mm:ssZ`. If not provided, the current timestamp is used. |
| Batch time to live | Time to live in minutes for the batch (between 1 and 60). Default: 10. |

#### Connector log parameters

For parameter descriptions, see [Connector log parameters]().