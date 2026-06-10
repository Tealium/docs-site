---
title: Elastic Connector Setup Guide
description: This article describes how to set up the Elastic connector.
url: https://docs.tealium.com/server-side-connectors/elastic-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:
* **Authentication type**: Select the authentication type.
* **Host**: (Required) The Elastic host URL.
* **API key**: (Required) Elastic API key.

### Create data stream

To create a data stream:

1. Under **Remote Configuration**, click **Create Data Stream**.
1. Enter the **Data stream name**.
1. Click **Create Data Stream &amp; Close**.

## Actions

| Action Name | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Send Entire Event Data | ✗ | ✓ |
| Send Entire Event Data (Batch) | ✗ | ✓ |
| Send Custom Event Data | ✗ | ✓ |
| Send Custom Event Data (Batch) | ✗ | ✓ |
| Send Entire Log Event | ✗ | ✓ |
| Send Log Event | ✗ | ✓ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Entire Visitor Data (Batch) | ✓ | ✗ |
| Send Custom Visitor Data | ✓ | ✗ |
| Send Custom Visitor Data (Batch) | ✓ | ✗ |

### Send Entire Event Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Target type | (Required) Specify the target type: **Index** or a **Data stream**. |
| Target | (Required) Specify the target. When target type is **Index**, custom values are accepted (the index is created on the fly if needed). When target type is **Data stream**, select an existing data stream or click **Create Data Stream** to create one. Enter a **Data stream name** and click **Create Data Stream &amp; Close**. |

#### Document details

Optional document metadata. Available keys depend on the target type.

| Parameter | Description |
| --- | --- |
| `document_id` | A unique document identifier. Available when target type is **Index**. |
| `timestamp` | Event timestamp in ISO 8601 format (for example, `2025-05-16T11:48:00Z`) or epoch nanoseconds (for example, `1715856480000000000`). Available when target type is **Data stream**. Defaults to the current time if blank or malformed. |

#### Concurrency control

| Parameter | Description |
| --- | --- |
| `primary_term` | Only perform the operation if the document has this primary term. |
| `seq_no` | Only perform the operation if the document has this sequence number. |
| `version` | Explicit version number for concurrency control. Must be a non-negative long. |
| Error Handling | Configure how Elastic reports parsing errors. |

Concurrency-control parameters are not supported for Data streams. Data streams are append-only and enforce first-write-wins semantics, so `primary_term`, `seq_no`, and `version` have no effect. If you need optimistic concurrency control or document updates, target a regular index or its write alias instead of a Data stream.

#### Indexing behavior

Optional parameters that control how documents are indexed.

| Parameter | Description |
| --- | --- |
| `operation_type` | Defines how the document is indexed. `index` overwrites an existing document with the same ID. `create` inserts only and fails if a document with the same ID already exists. Available when target type is **Index** only. |
| `pipeline` | ID of the ingest pipeline used to preprocess documents. Use `_none` to disable the default ingest pipeline. |
| `routing` | A custom routing value to direct operations to a specific shard. |
| `wait_for_active_shards` | Minimum shard copies required before proceeding. Default: `1`. Allowed values: `all` or any positive integer up to the total number of shards (`number_of_replicas &#43; 1`). |
| Refresh | Determines when indexing operations become visible in search. Allowed values: `true`, `false`, `wait_for`. |
| Event Data | Configure how event payload keys are emitted. |
| Custom attributes | Include any additional attributes that you want to add at the root level of the JSON object. |

### Send Entire Event Data (Batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 300,000
* Max time since oldest request: 60 minutes
* Max size of requests: 100 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Target type | (Required) Specify the target type: **Index** or a **Data stream**. |
| Target | (Required) Specify the target. When target type is **Index**, custom values are accepted (the index is created on the fly if needed). When target type is **Data stream**, select an existing data stream or click **Create Data Stream** to create one. Enter a **Data stream name** and click **Create Data Stream &amp; Close**. |

#### Document details

Optional document metadata. Available keys depend on the target type.

| Parameter | Description |
| --- | --- |
| `document_id` | A unique document identifier. Available when target type is **Index**. |
| `timestamp` | Event timestamp in ISO 8601 format (for example, `2025-05-16T11:48:00Z`) or epoch nanoseconds (for example, `1715856480000000000`). Available when target type is **Data stream**. Defaults to the current time if blank or malformed. |

