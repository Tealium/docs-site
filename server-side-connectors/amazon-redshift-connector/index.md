---
title: Amazon Redshift Connector Setup Guide
description: This article describes how to set up the Amazon Redshift connector.
url: https://docs.tealium.com/server-side-connectors/amazon-redshift-connector/
---
## Working with large visitor profiles

The [**Send Entire Visitor Data** actions](#send-entire-visitor-data-micro-batch) embed the full visitor JSON into each SQL INSERT statement. The Redshift Data API enforces a 100 kB limit per SQL statement, so if your visitor profiles exceed this limit, the connector action fails with the error: `ValidationException: Query string size exceeds 100 kB`.

To avoid this issue, follow these guidelines:

* **Use Send Entire Visitor Data for small visitor profiles.**  
Visitor profiles larger than a few kilobytes increase the risk of exceeding the limit. Use this action if your visitor profiles are well under the 100 kB limit. Use the [visitor lookup tool]() to fetch full profiles and evaluate their size.
* **Send mapped attributes instead of the entire profile.**  
Use a [**Send Custom Visitor Data**](#send-custom-visitor-data-micro-batch) action to select only the attributes you need, rather than sending the full visitor JSON.
* **Use S3 and Redshift for bulk or historical loads.**  
For large visitor JSON payloads or one-off bulk uploads, send visitor data to the [S3 connector](), then load data into Redshift using the COPY command. For more information, see [Amazon Redshift: Using the COPY command to load from Amazon S3](https://docs.aws.amazon.com/redshift/latest/dg/t_loading-tables-from-s3.html).
* **Use the Webhook (JDBC) connector for large payloads.**
The [Webhook (JDBC) connector]() connects directly to Redshift over JDBC, bypassing the Redshift Data API 100 kB limit. Use this option when your visitor profiles exceed 100 kB.

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Authentication Type**  
  * Select the authentication type:
    * **STS**: Requires the following fields **Assume Role: ARN**, **Assume Role: Session Name**. For more information, see [STS credentials](#sts-credentials).
    * **Access Key**: Requires the following fields **AWS Access Key** and **AWS Secret Access Key**. For more information, see [Access Key and Secret credentials](#access-key-and-secret-credentials).
* **STS - Assume Role: ARN**  
  * Required for STS authentication. Provide the Amazon Resource Name (ARN) of the role to assume.
  * For example, `arn:aws:iam:222222222222:role/myrole`.
  * For more information, see [AWS: Switching to an IAM Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html).
* **STS - Assume Role: Session Name**  
  * Required for STS authentication. Provide the session name of the role to assume.
  * Minimum length of 2, maximum length of 64.
* **STS - Assume Role: External ID**  
  * Provide a third-party external identifier.
  * For more information, see [AWS: Access to AWS accounts owned by third parties](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_third-party.html).
* **Access Key - AWS Access Key**  
  * Required for Access Key authentication. Provide the AWS access key.
* **Access Key - AWS Secret Access Key**  
  * Required for Access Key authentication. Provide the AWS secret access key.
* **Region**  
  * (Required) Select a region.
* **Secret Name**  
  * (Optional) If you are using the AWS Secrets Manager method to access Redshift,  provide your Secret Name so Tealium can dynamically pull the Secret ARN to use on the Redshift connection.
* **Workgroup Name**  
  * Required if **Cluster Identifier** isn&#39;t provided. If you are accessing a Redshift SERVERLESS instance, provide your workgroup name.
* **Cluster Identifier**  
  * Required if **Workgroup Name** isn&#39;t provided. If you are using a Redshift Cluster, provide the cluster identifier.
* **Database Name**  
  * (Optional) Provide your database name. Default value: `dev`.

### Create a connection to AWS Redshift

Tealium requires a connection to an AWS Redshift instance to display a list of clusters, workspaces, databases, and upload event and audience data into your Redshift tables. You have two options for authentication:

* [Provide an Access Key and Access Secret](#access-key-and-secret-credentials).
* [Provide STS credentials](#sts-credentials).

#### Access Key and Secret credentials

To find your AWS Access Key and Secret:

1. Log in to the AWS Management Console and go to the **IAM** (Identity and Access Management) service.
1. Click **Users** and then click **Add user**.
1. Enter a username. For example, `TealiumRedshiftUser`.
1. Attach policies to the role. For more information, see [Attach policies](#attach-policies).
1. Create the keys.
    * Go to the **Security credentials** tab and click **Create Access Key**.
    * Copy the **Access Key ID** and **Secret Access Key**, and save them securely.

#### STS credentials

To find your STS credentials:

1. Log in to the AWS Management Console and go to the **IAM** (Identity and Access Management) service.
1. Click **Roles**, and then click **Create role**.
1. Under **Trusted entity type**, select the AWS account.
1. Select Another AWS account and enter the Tealium account ID: `757913464184`.
1. (Optional) Select the **Require external ID** checkbox and specify the external ID that you want to use. External IDs can be up to 256 characters long and can include alphanumeric characters (`A-Z`, `a-z`, `0-9`) and symbols, such as hyphens (`-`), underscores (`_`), and periods (`.`).
1. Enter a name for the role. The role name must start with `TealiumRedshift`. For example: `TealiumRedshift-test`.
1. Attach policies to the role. For more information, see [Attach policies](#attach-policies).
1. Create a trust policy.
    * Go to the **Trust relationships** tab and click **Edit trust relationship**.
    * Ensure that the trust policy allows the specific external ID to use the role you created and that the Tealium production account ID is `757913464184`.
    * Set the `EXTERNAL_ID` value for the connection to Tealium. The ID can be up to 256 characters long and can include alphanumeric characters (`A-Z`, `a-z`, `0-9`) and symbols, such as hyphens (`-`), underscores (`_`), and periods (`.`).
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

#### Attach policies

To attach the policies:

1. In the **Permissions** tab, click **Attach existing policies directly**.
    1. Full access
        * Search for and attach the `SecretsManagerReadWrite`, `AmazonRedshiftAllCommandsFullAccess` and `AmazonRedshiftDataFullAccess` policies for full access. 
    1. Restricted access
        * To restrict access to a specific cluster, create a policy similar to the following example. In the example, `YOUR_CLUSTER_ARN` is the cluster that Tealium would use to insert event and audience data into your `YOUR_DATABASE_ARN` Redshift tables:
        ```json
        {
          &#34;Version&#34;: &#34;2012-10-17&#34;,
          &#34;Statement&#34;: [
            {
              &#34;Sid&#34;: &#34;RedshiftClusterManagement&#34;,
              &#34;Effect&#34;: &#34;Allow&#34;,
              &#34;Action&#34;: [
                &#34;redshift:DescribeClusters&#34;,
                &#34;redshift:GetClusterCredentials&#34;,
                &#34;redshift:GetClusterCredentialsWithIAM&#34;
              ],
              &#34;Resource&#34;: &#34;arn:aws:redshift:YOUR_REGION:YOUR_ACCOUNT_ID:cluster/YOUR_CLUSTER_ARN&#34;
            },
            {
              &#34;Sid&#34;: &#34;RedshiftDataAPI&#34;,
              &#34;Effect&#34;: &#34;Allow&#34;,
              &#34;Action&#34;: [
                &#34;redshift-data:ExecuteStatement&#34;,
                &#34;redshift-data:BatchExecuteStatement&#34;,
                &#34;redshift-data:DescribeStatement&#34;,
                &#34;redshift-data:GetStatementResult&#34;,
                &#34;redshift-data:ListStatements&#34;
              ],
              &#34;Resource&#34;: &#34;arn:aws:redshift:YOUR_REGION:YOUR_ACCOUNT_ID:database/YOUR_DATABASE_ARN&#34;
            },
            {
              &#34;Sid&#34;: &#34;SecretsManagerAccess&#34;,
              &#34;Effect&#34;: &#34;Allow&#34;,
              &#34;Action&#34;: [
                &#34;secretsmanager:GetSecretValue&#34;,
                &#34;secretsmanager:DescribeSecret&#34;,
                &#34;secretsmanager:ListSecrets&#34;
              ],
              &#34;Resource&#34;: &#34;arn:aws:secretsmanager:YOUR_REGION:YOUR_ACCOUNT_ID:secret/YOUR_SECRET_ARN&#34;
            }
          ]
        }
        ```

        * To restrict access to a specific workgroup, create a policy similar to the following example. In the example, `YOUR_WORKGROUP_ARN` is the cluster that Tealium would use to insert event and audience data into `YOUR_DATABASE_ARN` Redshift tables:

        ```json
        {
          &#34;Version&#34;: &#34;2012-10-17&#34;,
          &#34;Statement&#34;: [
            {
              &#34;Sid&#34;: &#34;RedshiftServerlessAccess&#34;,
              &#34;Effect&#34;: &#34;Allow&#34;,
              &#34;Action&#34;: [
                &#34;redshift-serverless:GetWorkgroup&#34;,
                &#34;redshift-serverless:GetCredentials&#34;,
                &#34;redshift-serverless:ListWorkgroups&#34;
              ],
              &#34;Resource&#34;: &#34;arn:aws:redshift-serverless:YOUR_REGION:YOUR_ACCOUNT_ID:workgroup/YOUR_WORKGROUP_ARN&#34;
            },
            {
              &#34;Sid&#34;: &#34;RedshiftDataAPI&#34;,
              &#34;Effect&#34;: &#34;Allow&#34;,
              &#34;Action&#34;: [
                &#34;redshift-data:ExecuteStatement&#34;,
                &#34;redshift-data:BatchExecuteStatement&#34;,
                &#34;redshift-data:DescribeStatement&#34;,
                &#34;redshift-data:GetStatementResult&#34;,
                &#34;redshift-data:ListStatements&#34;
              ],
              &#34;Resource&#34;: &#34;arn:aws:redshift:YOUR_REGION:YOUR_ACCOUNT_ID:database/YOUR_DATABASE_ARN&#34;
            },
            {
              &#34;Sid&#34;: &#34;SecretsManagerAccess&#34;,
              &#34;Effect&#34;: &#34;Allow&#34;,
              &#34;Action&#34;: [
                &#34;secretsmanager:GetSecretValue&#34;,
                &#34;secretsmanager:DescribeSecret&#34;,
                &#34;secretsmanager:ListSecrets&#34;
              ],
              &#34;Resource&#34;: &#34;arn:aws:secretsmanager:YOUR_REGION:YOUR_ACCOUNT_ID:secret/YOUR_SECRET_ARN&#34;
            }
          ]
        }
        ```

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Entire Event Data (Micro-batch) | ✗ | ✓ |
| Send Entire Event Data (Batch) | ✗ | ✓ |
| Send Custom Event Data (Micro-batch) | ✗ | ✓ |
| Send Custom Event Data (Batch) | ✗ | ✓ |
| Send Entire Visitor Data (Micro-batch) | ✓ | ✗ |
| Send Entire Visitor Data (Batch) | ✓ | ✗ |
| Send Custom Visitor Data (Micro-batch) | ✓ | ✗ |
| Send Custom Visitor Data (Batch) | ✓ | ✗ |
| Execute custom statement (Batch) | ✓ | ✓ |
| Send Entire Log Event (Micro-batch) | ✗ | ✓ |
| Send Log Event (Micro-batch) | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Entire Event Data (Micro-batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50
* Max time since oldest request: 16 minutes

#### Parameters

| Parameter | Description |
| --- | --- |
| Schema | Provide the schema name you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Column to record the Payload | Choose the `SUPER` column to record the payload. |
| Column to record the Timestamp | Choose the column to record the Timestamp. Not needed if you already have a **timestamp** column set to **default sysdate** in your table. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Consider that the payload names will reflect the update if the attribute names are updated. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `16` minutes. The default value is `5` minutes. |

### Send Entire Event Data (Batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 2,000
* Max time since oldest request: 60 minutes

#### Parameters

| Parameter | Description |
| --- | --- |
| Schema | Provide the schema name you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Column to record the Payload | Choose the `SUPER` column to record the payload. |
| Column to record the Timestamp | Choose the column to record the Timestamp. Not needed if you already have a **timestamp** column set to **default sysdate** in your table. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Consider that the payload names will reflect the update if the attribute names are updated. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `15` and `60` minutes. The default value is `30` minutes. |

### Send Custom Event Data (Micro-batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50
* Max time since oldest request: 16 minutes

#### Parameters

Map attributes to columns of the table.

| Parameter | Description |
| --- | --- |
| Schema | Provide the schema name you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Batch Time To Live |Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `16` minutes. The default value is `5` minutes. |

### Send Custom Event Data (Batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 2,000
* Max time since oldest request: 60 minutes

#### Parameters

Map attributes to columns of the table.

| Parameter | Description |
| --- | --- |
| Schema | Provide the schema name you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Batch Time To Live |Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `15` and `60` minutes. The default value is `30` minutes. |

### Send Entire Visitor Data (Micro-batch)


The Redshift Data API limits SQL statements to 100 kB. If visitor JSON payloads exceed this limit, the connector action fails.
For guidelines on avoiding this issue, see [Working with large visitor profiles](#working-with-large-visitor-profiles).


#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50
* Max time since oldest request: 16 minutes

#### Parameters

| Parameter | Description |
| --- | --- |
| Schema | Provide the schema name you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Column to record the Payload | Choose the `SUPER` column to record the payload. |
| Column to record the Timestamp | Choose the column to record the Timestamp. Not needed if you already have a **timestamp** column set to **default sysdate** in your table. |
| Include All Visitor Events | Include Current Visit Data with Visitor Data. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Consider that the payload names will reflect the update if the attribute names are updated. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `16` minutes. The default value is `5` minutes. |

### Send Entire Visitor Data (Batch)


The Redshift Data API limits SQL statements to 100 kB. If visitor JSON payloads exceed this limit, the connector action fails.
For guidelines on avoiding this issue, see [Working with large visitor profiles](#working-with-large-visitor-profiles).


#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 2,000
* Max time since oldest request: 60 minutes

#### Parameters

| Parameter | Description |
| --- | --- |
| Schema | Provide the schema name you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Column to record the Payload | Choose the `SUPER` column to record the payload. |
| Column to record the Timestamp | Choose the column to record the Timestamp. Not needed if you already have a **timestamp** column set to **default sysdate** in your table. |
| Include All Visitor Events | Include Current Visit Data with Visitor Data. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Consider that the payload names reflect the update if the attribute names are updated. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `15` and `60` minutes. The default value is `30` minutes. |

### Send Custom Visitor Data (Micro-batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50
* Max time since oldest request: 16 minutes

#### Parameters

Map attributes to columns of the table.

| Parameter | Description |
| --- | --- |
| Schema | Provide the schema name you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `16` minutes. The default value is `5` minutes. |

### Send Custom Visitor Data (Batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 2,000
* Max time since oldest request: 60 minutes

#### Parameters

Map attributes to columns of the table.

| Parameter | Description |
| --- | --- |
| Schema | Provide the schema name you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `15` and `60` minutes. The default value is `15` minutes. |

### Execute custom statement (Batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 40
* Max time since oldest request: 60 minutes

#### Parameters

| Parameter | Description |
| --- | --- |
| Schema | Provide the schema name you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Query Parameters | Map the parameters to the placeholder to replace in the query. You must map at least one parameter. |
| Query | Specify the raw statement to pass into the `SQL` attribute. Only `INSERT`, `UPDATE`, or `MERGE` statements are allowed. Add `:` before the attribute name to reference the variable. For more information, see [Query example](#query-example).|
| Batch Time To Live | The time to wait before sending the batch. This value can be between `1` and `60` minutes. The default value is `15` minutes. |

#### Query example

If you add a mapping in the **Query Parameters** section such as `my_boolean_tealium_attribute = MY_BOOLEAN_PARAM`, reference that parameter using `:MY_BOOLEAN_PARAM` in the query.

Example query where the following query parameters have been mapped: `MY_STRING_PARAM`, `MY_BOOLEAN_PARAM`, `ANOTHER_PARAM`, `MY_PARAM`.

```sql
INSERT INTO redshift_table
  (key1, key2) VALUES (&#39;:MY_STRING_PARAM&#39;, :MY_BOOLEAN_PARAM);
UPDATE redshift_table SET
  key1 = &#39;:MY_STRING_PARAM&#39;,
  key2 = :MY_BOOLEAN_PARAM
WHERE
  key3 = &#39;:ANOTHER_PARAM&#39;;
UPDATE redshift_table
  SET key2 = (SELECT new_key2 FROM source_table WHERE source_table.key1 = redshift_table.key1)
WHERE EXISTS
  (SELECT 1 FROM source_table WHERE source_table.key1 LIKE %:MY_PARAM%);
```

#### Debug

If Tealium returns successful responses but data does not appear in Redshift, the SQL statement may be rejected by Redshift after it is accepted by Tealium.

To investigate:

1. Run a [trace]() and note the ID from the response body of a successful call.
1. Use the [Amazon Redshift Data API](https://docs.aws.amazon.com/redshift-data/latest/APIReference/API_DescribeStatement.html) to check the details of the SQL statement.

Send the following request, replacing the `Id` value with the ID from your trace:

```http
POST / HTTP/1.1
Host: redshift-data.us-east-1.amazonaws.com
X-Amz-Target: RedshiftData.DescribeStatement
Content-Type: application/x-amz-json-1.1
Authorization: AUTHORIZATION_HEADER
X-Amz-Date: TIMESTAMP

{
    &#34;Id&#34;: &#34;37eb2735-b467-4852-884b-0f536970bf7e&#34;
}
```

The response includes the statement status and any error message returned by Redshift.

### Send Entire Log Event (Micro-batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50
* Max time since oldest request: 16 minutes

#### Parameters

| Parameter | Description |
| --- | --- |
| Schema | Provide the schema name you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Column to record the Payload | Choose the `SUPER` column to record the payload. |
| Column to record the Timestamp | Select the column to record the Timestamp. Not needed if you already have a `timestamp` column set to `default sysdate` in your table. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `16` minutes. The default value is `5` minutes. |

### Send Log Event (Micro-batch)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50
* Max time since oldest request: 16 minutes

#### Parameters

| Parameter | Description |
| --- | --- |
| Schema | Provide the schema name you want to connect to. |
| Table | Provide the table name you want to connect to. |
| Log event resource attributes | These fields capture information about the entity for which telemetry is recorded. |
| Log event HTTP attributes | These fields log the HTTP requests and responses within the logging system. To map the entire `http` array to a single column, map the `http` attribute. |
| Log event result attributes | These fields log the outcome of the operation, detailing whether it was successful or if it encountered errors. |
| Log event other attributes | These fields provide additional metadata about the logged events. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `16` minutes. The default value is `5` minutes. |
