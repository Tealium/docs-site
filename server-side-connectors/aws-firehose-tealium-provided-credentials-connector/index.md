---
title: AWS Firehose (Tealium-Provided Credentials) Connector Setup Guide
description: This article describes how to set up the AWS Firehose (Tealium Provided Credentials) connector.
url: https://docs.tealium.com/server-side-connectors/aws-firehose-tealium-provided-credentials-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Region**: (Required) Select a region.
* **Assume Role: ARN**: (Required) Provide Amazon Resource Name (ARN) of the role to assume. For example, `arn:aws:iam::222222222222:role/myrole`.
    * Ensure that the trust policy allows the Tealium root account (`arn:aws:iam::757913464184:root`) with an External ID condition.
    * We recommend including `TealiumFirehose` as a prefix in the IAM role name. 
    * For more information, see [AWS: Switch to an IAM Role](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)
* **Assume Role: Session Name**: Provide the session name of the role to assume.
* **Assume Role: External ID**: (Optional) Provide an external identifier.
    * For more information, see: [AWS: Access to AWS accounts owned by third parties](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)

### Add Tealium role to AWS account

Use the Tealium main AWS account ID, `757913464184`, as the principal and require an External ID condition. The following is an example trust policy to add to the **Trust** relationships tab of the IAM role in your AWS account. Replace `EXTERNAL_ID` with the exact value you configure in **Assume Role: External ID**. 

```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Principal&#34;: {
        &#34;AWS&#34;: &#34;arn:aws:iam::757913464184:root&#34;
      },
      &#34;Action&#34;: &#34;sts:AssumeRole&#34;,
      &#34;Condition&#34;: {
        &#34;StringEquals&#34;: {
          &#34;sts:ExternalId&#34;: &#34;EXTERNAL_ID&#34;
        }
      }
    }
  ]
}
```

#### Private cloud trust policy

For private cloud customers, Tealium uses a different AWS account ID: `111879511226`. The following is an example trust policy to add to the **Trust** relationships tab of the IAM role in your AWS account. Replace `EXTERNAL_ID` with the exact value you configure in **Assume Role: External ID**. 

```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Principal&#34;: {
        &#34;AWS&#34;: &#34;arn:aws:iam::111879511226:root&#34;
      },
      &#34;Action&#34;: &#34;sts:AssumeRole&#34;,
      &#34;Condition&#34;: {
        &#34;StringEquals&#34;: {
          &#34;sts:ExternalId&#34;: &#34;EXTERNAL_ID&#34;
        }
      }
    }
  ]
}
```

### IAM permissions policy

The following is a least‑privilege, single‑stream permissions policy that works with the preceding trust policies.

In the `Resource` field, replace the following placeholders:

* `REGION`: Your AWS region (for example, `us-west-2`).
* `ACCOUNT_ID`: Your AWS account ID.
* `MY_FIREHOSE_STREAM`: The Firehose delivery stream name you want Tealium to write to.

```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Sid&#34;: &#34;AllowListingDeliveryStreams&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;firehose:ListDeliveryStreams&#34;,
        &#34;firehose:DescribeDeliveryStream&#34;
      ],
      &#34;Resource&#34;: &#34;*&#34;
    },
    {
      &#34;Sid&#34;: &#34;AllowWritingToSpecificDeliveryStream&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;firehose:PutRecord&#34;,
        &#34;firehose:PutRecordBatch&#34;
      ],
      &#34;Resource&#34;: &#34;arn:aws:firehose:REGION:ACCOUNT_ID:deliverystream/MY_FIREHOSE_STREAM&#34;
    }
  ]
}
```

Attach this policy to the same IAM role whose trust policy is set to trust the Tealium account with an External ID (for private cloud: `arn:aws:iam::111879511226:root`, for all others `arn:aws:iam::757913464184:root`).

If you need Tealium to send to multiple delivery streams, do one of the following:

* Add additional ARNs as an array to `Resource` under `AllowWritingToSpecificDeliveryStream`.
* Use a pattern-based ARN (for example, all Tealium streams prefixed `tealium-`) if that fits the naming convention.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event Data to Delivery Stream | ✗ | ✓ |
| Send Customized Data to Delivery Stream (Advanced) | ✓ | ✓ |
| Send Log Event to Delivery Stream | ✗ | ✓ |
| Send Visitor Data to Delivery Stream | ✓ | ✗ |
| Send Customized Data to Delivery Stream (Batched) | ✓ | ✓ |
| Send Event Data to Delivery Stream (Batched) | ✗ | ✓ |

Enter a name for the action and select the action type.

The following section describes how to set up parameters and options for each action.