#### Concurrency control

| Parameter | Description |
| --- | --- |
| `primary_term` | Only perform the operation if the document has this primary term. |
| `seq_no` | Only perform the operation if the document has this sequence number. |
| `version` | Explicit version number for concurrency control. Must be a non-negative long. |
| Error Handling | Configure how Elastic reports parsing errors. |

Concurrency-control parameters are not supported for Data streams. Data streams are append-only and enforce first-write-wins semantics, so `primary_term`, `seq_no`, and `version` have no effect. If you need optimistic concurrency control or document updates, target a regular index or its write alias instead of a Data stream.

#### Indexing behavior

Optional parameters that control how documents are indexed.

| Parameter | Description |
| --- | --- |
| `operation_type` | Defines how the document is indexed. `index` overwrites an existing document with the same ID. `create` inserts only and fails if a document with the same ID already exists. Available when target type is **Index** only. |
| `pipeline` | ID of the ingest pipeline used to preprocess documents. Use `_none` to disable the default ingest pipeline. |
| `routing` | A custom routing value to direct operations to a specific shard. |
| `wait_for_active_shards` | Minimum shard copies required before proceeding. Default: `1`. Allowed values: `all` or any positive integer up to the total number of shards (`number_of_replicas &#43; 1`). |
| Refresh | Determines when indexing operations become visible in search. Allowed values: `true`, `false`, `wait_for`. |
| Event Data | Configure how event payload keys are emitted. |
| Custom attributes | Include any additional attributes that you want to add at the root level of the JSON object. |
| Batch time to live | Time to live for the batch, in minutes. Allowed values: `1` to `60`. Default: `60`. |

### Send Custom Event Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Target type | (Required) Specify the target type: **Index** or a **Data stream**. |
| Target | (Required) Specify the target. When target type is **Index**, custom values are accepted (the index is created on the fly if needed). When target type is **Data stream**, select an existing data stream or click **Create Data Stream** to create one. Enter a **Data stream name** and click **Create Data Stream &amp; Close**. |

#### Document details

Optional document metadata. Available keys depend on the target type.

| Parameter | Description |
| --- | --- |
| `document_id` | A unique document identifier. Available when target type is **Index**. |
| `timestamp` | Event timestamp in ISO 8601 format (for example, `2025-05-16T11:48:00Z`) or epoch nanoseconds (for example, `1715856480000000000`). Available when target type is **Data stream**. Defaults to the current time if blank or malformed. |

#### Concurrency control

| Parameter | Description |
| --- | --- |
| `primary_term` | Only perform the operation if the document has this primary term. |
| `seq_no` | Only perform the operation if the document has this sequence number. |
| `version` | Explicit version number for concurrency control. Must be a non-negative long. |
| Error Handling | Configure how Elastic reports parsing errors. |

Concurrency-control parameters are not supported for Data streams. Data streams are append-only and enforce first-write-wins semantics, so `primary_term`, `seq_no`, and `version` have no effect. If you need optimistic concurrency control or document updates, target a regular index or its write alias instead of a Data stream.

#### Indexing behavior

Optional parameters that control how documents are indexed.

| Parameter | Description |
| --- | --- |
| `operation_type` | Defines how the document is indexed. `index` overwrites an existing document with the same ID. `create` inserts only and fails if a document with the same ID already exists. Available when target type is **Index** only. |
| `pipeline` | ID of the ingest pipeline used to preprocess documents. Use `_none` to disable the default ingest pipeline. |
| `routing` | A custom routing value to direct operations to a specific shard. |
| `wait_for_active_shards` | Minimum shard copies required before proceeding. Default: `1`. Allowed values: `all` or any positive integer up to the total number of shards (`number_of_replicas &#43; 1`). |
| Refresh | Determines when indexing operations become visible in search. Allowed values: `true`, `false`, `wait_for`. |
| Custom attributes | Include any additional attributes that you want to add at the root level of the JSON object. |

