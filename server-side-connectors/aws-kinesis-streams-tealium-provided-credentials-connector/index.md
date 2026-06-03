---
title: AWS Kinesis Streams (Tealium-Provided Credentials) Connector Setup Guide
description: This article describes how to set up the AWS Kinesis Streams (Tealium-Provided Credentials) connector.
url: https://docs.tealium.com/server-side-connectors/aws-kinesis-streams-tealium-provided-credentials-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event Data to Kinesis Stream | ✗ | ✓ |
| Send Visitor Data to Kinesis Stream | ✓ | ✗ |
| Send Customized Data to Kinesis Stream (Advanced) | ✓ | ✓ |
| Send Batched Event Data to Kinesis Stream | ✗ | ✓ |
| Send Batched Visitor Data to Kinesis Stream | ✓ | ✗ |
| Send Batched Customized Data to Kinesis Stream (Advanced) | ✓ | ✓ |

## Add Tealium role to AWS account

Before you configure the connector, you must create a role for the Tealium account ID and set it as a trusted entity:

1. In the **Identity and Access Management** (IAM) console, locate the Amazon Resource Name (ARN) for the Kinesis stream in the **Details** tab.
1. Navigate to **Policies &gt; Create Policy**. If this is the first policy you have created, click **Get Started** and **Create Policy**.
1. Enter the ARN for the Kinesis Stream.
1. Click **{} JSON**.
1. Enter the following policy, replacing `arn:aws:kinesis:us-east-1:123456789:stream/example`  with the ARN from Step 1.

  ```
  {
    &#34;Version&#34;: &#34;2023-06-01&#34;,
    &#34;Statement&#34;: [
      {
        &#34;Effect&#34;: &#34;Allow&#34;,
        &#34;Action&#34;: [
          &#34;kinesis:PutRecord&#34;,
          &#34;kinesis:PutRecords&#34;
                  ],
        &#34;Resource&#34;: &#34;arn:aws:kinesis:us-east-1:123456789:stream/example&#34;
      }
    ]
  }
```

1. Click **Next Step**.
1. Under **Policy Name**, enter **TealiumKinesis**.
1. Click **Create Policy**.
1. Navigate to **Roles &gt; Create Role**.
1. Under **Trusted entity type**, select **AWS Account**.
1. Select **Another AWS account**.
1. Under **Account ID**, enter `757913464184`.
1. Click **Next: Permissions**.
1. Select the **TealiumKinesis** policy.
1. Click **Next: Review**.
1. For the Name, enter **TealiumUser**.
1. Click **Create Role**.

Kinesis generates an ARN for the role similar to the following:

```
arn:aws:kinesis:us-east-1:123456789:role/example
```

For more information, see [Controlling Access to Amazon Kinesis Data Streams Resources Using IAM](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html) and [Create an IAM Policy and User](https://docs.aws.amazon.com/streams/latest/dev/tutorial-stock-data-kplkcl-iam.html).

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Region**  
(Required) Select a region.
* **Assume Role: ARN**  
(Optional) Provide Amazon Resource Name (ARN) of role to assume. For example: `arn:aws:iam::222222222222:role/myrole` See: [Switching to an IAM Role](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html).
* **Assume Role: Session Name**  
(Required) Provide identifier for assumed role session. Length Constraints: Minimum length of 2, Maximum length of 64.
* **Assume Role: External ID**  
(Optional) Provide external identifier. See: [How to Use an External ID](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html).

After you configure the connector, click **Test Connection** to confirm that the connector can connect to Amazon.

## Actions

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action Settings - Send Event Data to Kinesis Stream

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Stream Name | Select the stream to send data to. If your IAM policy doesn&#39;t grant `kinesis:ListStreams` permission, manually enter a custom value. |
| Partition Key | (Required) A partition key groups data into shards within a stream. |
| Sequence Number For Ordering | The data record&#39;s sequence number within the Kinesis data stream&#39;s shard. |
| Explicit Hash Key | The key used to hash the Partition Key. |
| Print Attribute Names | If attribute names are updated, the names in the payload reflect the update. |

### Action Settings - Send Visitor Data to Kinesis Stream

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Stream Name | Select the stream to send data to. If your IAM policy doesn&#39;t grant `kinesis:ListStreams` permission, manually enter a custom value. |
| Partition Key | (Required) A partition key groups data into shards within a stream. |
| Sequence Number For Ordering | The data record&#39;s sequence number within the Kinesis data stream&#39;s shard. |
| Explicit Hash Key | The key used to hash the Partition Key. |
| Include Current Visit Data With Visitor Data | Add the current visit data to the payload. This includes event visit data if Exclude Current Visit Event Data isn&#39;t selected. |
| Exclude Current Visit Event Data | Exclude event data from the current visit data. |
| Print Attribute Names | If attribute names are updated, the names in the payload reflect the update. |

### Action Settings - Send Customized Data to Kinesis Stream (Advanced)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Stream Name | Select the stream to send data to. If your IAM policy doesn&#39;t grant `kinesis:ListStreams` permission, manually enter a custom value. |
| Partition Key | (Required) A partition key groups data into shards within a stream. |
| Sequence Number For Ordering | The data record&#39;s sequence number within the Kinesis data stream&#39;s shard. |
| Explicit Hash Key | The key used to hash the Partition Key. |
| Custom Message Definition | A custom message to include in the log file. |
| Template Variables | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`.&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| Templates | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in message data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |

### Action Settings - Send Batched Event Data to Kinesis Stream

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 5 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Stream Name | Select the stream to send data to. If your IAM policy doesn&#39;t grant `kinesis:ListStreams` permission, manually enter a custom value. |
| Partition Key | (Required) A partition key groups data into shards within a stream. |
| Explicit Hash Key | The key used to hash the Partition Key. |
| Print Attribute Names | If attribute names are updated, the names in the payload reflect the update. |

### Action Settings - Send Batched Visitor Data to Kinesis Stream

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 5 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Stream Name | Select the stream to send data to. If your IAM policy doesn&#39;t grant `kinesis:ListStreams` permission, manually enter a custom value. |
| Partition Key | (Required) A partition key groups data into shards within a stream.  |
| Explicit Hash Key | The key used to hash the Partition Key. |
| Include Current Visit Data | A `true`/`false` value that indicates whether to include the current visit data in the payload. |
| Print Attribute Names | If attribute names are updated, the names in the payload reflect the update. |

### Action Settings - Send Batched Customized Data to Kinesis Stream (Advanced)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 5 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Stream Name | Select the stream to send data to. If your IAM policy doesn&#39;t grant `kinesis:ListStreams` permission, manually enter a custom value. |
| Partition Key | (Required) A partition key groups data into shards within a stream.  |
| Explicit Hash Key | The key used to hash the Partition Key. |
| Custom Message Definition | A custom message to include in the log file. |
| Template Variables | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example: `items.name`.&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| Templates | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in message data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |