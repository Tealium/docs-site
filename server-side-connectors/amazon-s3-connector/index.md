---
title: Amazon S3 Connector Setup Guide
description: This article describes how to set up the Amazon S3 connector.
url: https://docs.tealium.com/server-side-connectors/amazon-s3-connector/
---
## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 100,000
* Maximum time since oldest request: 10 minutes
* Maximum size of requests: 100 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Authentication Type**  
  * Select the authentication type. Available options are: **STS** and **Access Key**.
    * **STS**: Requires **Assume Role: ARN** and **Assume Role: Session Name** fields.
    * **Access Key**: Requires **AWS Access Key** and AWS Secret Access Key fields.
* **Region**  
  * (Required) Select a region.
* **STS - Assume Role: ARN**  
  * Required for STS authentication. Provide the Amazon Resource Name (ARN) of the role to assume.
  * For example, `arn:aws:iam:222222222222:role/myrole`.
  * For more information, see [AWS Identity and Access Management: Switch to an IAM role (AWS API)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html).
* **STS - Assume Role: Session Name**  
  * The name of the session for the role to assume.
  * Must be between 2 and 64 characters.
* **STS - Assume Role: External ID**  
  * Provide a third-party external identifier.
  * For more information, see [AWS Identity and Access Management: Access to AWS accounts owned by third parties](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_third-party.html).
* **Access Key - AWS Access Key**  
  * Required for **Access Key** authentication. Provide the AWS access key.
* **Access Key - AWS Secret Access Key**  
  * Required for **Access Key** authentication. Provide the AWS secret access key.

### Create a connection to AWS S3

Tealium requires a connection to an AWS S3 instance to display a list of buckets and upload event and audience data into S3 objects. You have two options for authentication:

* Provide an Access Key and Access Secret.
* Provide STS (Security Token Service) credentials.

 If the S3 objects are encrypted, you will need to add decrypt permission to the IAM user and KMS key policy. 

#### Access Key and Secret credentials

To find your AWS Access Key and Secret:

1. Log in to the AWS Management Console and go to the **IAM** (Identity and Access Management) service.
1. Click **Users** and then click **Add user**.
1. Enter a username. For example, `TealiumS3User`.
1. Attach policies to the user you have just created.
    1. In the **Permissions** tab, click **Attach existing policies directly**.
    1. Search for and attach the `AmazonS3FullAccess` policy for full access. To restrict access to a specific bucket, create a policy similar to the following example. In the example, `YOUR_BUCKET_NAME` is the bucket that Tealium would use to upload event and audience data into S3 objects:
    ```json
    {
      &#34;Version&#34;: &#34;2012-10-17&#34;,
      &#34;Statement&#34;: [
          {
                &#34;Effect&#34;: &#34;Allow&#34;,
                &#34;Action&#34;: [
                   &#34;s3:ListBucket&#34;,
                    &#34;s3:PutObject&#34;,
                    &#34;s3:GetObject&#34;,
                    &#34;s3:ListBucketMultipartUploads&#34;,
                    &#34;s3:ListMultipartUploadParts&#34;
                ],
                &#34;Resource&#34;: [
                    &#34;arn:aws:s3:::YOUR_BUCKET_NAME&#34;,
                    &#34;arn:aws:s3:::YOUR_BUCKET_NAME/*&#34;
                ]
            },
            // Add the following section if you are running on a private cloud
            // and require decryption
            {
                &#34;Effect&#34;: &#34;Allow&#34;,
                &#34;Action&#34;: [
                     &#34;kms:Decrypt&#34;,
                     &#34;kms:GenerateDataKey&#34;
                ],
                 &#34;Resource&#34;: &#34;arn:aws:kms:YOUR_REGION:111879511226:key/YOUR_KEY_ID&#34;
           }
        ]
    }
    ```
1. Create the keys.
    1. Go to the **Security credentials** tab and click **Create Access Key**.
    1. Copy the **Access Key ID** and **Secret Access Key**, and save them securely.
    1. If you are using a private cloud environment, add a statement to your key policy similar to the following:
    ```
    {
        &#34;Sid&#34;: &#34;AllowDecryptFromIAMUser&#34;,
        &#34;Effect&#34;: &#34;Allow&#34;,
        &#34;Principal&#34;: {
            &#34;AWS&#34;: &#34;arn:aws:iam::&lt;&lt;account-id&gt;&gt;:user/&lt;&lt;user-name&gt;&gt;&#34;
        },
        &#34;Action&#34;: [
            &#34;kms:Decrypt&#34;,
            &#34;kms:GenerateDataKey&#34;
        ],
        &#34;Resource&#34;: &#34;*&#34;
    }
    ```