### Send Custom Event Data (Batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 300,000
* Max time since oldest request: 60 minutes
* Max size of requests: 100 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Target type | (Required) Specify the target type: **Index** or a **Data stream**. |
| Target | (Required) Specify the target. When target type is **Index**, custom values are accepted (the index is created on the fly if needed). When target type is **Data stream**, select an existing data stream or click **Create Data Stream** to create one. Enter a **Data stream name** and click **Create Data Stream &amp; Close**. |

#### Document details

Optional document metadata. Available keys depend on the target type.

| Parameter | Description |
| --- | --- |
| `document_id` | A unique document identifier. Available when target type is **Index**. |
| `timestamp` | Event timestamp in ISO 8601 format (for example, `2025-05-16T11:48:00Z`) or epoch nanoseconds (for example, `1715856480000000000`). Available when target type is **Data stream**. Defaults to the current time if blank or malformed. |

#### Concurrency control

| Parameter | Description |
| --- | --- |
| `primary_term` | Only perform the operation if the document has this primary term. |
| `seq_no` | Only perform the operation if the document has this sequence number. |
| `version` | Explicit version number for concurrency control. Must be a non-negative long. |
| Error Handling | Configure how Elastic reports parsing errors. |

Concurrency-control parameters are not supported for Data streams. Data streams are append-only and enforce first-write-wins semantics, so `primary_term`, `seq_no`, and `version` have no effect. If you need optimistic concurrency control or document updates, target a regular index or its write alias instead of a Data stream.

#### Indexing behavior

Optional parameters that control how documents are indexed.

| Parameter | Description |
| --- | --- |
| `operation_type` | Defines how the document is indexed. `index` overwrites an existing document with the same ID. `create` inserts only and fails if a document with the same ID already exists. Available when target type is **Index** only. |
| `pipeline` | ID of the ingest pipeline used to preprocess documents. Use `_none` to disable the default ingest pipeline. |
| `routing` | A custom routing value to direct operations to a specific shard. |
| `wait_for_active_shards` | Minimum shard copies required before proceeding. Default: `1`. Allowed values: `all` or any positive integer up to the total number of shards (`number_of_replicas &#43; 1`). |
| Refresh | Determines when indexing operations become visible in search. Allowed values: `true`, `false`, `wait_for`. |
| Event Data | Configure how event payload keys are emitted. |
| Custom attributes | Include any additional attributes that you want to add at the root level of the JSON object. |
| Batch time to live | Time to live for the batch, in minutes. Allowed values: `1` to `60`. Default: `60`. |

### Send Entire Log Event

#### Parameters

| Parameter | Description |
| --- | --- |
| Target type | (Required) Specify the target type: **Index** or a **Data stream**. |
| Target | (Required) Specify the target. When target type is **Index**, custom values are accepted (the index is created on the fly if needed). When target type is **Data stream**, select an existing data stream or click **Create Data Stream** to create one. Enter a **Data stream name** and click **Create Data Stream &amp; Close**. |

#### Document details

Optional document metadata. Available keys depend on the target type.

| Parameter | Description |
| --- | --- |
| `document_id` | A unique document identifier. Available when target type is **Index**. |
| `timestamp` | Event timestamp in ISO 8601 format (for example, `2025-05-16T11:48:00Z`) or epoch nanoseconds (for example, `1715856480000000000`). Available when target type is **Data stream**. Defaults to the current time if blank or malformed. |

#### Concurrency control

| Parameter | Description |
| --- | --- |
| `primary_term` | Only perform the operation if the document has this primary term. |
| `seq_no` | Only perform the operation if the document has this sequence number. |
| `version` | Explicit version number for concurrency control. Must be a non-negative long. |
| Error Handling | Configure how Elastic reports parsing errors. |

Concurrency-control parameters are not supported for Data streams. Data streams are append-only and enforce first-write-wins semantics, so `primary_term`, `seq_no`, and `version` have no effect. If you need optimistic concurrency control or document updates, target a regular index or its write alias instead of a Data stream.

#### Indexing behavior

Optional parameters that control how documents are indexed.

