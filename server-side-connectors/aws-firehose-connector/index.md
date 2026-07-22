---
title: AWS Firehose Connector Setup Guide
description: This article describes how to set up the AWS Firehose connector.
url: https://docs.tealium.com/server-side-connectors/aws-firehose-connector/
---
## Requirements

* An AWS account.
* (Required) **firehose:PutRecord** permission.
* (Optional) **firehose:ListDeliveryStreams** permission.
* Delivery stream to send data to.

## Configure settings

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

To configure your vendor, follow these steps:

1. In the **Configure tab**, provide a title for the connector instance.
1. Provide your IAM user access and secret key. 
<blockquote>
The policy statement attached to your IAM user instance must include the **firehose:PutRecord** permission and allow the Tealium root account (`arn:aws:iam::757913464184:root`) with an External ID condition. For more information about policies for Firehose, see: [AWS: Controlling access with Amazon Data Firehose](https://docs.aws.amazon.com/firehose/latest/dev/controlling-access.html).
</blockquote>

1. Select the region where you want to make the API calls.
1. **Assume Role Parameters**: Required only if your IAM User is not set up with all necessary permissions. The IAM role name must include the `TealiumFirehose` prefix. For more information, see [AWS: Switching to an IAM Role](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html).
  * **ARN**: (Required) Amazon Resource Name assigned to the role to assume.
  * **Session Name**: (Required) Unique identifier of the assumed role session.
  * **External ID**: (Optional) Unique identifier used by third parties when assuming roles in their customers' accounts. For more information, see: [AWS: Access to AWS accounts owned by third parties](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html).
1. Click **Test Connection** to verify API connectivity with the provided credentials.

## Actions

| Action Name | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Send Event Data to Delivery Stream | ✗ | ✓ |
| Send Visitor Data to Delivery Stream | ✓ | ✗ |
| Send Customized Data to Delivery Stream (Advanced) | ✓ | ✓ |
| Send Log Event to Delivery Stream | ✗ | ✓ |
| Send Customized Data to Delivery Stream (Batched) | ✓ | ✓ |
| Send Event Data to Delivery Stream (Batched) | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu. The following section describes how to set up parameters and options for each action.

### Send Event Data to Delivery Stream

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Delivery Stream | (Required) Select the delivery stream to send data to. To see available streams, the `firehose:ListDeliveryStreams` permission must be granted. |
| Record Suffix | Select a value to append to each record as a delimiter.<br>Options:<ul><li>`Newline (\n)` (default) - Adds a return character to the end of the record.</li><li>`No Delimiter` - Nothing is added to the record.</li></ul> |
| Print Attribute Names | Select this option to display names for each event data attribute in the message payload. |

### Send Visitor Data to Delivery Stream

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Delivery Stream | (Required) Select the delivery stream to send data to. To see available streams, the `firehose:ListDeliveryStreams` permission must be granted. |
| Record Suffix | Select a value to append to each record as a delimiter.<br>Options:<ul><li>`Newline (\n)` (default) - Adds a return character to the end of the record.</li><li>`No Delimiter` - Nothing is added to the record.</li></ul> |
| Include Current Visit Data | Add the current visit data to the payload. This includes event visit data if Exclude Current Visit Event Data isn't selected.  |
| Exclude Current Visit Event Data | Exclude event data from the current visit data. |
| Print Attribute Names | Select this option to display names for each visitor data Attribute in the message payload. |

### Send Customized Data to Delivery Stream (Advanced)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Delivery Stream | (Required) Select the delivery stream to send data to. To see available streams, the `firehose:ListDeliveryStreams` permission must be granted. |
| Record Suffix | Select a value to append to each record as a delimiter.<br>Options:<ul><li>`Newline (\n)` (default) - Adds a return character to the end of the record.</li><li>`No Delimiter` - Nothing is added to the record.</li></ul> |
| Message Data | (Required) Construct a custom message body. Map attributes to names in a simple one-level JSON format, or reference a template name enclosed in double curly braces and select the **Custom Message Definition** option.  |
| Message Template Variables | Map attributes to template variable names. Template variables are available for substitution and rendering of all templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/). |
| Message Templates | Provide one or more templates to render. Typically, a single template is used to construct a message data. For more information about syntax and extensions, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/). |

### Send Log Event to Delivery Stream

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Delivery Stream | (Required) Select the delivery stream to send data to. To see available streams, the `firehose:ListDeliveryStreams` permission must be granted. |
| Record Suffix | Select a value to append to each record as a delimiter.<br>Options:<ul><li>`Newline (\n)` (default) - Adds a return character to the end of the record.</li><li>`No Delimiter` - Nothing is added to the record.</li></ul> |

### Send Customized Data to Delivery Stream (Batched)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 4 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Delivery Stream | Select the delivery stream to send data to. To see available streams, the `firehose:ListDeliveryStreams` permission must be granted. There are limits on the Amazon Kinesis Data Firehose delivery stream. For more information, see [AWS: Amazon Data Firehose Quota](https://docs.aws.amazon.com/firehose/latest/dev/limits.html). |
| Record Suffix | Select a value to append to each record as a delimiter.<br>Options:<ul><li>`Newline (\n)` (default) - Adds a return character to the end of the record.</li><li>`No Delimiter` - Nothing is added to the record.</li></ul> |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| Message Template Variables | Map attributes to template variable names. Template variables are available for substitution and rendering of all templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/). |
| Message Templates | Provide one or more templates to render. Typically, a single template is used to construct a message data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/). |

### Send Event Data to Delivery Stream (Batched)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 4 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Delivery Stream | Select the delivery stream to send data to. To see available streams, the `firehose:ListDeliveryStreams` permission must be granted. There are limits on the Amazon Kinesis Data Firehose delivery stream. For more information, see [AWS: Amazon Data Firehose Quota](https://docs.aws.amazon.com/firehose/latest/dev/limits.html). |
| Record Suffix | Select a value to append to each record as a delimiter.<br>Options:<ul><li>`Newline (\n)` (default) - Adds a return character to the end of the record.</li><li>`No Delimiter` - Nothing is added to the record.</li></ul> |
| Print Attribute Names | If attribute names get updated, the names in the payload will reflect the update. |

## Vendor documentation

* [AWS: What is Amazon Data Firehose?](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)
* [AWS: Amazon Data Firehose Quota](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)
* [AWS: Controlling access with Amazon Data Firehose](https://docs.aws.amazon.com/firehose/latest/dev/controlling-access.html)
* [AWS: Switch to an IAM role (AWS API)](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)
* [AWS: Access to AWS accounts owned by third parties](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)