#### STS credentials

To find your STS credentials:

1. Log in to the **AWS Management Console** and go to the **IAM** (Identity and Access Management) service.
1. Click **Roles** and then click **Create role**.
1. For the **Trusted entity** type, select the AWS account.
1. Select **Another AWS account** and enter the Tealium account ID:
    * For private cloud customers, the ID is `111879511226`.
    * For all other customers, the ID is `757913464184`.
1.  (Optional) Select the **Require external ID** checkbox and specify the external ID that you want to use. External IDs can be up to 256 characters long and can include alphanumeric characters (`A-Z`, `a-z`, `0-9`) and symbols, such as hyphens (`-`), underscores (`_`), and periods (`.`).
1. Enter a name for the role. The role name must start with TealiumS3. For example: `TealiumS3-test.`
1. Attach policies to the role.
    1.  In the **Permissions** tab, click **Attach existing policies directly**.
    1. Search for and attach the `AmazonS3FullAccess` policy for full access. To restrict access to a specific bucket, create a policy similar to the following example. In the example, `YOUR_BUCKET_NAME` is the bucket that Tealium would use to upload event and audience data into S3 objects:
    ```json
    {
        &#34;Version&#34;: &#34;2012-10-17&#34;,
        &#34;Statement&#34;: [
            {
                &#34;Effect&#34;: &#34;Allow&#34;,
                &#34;Action&#34;: [
                    &#34;s3:ListBucket&#34;,
                    &#34;s3:PutObject&#34;,
                    &#34;s3:GetObject&#34;,
                    &#34;s3:ListBucketMultipartUploads&#34;,
                    &#34;s3:ListMultipartUploadParts&#34;
                ],
                &#34;Resource&#34;: [
                    &#34;arn:aws:s3:::YOUR_BUCKET_NAME&#34;,
                    &#34;arn:aws:s3:::YOUR_BUCKET_NAME/*&#34;
                ]
            },
            // Add the following section if you are running on a private cloud
            // and require decryption
            {
                &#34;Effect&#34;: &#34;Allow&#34;,
                &#34;Principal&#34;: {
                &#34;AWS&#34;: &#34;arn:aws:iam::111879511226:user/YOUR_USER_NAME&#34;
             },
                &#34;Action&#34;: &#34;s3:GetObject&#34;,
                &#34;Resource&#34;: &#34;arn:aws:s3:::YOUR_BUCKET_NAME/*&#34;
            }
        ]
    }
    ```
1. Create a trust policy.
    1. Go to the **Trust relationships** tab and click **Edit trust** relationship.
    1. Ensure that the trust policy allows the specific external ID to use the role you created and that for private cloud customers, the ID is `111879511226`, and for all other customers, the ID is `757913464184`.
    1. Set the `EXTERNAL_ID` value for the connection to Tealium. The ID can be up to 256 characters long and can include alphanumeric characters (`A-Z`, `a-z`, `0-9`) and symbols, such as hyphens (`-`), underscores (`_`), and periods (`.`).
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

### Create a bucket

An S3 bucket is a storage container within AWS S3 used to store and organize data. In the connector configuration window, you can create a new bucket by clicking **Create Bucket** in the configuration step.