| Parameter | Description |
| --- | --- |
| `operation_type` | Defines how the document is indexed. `index` overwrites an existing document with the same ID. `create` inserts only and fails if a document with the same ID already exists. Available when target type is **Index** only. |
| `pipeline` | ID of the ingest pipeline used to preprocess documents. Use `_none` to disable the default ingest pipeline. |
| `routing` | A custom routing value to direct operations to a specific shard. |
| `wait_for_active_shards` | Minimum shard copies required before proceeding. Default: `1`. Allowed values: `all` or any positive integer up to the total number of shards (`number_of_replicas &#43; 1`). |
| Refresh | Determines when indexing operations become visible in search. Allowed values: `true`, `false`, `wait_for`. |
| Custom attributes | Include any additional attributes that you want to add at the root level of the JSON object. |

### Send Log Event

#### Parameters

| Parameter | Description |
| --- | --- |
| Target type | (Required) Specify the target type: **Index** or a **Data stream**. |
| Target | (Required) Specify the target. When target type is **Index**, custom values are accepted (the index is created on the fly if needed). When target type is **Data stream**, select an existing data stream or click **Create Data Stream** to create one. Enter a **Data stream name** and click **Create Data Stream &amp; Close**. |

#### Document details

Optional document metadata. Available keys depend on the target type.

| Parameter | Description |
| --- | --- |
| `document_id` | A unique document identifier. Available when target type is **Index**. |
| `timestamp` | Event timestamp in ISO 8601 format (for example, `2025-05-16T11:48:00Z`) or epoch nanoseconds (for example, `1715856480000000000`). Available when target type is **Data stream**. Defaults to the current time if blank or malformed. |

#### Concurrency control

| Parameter | Description |
| --- | --- |
| `primary_term` | Only perform the operation if the document has this primary term. |
| `seq_no` | Only perform the operation if the document has this sequence number. |
| `version` | Explicit version number for concurrency control. Must be a non-negative long. |
| Error Handling | Configure how Elastic reports parsing errors. |

Concurrency-control parameters are not supported for Data streams. Data streams are append-only and enforce first-write-wins semantics, so `primary_term`, `seq_no`, and `version` have no effect. If you need optimistic concurrency control or document updates, target a regular index or its write alias instead of a Data stream.

#### Indexing behavior

Optional parameters that control how documents are indexed.

| Parameter | Description |
| --- | --- |
| `operation_type` | Defines how the document is indexed. `index` overwrites an existing document with the same ID. `create` inserts only and fails if a document with the same ID already exists. Available when target type is **Index** only. |
| `pipeline` | ID of the ingest pipeline used to preprocess documents. Use `_none` to disable the default ingest pipeline. |
| `routing` | A custom routing value to direct operations to a specific shard. |
| `wait_for_active_shards` | Minimum shard copies required before proceeding. Default: `1`. Allowed values: `all` or any positive integer up to the total number of shards (`number_of_replicas &#43; 1`). |
| Refresh | Determines when indexing operations become visible in search. Allowed values: `true`, `false`, `wait_for`. |
| Log event resource attributes | These fields capture information about the entity for which telemetry is recorded. |
| Log event HTTP attributes | These fields log the HTTP requests and responses within the logging system. To map the entire `http` array to a single column, map the `http` attribute. |
| Log event result attributes | These fields log the outcome of the operation, detailing whether it was successful or if it encountered errors. |
| Log event other attributes | These fields provide additional metadata about the logged events. |
| Custom attributes | Include any additional attributes that you want to add at the root level of the JSON object. |

### Send Entire Visitor Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Target type | (Required) Specify the target type: **Index** or a **Data stream**. |
| Target | (Required) Specify the target. When target type is **Index**, custom values are accepted (the index is created on the fly if needed). When target type is **Data stream**, select an existing data stream or click **Create Data Stream** to create one. Enter a **Data stream name** and click **Create Data Stream &amp; Close**. |

#### Document details

Optional document metadata. Available keys depend on the target type.

| Parameter | Description |
| --- | --- |
| `document_id` | A unique document identifier. Available when target type is **Index**. |
| `timestamp` | Event timestamp in ISO 8601 format (for example, `2025-05-16T11:48:00Z`) or epoch nanoseconds (for example, `1715856480000000000`). Available when target type is **Data stream**. Defaults to the current time if blank or malformed. |

#### Concurrency control

