---
title: Databricks Connector Setup Guide
description: This article describes how to set up the Databricks connector.
url: https://docs.tealium.com/server-side-connectors/databricks-customer-provided-storage-connector/
---

<blockquote>
This connector is only available by using [the new connectors interface](https://docs.tealium.com/about-connectors/) available by clicking **Connectors** in the left navigation.
</blockquote>


## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Entire Event Data | ✗ | ✓ |
| Send Custom Event Data | ✗ | ✓ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Custom Visitor Data | ✓ | ✗ |
| Send Entire Event Data (Batch) | ✗ | ✓ |
| Send Custom Event Data (Batch) | ✗ | ✓ |
| Send Entire Visitor Data (Batch) | ✓ | ✗ |
| Send Custom Visitor Data (Batch) | ✓ | ✗ |
| Send Log Event | ✗ | ✓ |
| Send Entire Log Event | ✗ | ✓ |


## How it works

The Databricks connector requires two sets of connections:

* Tealium to a compatible cloud storage solution (AWS S3, Azure Blob Storage or Google Cloud Storage).
* Databricks to that same cloud storage solution.

### Tealium to cloud storage connection

Tealium requires a connection to a Databricks Unity Catalog Volume, AWS S3, Azure Blob Storage, or Google Cloud Storage instance to list buckets and upload event and audience data into cloud storage objects and files. You have the following options for authentication for the Databricks connector:

* [Databricks Unity Catalog](#databricks-unity-catalog-settings)
    * Provide a client ID and client secret (OAuth).
* [AWS S3](#aws-s3-settings)
    * Provide an Access Key and Access Secret.
    * Provide STS (Security Token Service) credentials.
* [Azure Blob Storage](#azure-blob-storage-settings)
    * Client credentials.
    * Authorization Code flow (SSO).
    * Shared Access Signature (SAS).
* [Google Cloud Storage](#google-cloud-storage-settings)
    * Sign in with Google (SSO).

#### Databricks Unity Catalog settings

##### Client ID and secret credentials

To generate new OAuth credentials for your Databricks account:

1. Log in to your Databricks instance.
2. Go to your workspace.
3. On the top-right corner of the screen, go to **Settings > Identity and access > Service principals**.
4. Create a new service principal or click on an existing one.
5. Click the **Secrets** tab and click **Generate secret**.
6. Click the **Permissions** tab and make sure that your service principal is assigned to the role **Service principal: User**.

#### AWS S3 settings

##### Access Key and Secret credentials

To find your AWS Access Key and Secret:

1. Log in to the AWS Management Console and go to the IAM (Identity and Access Management) service.
1. Click **Users** and then **Add user**.
1. Enter a username. For example, `TealiumS3User`.
1. Attach policies to the user you have just created.
    1. In the **Permissions** tab, click **Attach existing policies directly**.
    1. Search for and attach the `AmazonS3FullAccess` policy, for full access. If you want to restrict access to a specific bucket, you can write a policy similar to the example below. In this example, `YOUR_BUCKET_NAME` is the bucket that Tealium would use to upload event and audience data into S3 objects.
        ```json
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                        "s3:ListBucket",
                        "s3:PutObject",
                        "s3:GetObject",
                        "s3:ListBucketMultipartUploads",
                        "s3:ListMultipartUploadParts"
                    ],
                    "Resource": [
                        "arn:aws:s3:::YOUR_BUCKET_NAME",
                        "arn:aws:s3:::YOUR_BUCKET_NAME/*"
                    ]
                }
            ]
        }
        ```
1. Create the keys.
    1. Go to the **Security credentials** tab and click **Create Access Key**.
    1. Copy the **Access Key ID** and **Secret Access Key** and save them securely.

##### STS credentials settings

1. Log in to the AWS Management Console and go to the IAM (Identity and Access Management) service.
1. Click **Roles** and then **Create role**.
1. For the **Trusted entity** type, select the AWS account.
1. Select **Another AWS account** and specify the Tealium account ID: `757913464184`.
1. (Optional) Check the **Require external ID** checkbox and specify the external ID that you want to use. External IDs can be up to 256 characters long and can include alphanumeric characters (`A-Z`, `a-z`, `0-9`) and symbols, such as hyphens (`-`), underscores (`_`), and periods (`.`).
1. Enter a name for the role. The role name must start with `tealium-databricks`. For example, `tealium-databricks-s3-test`.
1. Attach policies to the role.
    1. In the **Permissions** tab, click **Attach existing policies directly**.
    1. Search for and attach the `AmazonS3FullAccess` policy, for full access. If you want to restrict access to a specific bucket, you can write a policy similar to the example below. In this example, `YOUR_BUCKET_NAME` is the bucket that Tealium would use to upload event and audience data into S3 objects.
        ```json
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                        "s3:ListBucket",
                        "s3:PutObject",
                        "s3:GetObject",
                        "s3:ListBucketMultipartUploads",
                        "s3:ListMultipartUploadParts"
                    ],
                    "Resource": [
                        "arn:aws:s3:::YOUR_BUCKET_NAME",
                        "arn:aws:s3:::YOUR_BUCKET_NAME/*"
                    ]
                }
            ]
        }
        
        ```
1. Create a trust policy.
    1. Go to the **Trust relationships** tab and click **Edit trust relationship**.
    1. Ensure the trust policy allows the specific external ID to the role you created and that the Tealium production account ID is `757913464184` as seen in the example below.
    1. Set the `EXTERNAL_ID` value for the connection to Tealium. The ID can be up to 256 characters long and can include alphanumeric characters (`A-Z`, `a-z`, `0-9`) and symbols, such as hyphens (`-`), underscores (`_`), and periods (`.`).
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::757913464184:root"
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "sts:ExternalId": "EXTERNAL_ID"
                }
            }
        }
    ]
}
```

#### Azure Blob Storage settings

##### Client credentials

To retrieve the tenant ID, client ID, and client secret for an application in Azure,  use the following steps:

**Step 1: Access Azure Portal**

1. Go to Azure Portal.
1. Sign in with your Azure account.

**Step 2: Go to the App Registration**

1. In the search bar at the top, enter `Azure Active Directory` and select it.
1. In the left menu, click **App registrations**.
1. Locate your registered application.

**Step 3: Find the Tenant ID & Client ID**

1. Click your application.
1. In the **Overview** section, locate the following information:
    * **Tenant ID** (also known as **Directory ID**) is listed under **Tenant ID**.
    * **Client ID** (also known as **Application ID**) is displayed as **Application (client) ID**.

**Step 4: Generate Client Secret**

1. In the left menu, go to **Certificates & secrets**.
1. Under **Client secrets**, click **New client secret**.
1. Provide a description and select an expiration time.
1. Click **Add**.
1. Once generated, copy the client secret immediately, because you won’t be able to view it again after leaving the page.

##### Shared Access Signature (SAS)

To generate a Shared Access Signature (SAS) token in Azure, use the following steps:

**Step 1: Access Azure Portal**

1. Go to the Azure Portal.
1. Sign in with your Azure account.

**Step 2: Go to Storage Account**

1. In the search bar, enter `Storage accounts` and select it.
1. Choose the storage account where you want to generate the SAS token.

**Step 3: Generate SAS Token**

Option 1: Use the Azure Portal

1. In the **Storage Account**, go to **Shared access signature** under the **Security + networking** section.
1. Configure the permissions needed (`Read`, `Write`, `Delete`, `List`, etc.).
1. Set the expiration date and time to define how long the token remains valid.
1. Choose the allowed services (`Blob`, `File`, `Queue`, and `Table`).
1. Click **Generate SAS and connection string**.
1. Copy the SAS token or the connection string, which contains the SAS token.

Option 2: Use Azure Storage Explorer

1. Open Azure Storage Explorer and sign in to your Azure account.
1. Locate the storage account and right-click a *Blob Container* or File Share.
1. Select **Get Shared Access Signature**.
1. Configure permissions and expiration settings.
1. Click **Create** and copy the generated SAS URL or token.

Option 3: Use Azure CLI

1. Run the following command in Azure CLI to generate a SAS token:
```sh
    az storage blob generate-sas \
        --account-name <your-storage-account> \
        --container-name <your-container> \
        --name <your-blob> \
        --permissions r \
        --expiry 2026-04-25T12:00:00Z \
        --output tsv
