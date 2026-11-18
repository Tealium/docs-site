---
title: Apache Kafka Connector Setup Guide
description: This article describes how to set up the Apache Kafka connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/apache-kafka-connector/
---
## Configuration

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the common settings that apply to every authentication type, then configure the fields for the authentication type your broker requires.

### Common settings

* **Bootstrap Server**
  * (Required) The Kafka bootstrap server for the endpoint, for example, a Conduktor Gateway host or Kafka broker: `gateway.customer-domain.com:6969`.
  * The endpoint must be reachable from Tealium, typically through PrivateLink, VPN, or network peering.
* **CA Certificate (PEM)**
  * The PEM-encoded CA certificate chain used to validate the TLS certificate presented by the Kafka broker or gateway.
  * Required when the endpoint uses an internal PKI, private CA, or self-signed certificate.
* **Disable Hostname Verification**
  * Disables verification that the hostname matches the TLS certificate.
  * Disable this setting if you use SNI or non-standard hostnames. Default: verification enabled.
* **Confluent Schema Registry URL**
  * (Optional) The Schema Registry URL, for example, `https://schema-registry.example.com:8081`.
  * Required when using schema validation with custom actions.
* **Confluent Schema Registry Username**
  * (Optional) The username used to authenticate with the Schema Registry using HTTP Basic authentication.
  * Required if the Schema Registry requires authentication.
* **Confluent Schema Registry Password**
  * (Optional) The password or API secret used to authenticate with the Schema Registry using HTTP Basic authentication.
  * Required if the Schema Registry requires authentication.
* **Compression Type**
  * The compression algorithm to use for messages sent to Kafka. Reduces bandwidth and storage costs.
  * Defaults to `GZIP`.
* **Maximum Message Size (bytes)**
  * The maximum size, in bytes, of a single message or batch sent in one request. Raise this value to accommodate large visitor profiles, but ensure it matches the broker's configuration.
  * Defaults to `1,048,576` bytes (1 MB). The maximum is `2,097,152` bytes (2 MB).
  * The value must not exceed the Kafka broker's `message.max.bytes` setting.
* **Client ID**
  * An identifier sent to the broker with each request for logging, monitoring attribution, and quota enforcement.
  * Defaults to an automatically generated identifier in the following format: `tealium-{account}-{profile}-{connectorId}`.
  * Supported characters are letters, numbers, periods (`.`), hyphens (`-`), and underscores (`_`).
* **Acknowledgments (acks)**
  * Specifies the number of broker acknowledgments required before a message is considered successfully written.
  * **0**: No acknowledgment. Fastest but risks silent data loss.
  * **1**: The partition leader acknowledges the message after writing it locally. Fastest with a delivery guarantee.
  * **All**: All in-sync replicas must acknowledge, adding 50 to 100 ms latency but eliminating data loss risk.
* **Partitioner Strategy**
  * Controls how the producer assigns messages to partitions when no partition is specified.
  * **Default**: Uses sticky batching for optimal throughput.
  * **Round Robin**: Distributes messages evenly across all partitions.
  * When a message key is set, messages are always partitioned by key hash regardless of this setting.
* **Producer - Reconnect Backoff**
  * The time, in milliseconds, to wait before reconnecting to a broker after a connection failure.
  * Defaults to `50` milliseconds.
* **Producer - Retries**
  * The maximum number of retry attempts for failed send operations.
  * If left blank, the Kafka client default is used.
* **Producer - Retries Backoff**
  * The time, in milliseconds, to wait between retry attempts for the same record.
  * Defaults to `100` milliseconds.

### Authentication type

Select the authentication type the broker requires. The connector shows a different set of fields for each option:

* **SASL PLAIN** (default)
* **SASL SCRAM-SHA-512**
* **SASL OAUTHBEARER**
* **mTLS (DigiCert)**
* **mTLS (Self-Signed)**

#### SASL PLAIN

* **Service Account Username**
  * (Required) The Kafka principal used to authenticate with the broker using SASL PLAIN.
* **Service Account Token / Password**
  * (Required) The JWT token or equivalent credential for the service account principal.

#### SASL SCRAM-SHA-512

Before selecting this option, configure the Kafka broker to support the `SCRAM-SHA-512` mechanism.

* **Service Account Username**
  * (Required) The Kafka principal used to authenticate with the broker using SASL SCRAM-SHA-512.
* **Service Account Token / Password**
  * (Required) The password for the SCRAM-SHA-512 principal.

#### SASL OAUTHBEARER

Use this authentication type to log in to a Kafka broker using OAuth 2.0 client credentials. Confluent Cloud, and any broker that uses identity pools, requires SASL extensions. For the extension format, see the **Additional OAuth Parameters** field.

* **OAuth Token Endpoint**
  * (Required) The token endpoint URL for OAUTHBEARER authentication, for example, `https://auth.example.com/oauth2/token`.
* **OAuth Client ID**
  * (Required) The OAuth2 client ID.
* **OAuth Client Secret**
  * (Required) The OAuth2 client secret.
* **OAuth Scope**
  * (Optional) The OAuth2 scope to request, for example, `kafka`.
