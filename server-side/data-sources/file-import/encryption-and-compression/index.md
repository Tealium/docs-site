---
title: Encryption and compression in File Import data sources
description: This article describes how compression and encryption options work for a file import data source.
url: https://docs.tealium.com/server-side/data-sources/file-import/encryption-and-compression/
---
## How it works

### PGP encryption

PGP (Pretty Good Privacy) encryption is a trusted standard for encryption. Whether you are configuring your file service in Tealium for the first time or uploading an encrypted document to an existing file service configuration, you can use PGP encryption to protect all encrypted documents within one file service.

When you configure a data source, you generate public keys for that configuration, so you can have only one PGP key per data source.

PGP encryption uses private- and public-key encryption and lets you upload encrypted files securely to Tealium without having to exchange private keys. In your file import data source configuration, you can generate a public PGP encryption key that lets you encrypt your files using any encryption tool that supports PGP encryption. After you encrypt the file and upload it to your file service, Tealium will use its own private key to decrypt the file for processing. Without a matching public key, uploaded files cannot be decrypted by Tealium, ensuring security for bulk data uploads. 

#### Expiration time

Public keys expire after 2 years. After your key expires, you will need to generate a new public key to upload encrypted files. 

### GZIP compression

GZIP is the compression file format currently supported by Tealium. While we recommend splitting files into 100,000 rows per file, you may have files that have many columns, which expands the size of the file. Using GZIP compression can help decrease file sizes, resulting in more efficient uploads.



### Using both compression and encryption

If you are uploading files that are both compressed and encrypted, the files must be compressed first, then encrypted. If files are encrypted and then compressed, the file processing will fail.

For more details on compression and encryption processing errors, use the custom [Bulk Download Logs](https://support.tealiumiq.com/en/support/solutions/articles/36000363442-tealium-tools-bulk-download-logs) tool. 


## Encrypt files using PGP encryption

To encrypt files using PGP encryption, complete the following steps:

1. Navigate to **File Import &gt; Add a Data Source &gt; File Import**. 
1. Complete the steps in the wizard. In the **Service Configuration** step, select an existing file service configuration or create a new one.
1. Enter a prefix for **File Name Prefix**.
1. In **File Compression and Encryption**, select **PGP** from the **Encryption** drop down list. 
1. Under **PGP Key Generator**, click **Generate**. The generator will create the public key that will be shared between your encryption tool and Tealium.
1. Download the public key.
1. Import the public key to the encryption tool you are using to encrypt your files.
1. Encrypt the files.
1. Upload the encrypted files to the file service you are using in your File Import data source configuration.
1. Complete the File Import data source configuration.
1. Save/Publish your profile.

 If you need to update an encrypted file that has already been uploaded, update your file and encrypt the file again before you upload it to your file service. If the file is not encrypted, file processing will fail. 

## Compress files using GZIP compression

The following instructions are for Mac OS or Linux users. For Windows users, use a third-party compression tool that supports GZIP compression.

1. Open a Terminal window and navigate to the directory where your files are located on your computer.
1. Enter the following command to compress the file. If the file name contains spaces, put the file name in double quotes. Use the `-k` flag to indicate to the compression application that you want to keep the original file.   
    * **File name without space**  
    `gzip -k demo_100_airline_records.csv`  
    * **File name with spaces**  
    `gzip -k &#34;demo_100 airline records.csv&#34;`
1. Your compression application will create files with the file type `.gz` in your working directory. 
1. Upload your compressed files to the file service you are using in your File Import data source.
1. In Tealium, navigate to **File Import &gt; Add a Data Source &gt; File Import**. 
1. Complete the steps in the wizard. In the **Service Configuration** step, select an existing file service configuration or create a new one.
1. Enter a prefix for **File Name Prefix**.
1. In **File Compression and Encryption**, select **GZIP** for the **Compression** drop down list.
1. Complete the File Import data source configuration.
1. Save/Publish your profile.

 All files that were originally compressed during the File Import data source configuration will need to be compressed again when data is updated and a new version is uploaded to the file service. If the file is not compressed, file processing will fail. 