```

This will output a SAS token, which can be appended to the storage URL to provide controlled access.

##### Authorization Code flow (SSO)

When you click **Establish Connection**, you're initiating a secure authentication process known as the Authorization Code Flow. This allows your application to gain access to your Azure Blob Storage without requiring you to manually enter credentials, ensuring a seamless and secure experience.

You will see the following:

1. **Redirect to Sign-In:** You're temporarily directed to your organization’s Identity Provider (IdP), such as Azure Active Directory, where you log in using your existing credentials.
1. **Granting Consent**: After authenticating, you'll see a consent screen explaining the permissions that Tealium’s app is requesting—specifically, access to your Blob Storage.
1. **Secure Access to Blob Storage**: Tealium’s application now has the permission to interact with your storage while maintaining Azure's security policies.

#### Google Cloud Storage settings

##### Sign in with Google

When you click **Sign in with Google**, you initiate a secure authorization process that allows your application to access Google Cloud Storage with your Google account. This process ensures a seamless experience while maintaining security and control over your data.

You will see the following:

1. **Redirect to Google Sign-In**: You are temporarily redirected to Google’s authentication page, where you log in using your Google account credentials.
1. **Granting Consent**: After signing in, you’ll be presented with a consent screen detailing the permissions Tealium’s app is requesting—such as access to your Cloud Storage.
1. **Receiving an Authorization Code**: After you approve, Google generates a one-time authorization code and sends it back to your application.
1. **Secure Access to Cloud Storage**: Tealium’s application now has permission to interact with your storage while adhering to Google’s security policies.

### Databricks to AWS S3 connection

To connect Databricks to an AWS S3 instance, you must first create an IAM role in your AWS instance that can be used to create storage credentials in the Databricks instance. For more information about creating the AWS IAM role, see [Databricks: Create a storage credential for connecting to AWS S3](https://docs.databricks.com/en/connect/unity-catalog/cloud-storage/storage-credentials.html).

After the storage credentials have been created, define the external location in the AWS S3 instance that you will pull data from. For more information, see [Databricks: Create an external location to connect cloud storage to Databricks](https://docs.databricks.com/en/connect/unity-catalog/cloud-storage/external-locations.html).

### Databricks to Azure Blob Storage connection

To connect Databricks to an Azure Blob Storage instance, you need to create a storage credential using Azure service principals or managed identities. This allows Databricks to authenticate and access the Blob Storage securely. For more information, see [Databricks: Create a storage credential for connecting to Azure Blob Storage](https://learn.microsoft.com/en-us/azure/databricks/connect/unity-catalog/cloud-storage/storage-credentials).

Once the storage credentials are configured, define an external location in Azure Blob Storage that Databricks will use for reading and writing data. For more information, see [Databricks: Create an external location to connect cloud storage to Databricks](https://learn.microsoft.com/en-us/azure/databricks/connect/unity-catalog/cloud-storage/external-locations).

### Databricks to Google Cloud Storage connection

To integrate Google Cloud Storage with Databricks, you first need to set up a service account in Google Cloud with the required permissions to access storage buckets. Then, you create a storage credential in Databricks to use this service account for authentication. For more information, see [Databricks: Create a storage credential for connecting to Google Cloud Storage](https://docs.databricks.com/gcp/en/connect/unity-catalog/cloud-storage/storage-credentials).

After setting up the storage credentials, you must define an external location in Google Cloud Storage, specifying the bucket and permissions necessary for Databricks to interact with the data. For more information, see [Databricks: Create an external location to connect cloud storage to Databricks](https://docs.databricks.com/gcp/en/connect/unity-catalog/cloud-storage/external-locations).

## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Maximum number of requests: 100,000
* Maximum time since oldest request: You can set a custom TTL between 1 and 60 minutes. The default value is 10 minutes.
* Maximum size of requests: 10 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Cloud Solution**: Select the cloud solution you are using. Available options are `Databricks Unity Catalog Volume`, `AWS S3`, `Azure Blob Storage`, `Google Cloud Storage`.
* **Databricks Host URL**: Provide the Databricks account URL. For example: `https://{ACCOUNT_NAME}.cloud.databricks.com`.
* **Databricks Token**: Provide the Databricks access token. This parameter is optional if you are sending the data to a Databricks Unity Catalog Volume. To create an access token in Databricks, click the user avatar in Databricks and go to **Settings > Developer > Access Tokens > Manage > Generate New Token**.