| Parameter | Description |
| --- | --- |
| `primary_term` | Only perform the operation if the document has this primary term. |
| `seq_no` | Only perform the operation if the document has this sequence number. |
| `version` | Explicit version number for concurrency control. Must be a non-negative long. |
| Error Handling | Configure how Elastic reports parsing errors. |

Concurrency-control parameters are not supported for Data streams. Data streams are append-only and enforce first-write-wins semantics, so `primary_term`, `seq_no`, and `version` have no effect. If you need optimistic concurrency control or document updates, target a regular index or its write alias instead of a Data stream.

#### Indexing behavior

Optional parameters that control how documents are indexed.

| Parameter | Description |
| --- | --- |
| `operation_type` | Defines how the document is indexed. `index` overwrites an existing document with the same ID. `create` inserts only and fails if a document with the same ID already exists. Available when target type is **Index** only. |
| `pipeline` | ID of the ingest pipeline used to preprocess documents. Use `_none` to disable the default ingest pipeline. |
| `routing` | A custom routing value to direct operations to a specific shard. |
| `wait_for_active_shards` | Minimum shard copies required before proceeding. Default: `1`. Allowed values: `all` or any positive integer up to the total number of shards (`number_of_replicas &#43; 1`). |
| Refresh | Determines when indexing operations become visible in search. Allowed values: `true`, `false`, `wait_for`. |
| Visitor Data | Configure how the visitor payload is composed. |
| Print Attribute Names | Configure how event payload keys are emitted. |
| Custom attributes | Include any additional attributes that you want to add at the root level of the JSON object. |

### Send Entire Visitor Data (Batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 300,000
* Max time since oldest request: 60 minutes
* Max size of requests: 100 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Target type | (Required) Specify the target type: **Index** or a **Data stream**. |
| Target | (Required) Specify the target. When target type is **Index**, custom values are accepted (the index is created on the fly if needed). When target type is **Data stream**, select an existing data stream or click **Create Data Stream** to create one. Enter a **Data stream name** and click **Create Data Stream &amp; Close**. |

#### Document details

Optional document metadata. Available keys depend on the target type.

| Parameter | Description |
| --- | --- |
| `document_id` | A unique document identifier. Available when target type is **Index**. |
| `timestamp` | Event timestamp in ISO 8601 format (for example, `2025-05-16T11:48:00Z`) or epoch nanoseconds (for example, `1715856480000000000`). Available when target type is **Data stream**. Defaults to the current time if blank or malformed. |

#### Concurrency control

| Parameter | Description |
| --- | --- |
| `primary_term` | Only perform the operation if the document has this primary term. |
| `seq_no` | Only perform the operation if the document has this sequence number. |
| `version` | Explicit version number for concurrency control. Must be a non-negative long. |
| Error Handling | Configure how Elastic reports parsing errors. |

Concurrency-control parameters are not supported for Data streams. Data streams are append-only and enforce first-write-wins semantics, so `primary_term`, `seq_no`, and `version` have no effect. If you need optimistic concurrency control or document updates, target a regular index or its write alias instead of a Data stream.

#### Indexing behavior

Optional parameters that control how documents are indexed.

| Parameter | Description |
| --- | --- |
| `operation_type` | Defines how the document is indexed. `index` overwrites an existing document with the same ID. `create` inserts only and fails if a document with the same ID already exists. Available when target type is **Index** only. |
| `pipeline` | ID of the ingest pipeline used to preprocess documents. Use `_none` to disable the default ingest pipeline. |
| `routing` | A custom routing value to direct operations to a specific shard. |
| `wait_for_active_shards` | Minimum shard copies required before proceeding. Default: `1`. Allowed values: `all` or any positive integer up to the total number of shards (`number_of_replicas &#43; 1`). |
| Refresh | Determines when indexing operations become visible in search. Allowed values: `true`, `false`, `wait_for`. |
| Event Data | Configure how event payload keys are emitted. |
| Custom attributes | Include any additional attributes that you want to add at the root level of the JSON object. |

### Send Custom Visitor Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Target type | (Required) Specify the target type: **Index** or a **Data stream**. |
| Target | (Required) Specify the target. When target type is **Index**, custom values are accepted (the index is created on the fly if needed). When target type is **Data stream**, select an existing data stream or click **Create Data Stream** to create one. Enter a **Data stream name** and click **Create Data Stream &amp; Close**. |

