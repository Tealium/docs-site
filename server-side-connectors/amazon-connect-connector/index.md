---
title: AWS Amazon Connect Connector Setup Guide
description: This article describes how to set up the Amazon Connect connector.
url: https://docs.tealium.com/server-side-connectors/amazon-connect-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Amazon Connect
* API Version: v1.0
* API Endpoint: `https://connect.{REGION}.amazonaws.com`
* Documentation: [Amazon Connect: StartOutboundVoiceContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartOutboundVoiceContact.html)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Authentication Type**: (Required) The type of authentication to use.
    * **Access Key**
        * **Access Key**: (Required) Provide your IAM user's access key. The associated IAM policy (for either IAM user or Assumed Role) must grant `kinesis:PutRecord` permission along with streams you want to send data to.
        * **Secret Key**: (Required) Provide your IAM user's secret key.
        * **Region**: (Required) Select the AWS Connect region you are using.
    * **STS**
        * **STS - Assume Role: ARN**: (Required) Amazon Resource Name assigned to the role to assume. For more information, see: [Switching to an IAM Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html).
        * **STS - Assume Role: Session Name**: (Required) Unique identifier of the assumed role session.
        * **STS - Assume Role: External ID**: (Optional) Unique identifier used by third parties when assuming roles in their customers' accounts. For more information, see: [AWS: Access to AWS accounts owned by third parties](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_third-party.html).
        * **Region**: (Required) Select the AWS Connect region you are using.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Start Outbound Voice Contact | ✓ | ✓ |
| Update Profile Attributes | ✓ | ✓ |
| Update Profile Attributes (Batch) | ✓ | ✓ |

Enter a name for the action and select the action type.

The following section describes how to set up parameters and options for each action.

### Start Outbound Voice Contact

#### Parameters

| Parameter | Description |
| --- | --- |
| Instance ID | (Required) The Amazon Connect instance identifier. |
| Queue ID | The queue for the call. If you specify a queue, the phone displayed for caller ID is the phone number specified in the queue. If you do not specify a queue, the queue defined in the flow is used. Either **Queue ID** or **Source Phone Number** are required. |
| Source Phone Number | The phone number associated with the Amazon Connect instance, in E.164 format. Either **Queue ID** or **Source Phone Number** are required.  |
| Contact Flow ID | (Required) The identifier of the flow for the outbound call. |

#### Vendor Parameters

| Parameter | Description |
| --- | --- |
| Destination Phone Number | (Required) Customer phone number in E.164 format. |
| Campaign ID | The campaign identifier of the outbound communication. The value must be 1 to 100 characters long. |
| Client Token | A unique, case-sensitive identifier to prevent duplicate requests. If not provided, the AWS SDK populates this field. The maximum length is 500 characters. |
| Description | Voice contact description in the agent's panel. The value must be 0 to 4096 characters long. |
| Name | (Required) Voice contact name shown in CCP. The value must be 0 to 1024 characters long. |
| Related Contact ID | Related `contactId` to link tasks/chats. The value must be 1 to 256 characters long. |
| Traffic Type | Traffic class. Possible values: `GENERAL` or `CAMPAIGN`. |

#### Answering Machine Detection Config

| Parameter | Description |
| --- | --- |
| Await Answer Machine Prompt | A boolean value that indicates whether to wait for the answering machine prompt. |
| Enable Answer Machine Detection | A boolean value that indicates whether answering machine detection is needed. If `true`, **Traffic Type** must be `CAMPAIGN`. |
| Attributes | A custom key-value pair using an attribute map. The attributes are standard Amazon Connect attributes, and can be accessed in flows just like any other contact attributes. There can be up to 32,768 UTF-8 bytes across all key-value pairs per contact. Attribute keys can include only alphanumeric, dash, and underscore characters. |

#### References

| Parameter | Description |
| --- | --- |
| Type | Type of the reference. Possible values: `URL`, `NUMBER`, `STRING`, `DATE`, `EMAIL`. |
| Value | Valid value for the reference. For example, a formatted URL that is displayed to an agent in the Contact Control Panel (CCP). If the type is `DATE`, the value must be in Unix Epoch time format. |

### Update Profile Attributes (Standard and Batched)

#### Batch Limits

This action lets you use batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 5 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Stream Name | (Required) Select stream to send data to. If your IAM policy does not grant `kinesis:ListStreams` permission, manually enter a custom value. |
| Region Override | If the Kinesis region and the Connect region differ, select the AWS Kinesis region that you are using. |

#### Message Options

| Parameter | Description |
| --- | --- |
| Partition Key | (Required) Determines which shard in the stream the data record is assigned to. |
| Explicit Hash Key | (Required) Used to explicitly determine the shard the data record is assigned to. |
| Sequence Number For Ordering | (Required) Guarantees strictly increasing sequence numbers, for messages from the same client and to the same partition key. |

#### Message Data

| Parameter | Description |
| --- | --- |
| Template Variables | (Required) Provide template variables as data input for Templates. Name nested template variables with the dot notation. For example, `items.name`. Nested template variables are typically built from data layer list attributes. For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).|
| Templates | (Required) Provide templates to be referenced in Data section. Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).|