Authentication settings vary based on the cloud solution you use:

### Databricks Unity Catalog Volume


<blockquote>
If you expect more than 1000 events per minute, use the batch actions.
</blockquote>


* **Authentication type**: Select the **Databricks OAuth** authentication type.
* **Client ID**: The unique identifier assigned to your service principal secret.
* **Secret**: The string that acts like a password, used by the application to authenticate with Databricks as a service principal.
* **JDBC HTTP path**: The HTTP path to your compute resource. For example, `/sql/1.0/warehouses/3fbc78304284503a`.

### Amazon AWS S3

* **Region**: (Required) Select a region.
* **Authentication Type**: (Required) Select the authentication type for your platform:
    * Provide STS (Security Token Service) credentials.
        * **STS - Assume Role: ARN**: Required for STS authentication. Provide the Amazon Resource Name (ARN) of the role to assume. For example: `arn:aws:iam:222222222222:role/myrole`. For more information, see [AWS Identity and Access Management: Switch to an IAM role (AWS API)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html).
        * **STS - Assume Role: Session Name**: Required for STS authentication. Provide the session name of the role to assume. Minimum length of 2, maximum length of 64.
        * **STS - Assume Role: External ID**: Required for STS authentication. Provide a third-party external identifier. For more information, see [AWS Identity and Access Management: Access to AWS accounts owned by third parties](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_third-party.html).
    * Provide an Access Key and Access Secret.
        * **Access Key - AWS Access Key**: Required for Access Key authentication. Provide the AWS access key.
        * **Access Key - AWS Secret Access Key**: Required for Access Key authentication. Provide the AWS secret access key.

