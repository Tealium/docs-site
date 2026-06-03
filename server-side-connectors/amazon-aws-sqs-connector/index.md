---
title: Amazon AWS SQS Connector Setup Guide
description: This article describes how to set up the AWS SQS connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/amazon-aws-sqs-connector/
---
Amazon SQS provides fully managed message queues for micro-services, distributed systems, and server-less applications.

## Requirements

* AWS Account
* (Required) `sqs:SendMessage` permission
* (Optional) `sqs:ListQueues` permission
* Queue to send data to

## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Event Data to Queue| ✗| ✓|
|Send Event Data to Queue (Batch)| ✗| ✓|
|Send Visitor Data to Queue| ✓| ✗|
|Send Visitor Data to Queue (Batch)| ✓| ✗|
|Send Customized Data to Queue (Advanced)| ✓| ✓|
|Send Customized Data to Queue (Advanced Batch)| ✓| ✓| 

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Access Key**
  * (Required) Provide your IAM User&#39;s access key. Associated IAM policy (for either IAM User or Assumed Role) must grant `sqs:SendMessage` permission.
  * For more information, see [Access Control for Amazon SQS](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-authentication-and-access-control.htm).

* **Secret Key**
  * (Required) Provide your IAM User&#39;s secret key

* **Region**
  * (Required) Select the region.

* **Assume Role: ARN**
  * (Optional) Provide Amazon Resource Name (ARN) of role to assume.  
For example: `arn:aws:iam::222222222222:role/myrole`
  * For more information, see [Switching to an IAM Role](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html).

* **Assume Role: Session Name**
  * (Optional) Provide identifier for assumed role session.

* **Assume Role: External ID**
  * (Optional) Provide external identifier.
  * For more information, see [How to Use an External ID](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html).

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

The following sections describe how to set up parameters and options for each action.

### Action - Send Event Data to Queue and Send Event Data to Queue (Batch)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 10
* Maximum time since oldest request: 5 minutes
* Maximum size of requests: 1 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Queue|  &lt;ul&gt;&lt;li&gt;(Required) Select queue to send data to.&lt;/li&gt;&lt;li&gt;If your IAM policy does not grant `sqs:ListQueues` permission, you will need to manually enter a Custom Value.&lt;/li&gt;&lt;li&gt;The custom value should be a URL. For example: `https://sqs.us-west-2.amazonaws.com/0123456789/queue_name`&lt;/li&gt;&lt;/ul&gt; |
|MessageGroupId|Specifies that a message belongs to a specific message group (FIFO Queues only).|
|DelaySeconds|The length of time (in seconds) to delay a specific message (0 to 900).|
|Print Attribute Names|If attribute names are updated, the names in the payload reflect the update.|

See [Using Amazon SQS Message Attributes](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-message-attributes.html).

### Action - Send Visitor Data to Queue and Send Visitor Data to Queue (Batch)

#### Batch Limits

The Send Visitor Data to Queue (Batch) action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Maximum  number of requests: 10
* Maximum time since oldest request: 5 minutes
* Maximum size of requests: 1 MB


#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Queue|  &lt;ul&gt;&lt;li&gt;(Required) Select queue to send data to.&lt;/li&gt;&lt;li&gt;If your IAM policy does not grant `sqs:ListQueues` permission, you will need to manually enter a Custom Value&lt;/li&gt;&lt;li&gt;The custom value should be a URL. For example: `https://sqs.us-west-2.amazonaws.com/0123456789/queue_name`&lt;/li&gt;&lt;/ul&gt;|
|MessageGroupId|Specifies that a message belongs to a specific message group (FIFO Queues only).|
|DelaySeconds|The length of time (in seconds) to delay a specific message (0 to 900).|
| Include Current Visit Data With Visitor Data | Add the current visit data to the payload. This includes event visit data if Exclude Current Visit Event Data isn&#39;t selected. |
| Exclude Current Visit Event Data | Exclude event data from the current visit data. |
|Print Attribute Names| If attribute names are updated, the names in the payload reflect the update.|

### Action - Send Customized Data to Queue (Advanced) and Send Customized Data to Queue (Advanced Batch)

#### Batch Limits

The Send Customized Data to Queue (Advanced Batch) action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Maximum number of requests: 10
* Maximum time since oldest request: 5 minutes
* Maximum size of requests: 1 MB


#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Queue|  &lt;ul&gt;&lt;li&gt;(Required) Select queue to send data to.&lt;/li&gt;&lt;li&gt;If your IAM policy does not grant `sqs:ListQueues` permission, you will need to manually enter a Custom Value. The custom values should be a URL. For example: `https://sqs.us-west-2.amazonaws.com/0123456789/queue_name`&lt;/li&gt;&lt;/ul&gt;|
|MessageGroupId|Specifies that a message belongs to a specific message group (FIFO Queues only).|
|DelaySeconds|The length of time (in seconds) to delay a specific message (0 to 900).|
|Custom Message Definition||
|Message Template Variables|&lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation For example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Message Templates|  &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header or Body Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected into supported fields by name with double curly braces. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |
|Message Template Variables|&lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation For example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Message Templates|  &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either URL, URL Parameter, Header or Body Data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected into supported fields by name with double curly braces. For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |

See [Using Amazon SQS Message Attributes](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-message-attributes.html).


## Vendor Documentation

* [Access Control for Amazon SQS](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-authentication-and-access-control.html)
* [Switching to an IAM Role](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)
* [How to Use an External ID](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)
* [Using Amazon SQS Message Attributes](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-message-attributes.html)
* [How Amazon SQS Queues Work](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-how-it-works.html)