1. In the connector configuration screen, click **Create Bucket**.
1. Enter the bucket name.
1. Click **Create**.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Entire Event Data | ✗ | ✓ |
| Send Custom Event Data | ✗ | ✓ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Custom Visitor Data | ✓ | ✗ |
| Send Log Event | ✗ | ✓ |
| Send Entire Log Event | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Entire Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Bucket | Select the Amazon S3 bucket or provide a custom value. |
| File Path | Specify the path to the S3 object where you want the data to be appended. |
| File Path Suffix | If you want to dynamically add a suffix to the file path, such as an attribute with the current timestamp, select it here. This creates a unique file for each event and prevents overwriting existing files. If you enter multiple suffix values, they are separated by an underscore. |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`. &lt;/li&gt;&lt;li&gt;Available options are `Newline` and `No Delimiter`.&lt;/li&gt;&lt;/ul&gt; |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Consider that the payload names will reflect the update if the attribute names are updated. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Custom Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Bucket | Select the Amazon S3 bucket or provide a custom value. |
| File Path | Specify the path to the S3 object where you want the data to be appended. |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| Event Attribute | Define custom mappings between event attributes and vendor parameters. |
| File Path Suffix | If you want to dynamically add a suffix to the file path, such as an attribute with the current timestamp, select it here. This creates a unique file for each event and prevents overwriting existing files. If you enter multiple suffix values, they are separated by an underscore. |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`. &lt;/li&gt;&lt;li&gt;Available options are `Newline` and `No Delimiter`.&lt;/li&gt;&lt;/ul&gt; |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |
| Template Variables | &lt;ul&gt;&lt;li&gt;Provide template variables as data input for **Templates**.  For more information and usage examples, see  .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. Example: `items.name.`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| Templates | &lt;ul&gt;&lt;li&gt;Provide templates to be referenced in Event Parameters. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields, for example: `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt;|

### Send Entire Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Bucket | Select the Amazon S3 bucket or provide a custom value. |
| File Path | Specify the path to the S3 object where you want the data to be appended. |
| File Path Suffix | If you want to dynamically add a suffix to the file path, such as an attribute with the current timestamp, select it here. This creates a unique file for each event and prevents overwriting existing files. If you enter multiple suffix values, they are separated by an underscore. |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`. &lt;/li&gt;&lt;li&gt;Available options are `Newline` and `No Delimiter`.&lt;/li&gt;&lt;/ul&gt; |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Consider that the payload names will reflect the update if the attribute names are updated. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |
| Include All Visitor Events | Select to include current visit data with visitor data. |

### Send Custom Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Bucket | Select the Amazon S3 bucket or provide a custom value. |
| File Path | Specify the path to the S3 object where you want the data to be appended. |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| File Path Suffix | If you want to dynamically add a suffix to the file path, such as an attribute with the current timestamp, select it here. This creates a unique file for each event and prevents overwriting existing files. If you enter multiple suffix values, they are separated by an underscore. |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`. &lt;/li&gt;&lt;li&gt;Available options are `Newline` and `No Delimiter`.&lt;/li&gt;&lt;/ul&gt; |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |
| Template Variables | &lt;ul&gt;&lt;li&gt;Provide template variables as data input for **Templates**.  For more information and usage examples, see  .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. Example: `items.name.`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| Templates | &lt;ul&gt;&lt;li&gt;Provide templates to be referenced in Event Parameters. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields, for example: `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt;|

### Send Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Bucket | Select the Amazon S3 bucket or provide a custom value. |
| File Path | Specify the path to the S3 object where you want the data to be appended. |

#### Message Data

| **Parameter** | **Description** |
| --- | --- |
| Event Attribute | Define custom mappings between event attributes and vendor parameters. |
| File Path Suffix | If you want to dynamically add a suffix to the file path, such as an attribute with the current timestamp, select it here. This creates a unique file for each event and prevents overwriting existing files. If you enter multiple suffix values, they are separated by an underscore. |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`. &lt;/li&gt;&lt;li&gt;Available options are `Newline` and `No Delimiter`.&lt;/li&gt;&lt;/ul&gt; |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |
| Template Variables | &lt;ul&gt;&lt;li&gt;Provide template variables as data input for **Templates**.  For more information and usage examples, see  .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation. Example: `items.name.`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| Templates | &lt;ul&gt;&lt;li&gt;Provide templates to be referenced in Event Parameters. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields, for example: `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt;|

### Send Entire Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Bucket | Select the Amazon S3 bucket or provide a custom value. |
| File Path | Specify the path to the S3 object where you want the data to be appended. |
| File Path Suffix | If you want to dynamically add a suffix to the file path, such as an attribute with the current timestamp, select it here. This creates a unique file for each event and prevents overwriting existing files. If you enter multiple suffix values, they are separated by an underscore. |
| Record Suffix | &lt;ul&gt;&lt;li&gt;A suffix to add on the end of each record as a delimiter.&lt;/li&gt;&lt;li&gt;The default is `Newline`. &lt;/li&gt;&lt;li&gt;Available options are `Newline` and `No Delimiter`.&lt;/li&gt;&lt;/ul&gt; |