### Send Event Data to Delivery Stream

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Delivery Stream | &lt;ul&gt;&lt;li&gt;Select the delivery stream to send data to.&lt;/li&gt;&lt;li&gt;To see available streams, the `firehose:ListDeliveryStreams` permission must be granted.&lt;/li&gt;&lt;li&gt;For more information, see [AWS: Amazon Data Firehose Quota](https://docs.aws.amazon.com/firehose/latest/dev/limits.html).&lt;/ul&gt;&lt;/li&gt; |
| Record Suffix | &lt;ul&gt;&lt;li&gt;Suffix added to the end of each record to be used as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`.&lt;/ul&gt;&lt;/li&gt; |
| Print Attribute Names | If attribute names are updated, the names in the payload reflect the update. |

### Send Customized Data to Delivery Stream (Advanced)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Delivery Stream | &lt;ul&gt;&lt;li&gt;Select the delivery stream to send data to.&lt;/li&gt;&lt;li&gt;To see available streams, the `firehose:ListDeliveryStreams` permission must be granted.&lt;/li&gt;&lt;li&gt;For more information, see [AWS: Amazon Data Firehose Quota](https://docs.aws.amazon.com/firehose/latest/dev/limits.html).&lt;/ul&gt;&lt;/li&gt; |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`.&lt;/ul&gt;&lt;/li&gt; |
| Message Template Variables | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example, `items.name`.&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/ul&gt;&lt;/li&gt; |
| Message Templates | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either `URL`, `URL` parameter, header, or body data&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields.&lt;/li&gt;&lt;li&gt;For example, `{{SomeTemplateName}}`.&lt;/ul&gt;&lt;/li&gt; |

### Send Log Event to Delivery Stream

#### Parameters

| Parameter | Description |
| --- | --- |
| Delivery Stream | &lt;ul&gt;&lt;li&gt;Select the delivery stream to send data to.&lt;/li&gt;&lt;li&gt;To see available streams, the `firehose:ListDeliveryStreams` permission must be granted.&lt;/li&gt;&lt;li&gt;For more information, see [AWS: Amazon Data Firehose Quota](https://docs.aws.amazon.com/firehose/latest/dev/limits.html).&lt;/ul&gt;&lt;/li&gt; |
| Record Suffix | &lt;ul&gt;&lt;li&gt;Suffix added to the end of each record to be used as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`.&lt;/ul&gt;&lt;/li&gt; |

### Send Visitor Data to Delivery Stream

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Delivery Stream | &lt;ul&gt;&lt;li&gt;Select the delivery stream to send data to.&lt;/li&gt;&lt;li&gt;To see available streams, the `firehose:ListDeliveryStreams` permission must be granted.&lt;/li&gt;&lt;li&gt;For more information, see [AWS: Amazon Data Firehose Quota](https://docs.aws.amazon.com/firehose/latest/dev/limits.html).&lt;/ul&gt;&lt;/li&gt; |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`.&lt;/ul&gt;&lt;/li&gt; |
| Include Current Visit Data | Add the current visit data to the payload. This includes event visit data if Exclude Current Visit Event Data isn&#39;t selected. |
| Exclude Current Visit Event Data | Exclude event data from the current visit data. |
| Print Attribute Names | If attribute names are updated, the names in the payload reflect the update. |

### Send Customized Data to Delivery Stream (Batched)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Delivery Stream | &lt;ul&gt;&lt;li&gt;Select the delivery stream to send data to.&lt;/li&gt;&lt;li&gt;To see available streams, the `firehose:ListDeliveryStreams` permission must be granted.&lt;/li&gt;&lt;li&gt;For more information, see [AWS: Amazon Data Firehose Quota](https://docs.aws.amazon.com/firehose/latest/dev/limits.html).&lt;/ul&gt;&lt;/li&gt; |

#### Message Data


| **Parameter** | **Description** |
| --- | --- |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`.&lt;/ul&gt;&lt;/li&gt; |
| Message Template Variables | &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. For example, `items.name`.&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/ul&gt;&lt;/li&gt; |
| Message Templates | &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in either `URL`, `URL` parameter, header, or body data&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields.&lt;/li&gt;&lt;li&gt;For example, `{{SomeTemplateName}}`.&lt;/ul&gt;&lt;/li&gt; |

### Send Event Data to Delivery Stream (Batched)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Delivery Stream | &lt;ul&gt;&lt;li&gt;Select the delivery stream to send data to.&lt;/li&gt;&lt;li&gt;To see available streams, the `firehose:ListDeliveryStreams` permission must be granted.&lt;/li&gt;&lt;li&gt;For more information, see [AWS: Amazon Data Firehose Quota](https://docs.aws.amazon.com/firehose/latest/dev/limits.html).&lt;/ul&gt;&lt;/li&gt; |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`.&lt;/ul&gt;&lt;/li&gt; |
| Print Attribute Names | If attribute names are updated, the names in the payload reflect the update. |