### Google Cloud Storage

1. Click **Sign in with Google** and follow the on-screen instructions.
1. Select the **Project ID**.

### Azure Blob Storage

* **Authentication type**: Select the authentication type. Available options are: Client credentials, Authorization Code flow (SSO), and Shared Access Signature (SAS).
    * Provide client credentials.
        * **Tenant ID**: The unique identifier for your Azure Active Directory instance, representing your organization.
        * **Client ID**: The unique identifier assigned to your application registered in Azure Active Directory.
        * **Client Secret**: The string that acts like a password, used by the application to authenticate with Azure Active Directory.
        * **Storage account name**: The unique name of your Azure Storage account, used to access storage services like Blob, File, Queue, and Table storage.
    * Provide authorization code flow (SSO).
            * **Storage account name**: The unique name of your Azure Storage account. Click **Establish Connection** and follow the on-screen instructions. 
    * Provide shared access signature (SAS).
        * **Shared Access Signature**: The shared access signature for your Azure Storage account.
        * **Storage account name**: The unique name of your Azure Storage account.
* **API version**: The API version compatible with your Azure Storage instance.

## Create a notebook

Notebooks in Databricks are documents that contain executable code, visualizations, and narrative text. They are used for data exploration, visualization, and collaboration. In the connector configuration, you have the option to create a new notebook while you create a new connector by clicking **Create Notebook** in the configuration step.

1. In the connector configuration screen, click **Create Notebook**.
1. Enter the **Table Name**. The schema is specified when creating the job, so do not add it into this field.
    * Names can include alphanumeric characters (`A-Z`, `a-z`, `0-9`) and underscores (`_`).
    * Spaces and special characters, such as `!`, `@`, `#`, `-`, and `.`, are not allowed.
    * Names are case-sensitive. For example, `tableName` and `tablename` would be considered different names.
    * Names cannot start with a digit. For example, `1table` is invalid.
1. For **Notebook Path**, enter the absolute path of the notebook. For example: `/Users/user@example.com/project/NOTEBOOK_NAME`. 
    1. To locate the absolute path of the notebook in Databricks, go to your Databricks workspace and expand the **Users** section. 
    1. Click on the user and then expand the options menu. 
    1. Click on **Copy URL/Path > Full Path**. The path name will be in the following format: `/Workspace/Users/myemail@company.com`. Add the virtual folder and notebook name that you want separated by a slash `/`. For example, `/Workspace/Users/myemail@company.com/virtualfolder/virtualsubfolder/MyNotebook`.
