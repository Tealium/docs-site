---
title: AWS Kinesis Streams Connector Setup Guide
description: This article describes how to set up the AWS Kinesis Streams connector.
url: https://docs.tealium.com/server-side-connectors/aws-kinesis-streams-connector/
---
## Requirements

* Amazon Web Services Account
* Identity and Access Management (IAM) User Credentials
* Kinesis Streams

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event Data to Kinesis Stream | ✗ | ✓ |
| Send Visitor Data to Kinesis Stream | ✓ | ✗ |
| Send Customized Data to Kinesis Stream (Advanced) | ✓ | ✓ |
| Send Batched Event Data to Kinesis Stream | ✗ | ✓ |
| Send Batched Visitor Data to Kinesis Stream | ✓ | ✗ |
| Send Batched Customized Data to Kinesis Stream (Advanced) | ✓ | ✓ |

## Configure Settings

Navigate to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Access Key**  
(Required) Provide your IAM User's access key. The associated IAM policy (for either IAM User or Assumed Role) must grant `kinesis:PutRecord` permission along with streams you want to send data to. See: [Kinesis Streams Resources Access](http://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).
* **Secret Key**  
(Required) Provide your IAM User's secret key.
* **Region**  
(Required) Select a region.
* **Assume Role: ARN**  
(Optional) Provide Amazon Resource Name (ARN) of role to assume. For example: `arn:aws:iam::222222222222:role/myrole`. See: [Switching to an IAM Role](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html).
* **Assume Role: Session Name**  
(Optional) Provide identifier for assumed role session.
* **Assume Role: External ID**  
(Optional) Provide external identifier. See: [How to Use an External ID](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html).

## Actions

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action Settings - Send Event Data to Kinesis Stream

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Stream Name | Select the stream to send data to. If your IAM policy does not grant `kinesis:ListStreams` permission, you will need to manually enter a custom value. |
| Partition Key | (Required) A partition key groups data into shards within a stream. |
| Sequence Number For Ordering | The data record's sequence number within the Kinesis data stream's shard. |
| Explicit Hash Key | The key used to hash the Partition Key. |
| Print Attribute Names | If attribute names are updated, the names in the payload will reflect the update. |

### Action Settings - Send Visitor Data to Kinesis Stream

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Stream Name | Select the stream to send data to. If your IAM policy does not grant `kinesis:ListStreams` permission, you will need to manually enter a custom value. |
| Partition Key | (Required) A partition key groups data into shards within a stream. |
| Sequence Number For Ordering | The data record's sequence number within the Kinesis data stream's shard. |
| Explicit Hash Key | The key used to hash the Partition Key. |
| Include Current Visit Data With Visitor Data | Add the current visit data to the payload. This includes event visit data if Exclude Current Visit Event Data isn't selected. |
| Exclude Current Visit Event Data | Exclude event data from the current visit data. |
| Print Attribute Names | If attribute names are updated, the names in the payload will reflect the update. |

### Action Settings - Send Customized Data to Kinesis Stream (Advanced)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Stream Name | Select the stream to send data to. If your IAM policy does not grant 'kinesis:ListStreams' permission, you will need to manually enter a custom value. |
| Partition Key | (Required) A partition key groups data into shards within a stream. |
| Sequence Number For Ordering | The data record's sequence number within the Kinesis data stream's shard. |
| Explicit Hash Key | The key used to hash the Partition Key. |
| Custom Message Definition | A custom message to include in the log file. |
| Template Variables | Optional. <ul><li>(Optional) Provide template variables as data input for templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation. For example: `items.name`.</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
| Templates | Optional. <ul><li>(Optional) Provide templates to be referenced in message data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.</li></ul> |

### Action Settings - Send Batched Event Data to Kinesis Stream

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 5 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Stream Name | Select the stream to send data to. If your IAM policy does not grant `kinesis:ListStreams` permission, you will need to manually enter a custom value. |
| Partition Key | (Required) A partition key groups data into shards within a stream. |
| Explicit Hash Key | The key used to hash the Partition Key. |
| Print Attribute Names | If attribute names are updated, the names in the payload will reflect the update. |

### Action Settings - Send Batched Visitor Data to Kinesis Stream

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 5 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Stream Name | Select the stream to send data to. If your IAM policy does not grant 'kinesis:ListStreams' permission, you will need to manually enter a custom value. |
| Partition Key | (Required) A partition key groups data into shards within a stream. |
| Explicit Hash Key | The key used to hash the Partition Key. |
| Include Current Visit Data | A `true`/`false` value that indicates whether to include the current visit data in the payload. |
| Print Attribute Names | If attribute names are updated, the names in the payload will reflect the update. |

### Action Settings - Send Batched Customized Data to Kinesis Stream (Advanced)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 5 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Stream Name | Select the stream to send data to. If your IAM policy does not grant `kinesis:ListStreams` permission, you will need to manually enter a custom value. |
| Partition Key | (Required) A partition key groups data into shards within a stream. |
| Explicit Hash Key | The key used to hash the Partition Key. |
| Custom Message Definition | A custom message to include in the log file. |
| Template Variables | <ul><li>(Optional) Provide template variables as data input for templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation (For example: `items.name`).</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
| Templates | <ul><li>(Optional) Provide templates to be referenced in message data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields (For example, `{{SomeTemplateName}}`.)</li></ul> |
