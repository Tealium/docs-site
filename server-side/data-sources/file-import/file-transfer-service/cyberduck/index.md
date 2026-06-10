---
title: Use Cyberduck to upload a file with SFTP or Amazon S3
description: This article describes how to configure Cyberduck to upload a file with SFTP or Amazon S3.
url: https://docs.tealium.com/server-side/data-sources/file-import/file-transfer-service/cyberduck/
---
1. Run Cyberduck.
1. Create a new connection and enter a name for the connection.
1. Select the file transfer service used in your File Service configuration.
1. Enter the credentials (username and password) for your service.  
    * **Tealium S3 Bucket** - The Tealium S3 bucket credentials are generated automatically when you configure your file service in the file import data source.
        * You can find the Tealium S3 credentials in the **Data Sources Dashboard** by expanding the data source and clicking the **Service Configuration** tab.  
        ![](/images/server-side/data-sources/tealium-s3-bucket-credentials.png)
        * In Cyberduck, enter the following:
            * **Server**: `s3.amazonaws.com`
            * **Access Key ID**: Tealium S3 **Access key**
            * **Secret Access Key**: Tealium S3 **Secret key**
            * **Path**: Tealium S3 **Bucket/Prefix**. For example,  
            `collect-us-east-1.tealium.com/bulk-downloader/{{ACCOUNT-PROFILE}}`
1. Provide other details, such as the server, path, port, etc., required by your service. To learn more about accessing third-party S3 buckets using Cyberduck, see [Cyberduck: Amazon S3](https://docs.cyberduck.io/protocols/s3/#Accessthirdpartybuckets).
1. Save the connection.

Upload files by dragging and dropping your CSV files into Cyberduck. If this is a new S3 bucket (an empty bucket), see [Uploading a File to an Empty S3 Bucket]() for instructions on uploading your first file.

When using SFTP, the file must be located in the root folder. Files cannot be located in the sub-folders for an SFTP connection.