1. **Cloud Bucket / Volume**:
    1. For **Cloud Bucket**, select the Google Cloud Platform (GCP), Azure Blob Storage, or AWS S3 storage bucket to connect as your data destination.
    1. If you are using the **Databricks OAuth** authentication type, specify the Databricks Unity Catalog Volume instead.
1. The **Overwrite** option indicates whether to overwrite an existing notebook in the specified workspace if one already exists.

## Create a job

Jobs in Databricks automate running notebooks on a schedule or based on specific triggers. Jobs allow you to perform tasks, such as data processing, analysis, and reporting, at regular intervals or triggered on certain events. 

1. In the connector configuration screen, click **Create Job**.
1. Enter a name for the processing job.
1. For **Catalog**, specify a catalog from the Unity catalog to use as a destination for publishing pipeline data.
1. For **Target**, specify the schema you want to publish/update your table in the above catalog. Do not specify the target table here, as the table that will be used is the one specified in the notebook.
1. For **Notebook Path**, enter the absolute path of the notebook. For example: `/Users/user@example.com/project/NOTEBOOK_NAME`. 
    1. To locate the absolute path of the notebook in Databricks, go to your Databricks workspace and expand the **Users** section. 
    1. Click on the user and then expand the options menu. 
    1. Click on **Copy URL/Path > Full Path**. The path name will be in the following format: `/Workspace/Users/myemail@company.com`. Add the virtual folder and notebook name that you want separated by a slash `/`. For example, `/Workspace/Users/myemail@company.com/virtualfolder/virtualsubfolder/MyNotebook`.
1. For **Cloud Bucket** or **Volume**, select the cloud storage bucket or Databricks Unity Catalog Volume to connect to Databricks.
1. For **Trigger Type**, select when to process the data. Available options are:
    * **File Arrived**: Process data every time a new file arrives.
    * **Scheduled**: Process data on a repeating schedule that you specify.
    * **Cron**: Process data on a repeating schedule that you define in the **Cron** field.
1. For **Start Time**, specify the start time for job processing in the `hh:mm` format. The default value for the start time is `00:00`.
1. For **Timezone**, specify the timezone in `country/city` format. For example, `Europe/London`. This field is required if you provide a start time.
1. For **Cron**, enter the quartz cron expression you want to use for scheduled processing. For example `20 30 * * * ?` will process files on the twentieth second of the thirtieth minute of every hour, day, day of the week, and year. For more information, see [Quartz: Cron Trigger Tutorial](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html).

## Create a job and notebook

