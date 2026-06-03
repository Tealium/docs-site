---
title: Upload files to a service
description: This article describes how to get started uploading files to your file service.
url: https://docs.tealium.com/server-side/data-sources/file-import/file-transfer-service/upload-files/
---
Tealium supports the following file transfer services for file import:

* Amazon S3
  * [AWS S3 bucket]()
  * [Tealium S3 bucket]()
* [Microsoft Azure File/Blob Storage]()
* [FTP/SFTP]()

## Upload and manage files using Cyberduck and Amazon CLI

After you set up your data source, upload your CSV files to your file service using a third-party app. Though you may use any client for this purpose, we recommend Cyberduck because it&#39;s free and supports FTP/SFTP and Amazon S3.

Use the following articles to get started uploading and managing your files:

* [Upload a file with FTP/SFTP or Amazon S3 with Cyberduck]()
* [Upload and manage files using the Amazon Command Line Interface]()


## Usage reports

After you set up a file import data source, use usage reports to review the number of file import rows or lines imported into AudienceStream. For more information, see [Understanding the usage report]().

## File upload errors

When a file process failure occurs, the file is ignored. The system does not attempt to process the file again. The most common reasons for failure are:

* The CSV file is improperly formatted and is therefore not a valid CSV file.
* The CSV file must be in UTF-8 format with no BOM encoding.
* Column names used in the file definition do not exist in the file.
* A column name is used more than once in the File Service configuration.

If AudienceStream fails to copy a file using the file transfer service, it will retry in 10 minutes.