#### Document details

Optional document metadata. Available keys depend on the target type.

| Parameter | Description |
| --- | --- |
| `document_id` | A unique document identifier. Available when target type is **Index**. |
| `timestamp` | Event timestamp in ISO 8601 format (for example, `2025-05-16T11:48:00Z`) or epoch nanoseconds (for example, `1715856480000000000`). Available when target type is **Data stream**. Defaults to the current time if blank or malformed. |
| Message attributes | Maps custom attributes to the JSON object sent to Elastic inside the `message` attribute. To pass values at the root of the document, use **Custom attributes** instead. |

#### Concurrency control

| Parameter | Description |
| --- | --- |
| `primary_term` | Only perform the operation if the document has this primary term. |
| `seq_no` | Only perform the operation if the document has this sequence number. |
| `version` | Explicit version number for concurrency control. Must be a non-negative long. |
| Error Handling | Configure how Elastic reports parsing errors. |

Concurrency-control parameters are not supported for Data streams. Data streams are append-only and enforce first-write-wins semantics, so `primary_term`, `seq_no`, and `version` have no effect. If you need optimistic concurrency control or document updates, target a regular index or its write alias instead of a Data stream.

#### Indexing behavior

Optional parameters that control how documents are indexed.

| Parameter | Description |
| --- | --- |
| `operation_type` | Defines how the document is indexed. `index` overwrites an existing document with the same ID. `create` inserts only and fails if a document with the same ID already exists. Available when target type is **Index** only. |
| `pipeline` | ID of the ingest pipeline used to preprocess documents. Use `_none` to disable the default ingest pipeline. |
| `routing` | A custom routing value to direct operations to a specific shard. |
| `wait_for_active_shards` | Minimum shard copies required before proceeding. Default: `1`. Allowed values: `all` or any positive integer up to the total number of shards (`number_of_replicas &#43; 1`). |
| Refresh | Determines when indexing operations become visible in search. Allowed values: `true`, `false`, `wait_for`. |
| Custom attributes | Include any additional attributes that you want to add at the root level of the JSON object. |

### Send Custom Visitor Data (Batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 300,000
* Max time since oldest request: 60 minutes
* Max size of requests: 100 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Target type | (Required) Specify the target type: **Index** or a **Data stream**. |
| Target | (Required) Specify the target. When target type is **Index**, custom values are accepted (the index is created on the fly if needed). When target type is **Data stream**, select an existing data stream or click **Create Data Stream** to create one. Enter a **Data stream name** and click **Create Data Stream &amp; Close**. |

#### Document details

Optional document metadata. Available keys depend on the target type.

| Parameter | Description |
| --- | --- |
| `document_id` | A unique document identifier. Available when target type is **Index**. |
| `timestamp` | Event timestamp in ISO 8601 format (for example, `2025-05-16T11:48:00Z`) or epoch nanoseconds (for example, `1715856480000000000`). Available when target type is **Data stream**. Defaults to the current time if blank or malformed. |
| Message attributes | Maps custom attributes to the JSON object sent to Elastic inside the `message` attribute. To pass values at the root of the document, use **Custom attributes** instead. |
| Error Handling | Configure how Elastic reports parsing errors. |

#### Indexing behavior

Optional parameters that control how documents are indexed.

| Parameter | Description |
| --- | --- |
| `operation_type` | Defines how the document is indexed. `index` overwrites an existing document with the same ID. `create` inserts only and fails if a document with the same ID already exists. Available when target type is **Index** only. |
| `pipeline` | ID of the ingest pipeline used to preprocess documents. Use `_none` to disable the default ingest pipeline. |
| `routing` | A custom routing value to direct operations to a specific shard. |
| `wait_for_active_shards` | Minimum shard copies required before proceeding. Default: `1`. Allowed values: `all` or any positive integer up to the total number of shards (`number_of_replicas &#43; 1`). |
| Refresh | Determines when indexing operations become visible in search. Allowed values: `true`, `false`, `wait_for`. |
| Custom attributes | Include any additional attributes that you want to add at the root level of the JSON object. |
| Batch time to live | Time to live for the batch, in minutes. Allowed values: `1` to `60`. Default: `60`. |