To create a notebook and a job at the same time, click **Create Notebook & Job**. Use the steps in the [Create a notebook](#create-a-notebook) and [Create a job](#create-a-job) sections.

## Actions

The following section lists the supported parameters for each action.

### Send Entire Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Cloud bucket | Select the cloud bucket or container from which Databrick pulls the data. |
| Databricks Catalog | Select the Databricks catalog or provide a custom value. |
| Databricks Schema | Select the Databricks schema or provide a custom value. |
| Databricks Table | Select the Databricks table or provide a custom value. |
| Column to record the payload | Select the `VARIANT` column to record the payload. |
| Column to record the Timestamp | Select the column to record the timestamp. |
| Timestamp Attribute | The default sends the current timestamp for the action. Select an attribute to assign as the timestamp if you want to send a different format. If an attribute is assigned and produces an empty value, we will send the current timestamp. |

### Send Custom Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Cloud bucket | Select the cloud bucket or container from which Databrick pulls the data. |
| Databricks Catalog | Select the Databricks catalog or provide a custom value. |
| Databricks Schema | Select the Databricks schema or provide a custom value. |
| Databricks Table | Select the Databricks table or provide a custom value. |
| Event Parameters | Map event attributes to the columns of the Databricks table. You must map at least one event attribute. |

### Send Entire Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Cloud bucket | Select the cloud bucket or container from which Databrick pulls the data. |
| Databricks Catalog | Select the Databricks catalog or provide a custom value. |
| Databricks Schema | Select the Databricks schema or provide a custom value. |
| Databricks Table | Select the Databricks table or provide a custom value. |
| Column to record the visitor data | Select the `VARIANT` column to record the visitor data. |
| Column to record the Timestamp | Select the column to record the timestamp. |
| Timestamp Attribute | The default sends the current timestamp for the action. Select an attribute to assign as the timestamp if you want to send a different format. If an attribute is assigned and produces an empty value, we will send the current timestamp. |
| Include Current Visit Data with Visitor Data | Select to include the current visit data with visitor data. |

### Send Custom Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Cloud bucket | Select the cloud bucket or container from which Databrick pulls the data. |
| Databricks Catalog | Select the Databricks catalog or provide a custom value. |
| Databricks Schema | Select the Databricks schema or provide a custom value. |
| Databricks Table | Select the Databricks table or provide a custom value. |
| Visitor Parameters | Map visitor attributes to the columns of the Databricks table. You must map at least one visitor attribute. |

### Send Entire Event Data (Batch)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Cloud bucket | Select the cloud bucket or container from which Databricks pulls the data. |
| Databricks Catalog | Select the Databricks catalog or provide a custom value. |
| Databricks Schema | Select the Databricks schema or provide a custom value. |
| Databricks Table | Select the Databricks table or provide a custom value. |
| Column to record the payload | Select the `VARIANT` column to record the payload. |
| Column to record the Timestamp | Select the column to record the timestamp. |
| Timestamp Attribute | The default sends the current timestamp for the action. Select an attribute to assign as the timestamp if you want to send a different format. If an attribute is assigned and produces an empty value, the connector sends the current timestamp. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Custom Event Data (Batch)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Cloud bucket | Select the cloud bucket or container from which Databricks pulls the data. |
| Databricks Catalog | Select the Databricks catalog or provide a custom value. |
| Databricks Schema | Select the Databricks schema or provide a custom value. |
| Databricks Table | Select the Databricks table or provide a custom value. |
| Event Parameters | Map the parameters to the columns of the table. You must map at least one parameter. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Entire Visitor Data (Batch)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Cloud bucket | Select the cloud bucket or container from which Databricks pulls the data. |
| Databricks Catalog | Select the Databricks catalog or provide a custom value. |
| Databricks Schema | Select the Databricks schema or provide a custom value. |
| Databricks Table | Select the Databricks table or provide a custom value. |
| Column to record the visitor data | Select the `VARIANT` column to record the visitor data. |
| Column to record the Timestamp | Select the column to record the timestamp. |
| Timestamp Attribute | The default sends the current timestamp for the action. Select an attribute to assign as the timestamp if you want to send a different format. If an attribute is assigned and produces an empty value, we will send the current timestamp. |
| Include Current Visit Data with Visitor Data | Select to include the current visit data with visitor data. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Custom Visitor Data (Batch)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Cloud bucket | Select the cloud bucket or container from which Databricks pulls the data. |
| Databricks Catalog | Select the Databricks catalog or provide a custom value. |
| Databricks Schema | Select the Databricks schema or provide a custom value. |
| Databricks Table | Select the Databricks table or provide a custom value. |
| Visitor Parameters | Map the parameters to the columns of the table. You must map at least one parameter. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Cloud bucket | Select the cloud bucket or container from which Databricks pulls the data. |
| Databricks Catalog | Select the Databricks catalog or provide a custom value. |
| Databricks Schema | Select the Databricks schema or provide a custom value. |
| Databricks Table | Select the Databricks table or provide a custom value. |
| Event Parameters | Map the parameters to the columns of the table. You must map at least one parameter. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Entire Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Cloud bucket | Choose the cloud bucket/container from which Databricks pulls the data. |
| Databricks Catalog | Select the Databricks catalog or provide a custom value. |
| Databricks Schema | Select the Databricks schema or provide a custom value. |
| Volume | Volume where the files will be exported. |
| Files path | Path where the files will be exported. Do not change this value if you want the files to be dropped in the root of the volume. |
| Databricks Table | Select the Databricks table or provide a custom value. |
| Column to record the payload | Select the `VARIANT` column to record the payload. |
| Column to record the Timestamp | Select the column to record the timestamp. |
| Timestamp Attribute | The default sends the current timestamp for the action. Select an attribute to assign as the timestamp if you want to send a different format. If an attribute is assigned and produces an empty value, we  send the current timestamp. |