* **Additional OAuth Parameters**
  * (Optional) Additional parameters in the format `param="value"`, separated by spaces.
  * The connector sends parameters without the `extension_` prefix to the OAuth2 token endpoint, for example, `audience="https://auth.example.com"`.
  * The connector sends parameters prefixed with `extension_` to the Kafka broker as SASL extensions, with the prefix stripped. Confluent Cloud requires `extension_logicalCluster` and, when the cluster uses identity pools, `extension_identityPoolId`. Example: `extension_logicalCluster="lkc-abc123" extension_identityPoolId="pool-xyz"`.
  * The connector validates extension names and values against the Kafka client rules at login. Invalid values fail with a clear configuration error. The name `auth` is reserved.
  * Token request behavior does not change when no `extension_` parameters are configured.

#### mTLS (DigiCert)

Use this authentication type to generate a client certificate through DigiCert for mTLS authentication to the broker.

* **Client Certificate (DigiCert)**
  * (Required) Generates a client certificate through DigiCert for mTLS authentication.
* **Key Algorithm**
  * Select an algorithm to generate the key pair and CSR. After generation, download the CSR file, have it signed by your certificate authority, and upload the signed certificate.

#### mTLS (Self-Signed)

Use this authentication type to supply a client certificate signed by your own certificate authority. The connector collects the CSR subject fields, generates the key pair and CSR, and accepts the signed certificate.

* **Common Name (CN)**
  * (Required) The Common Name for the certificate signing request, for example, `kafka-client.example.com`.
* **Organization (O)**
  * (Required) The organization name for the certificate signing request.
* **Organizational Unit (OU)**
  * (Optional) The organizational unit for the certificate signing request.
* **Locality (L)**
  * (Optional) The locality (city) for the certificate signing request.
* **State (ST)**
  * (Optional) The state or province for the certificate signing request.
* **Country (C)**
  * (Optional) The two-letter country code for the certificate signing request, for example, `US`.
* **Key Algorithm**
  * Select an algorithm to generate the key pair and CSR. After generation, download the CSR file, have it signed by your certificate authority, and upload the signed certificate.
* **Client Certificate (PEM)**
  * (Required) Paste the client certificate in PEM format for mTLS authentication.

After you configure the connector, click **Done**.

## Actions

| Action name | Visitor profile | Event data |
| ----------- | :------------: | :---------: |
| Send Entire Event Data | ✗ | ✓ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Custom Event Data | ✗ | ✓ |
| Send Custom Visitor Data | ✓ | ✗ |
| Send Entire Log Event | ✗ | ✓ |
| Send Log Event | ✗ | ✓ |

Click **Continue** to configure the connector actions. Enter a name for the action and select the action type from the list.

The following sections describe how to set up parameters and options for each action.

### Send Entire Event Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Topic | Select the topic or type the Topic ID. |
| Data Format | Specify the format for data delivery: `JSON`, `STRING`, or `BINARY`. |
| Partition ID | (Optional) Select the Partition ID. If left blank, Kafka's default partitioner is used based on the message key or round-robin. |
| Headers | (Optional) A set of key-value pairs added to the Kafka record headers. |
| Message Key | (Optional) Specify the raw message key. When the data format is set to `BINARY`, this value is encoded before it's sent. |
| Timestamp | (Optional) The message timestamp in ISO 8601 UTC format `YYYY-MM-DDThh:mm:ssZ`. If not provided, the current timestamp is used. |
| Print Attribute Names | By default, attribute keys are used. Enable this option to use attribute names as keys instead. |
| Batch time to live | Time to live in minutes for the batch (between 1 and 60). Default: 10. |

### Send Entire Visitor Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Topic | Select the topic or type the Topic ID. |
| Data Format | Specify the format for data delivery: `JSON`, `STRING`, or `BINARY`. |
| Partition ID | (Optional) Select the Partition ID. If left blank, Kafka's default partitioner is used based on the message key or round-robin. |
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
| Partition ID | (Optional) Select the Partition ID. If left blank, Kafka's default partitioner is used based on the message key or round-robin. |
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
| Partition ID | (Optional) Select the Partition ID. If left blank, Kafka's default partitioner is used based on the message key or round-robin. |
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
| Partition ID | (Optional) Select the Partition ID. If left blank, Kafka's default partitioner is used based on the message key or round-robin. |
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
| Partition ID | (Optional) Select the Partition ID. If left blank, Kafka's default partitioner is used based on the message key or round-robin. |
| Headers | (Optional) A set of key-value pairs added to the Kafka record headers. |
| Message Key | (Optional) Specify the raw message key. If you chose **BINARY** as the data format, Tealium encodes this value before sending it. |
| Timestamp | (Optional) The message timestamp in ISO 8601 UTC format `YYYY-MM-DDThh:mm:ssZ`. If not provided, the current timestamp is used. |
| Batch time to live | Time to live in minutes for the batch (between 1 and 60). Default: 10. |

#### Connector log parameters

For parameter descriptions, see [Connector log parameters](https://docs.tealium.com/connector-error-logging/#connector-log-parameters).
