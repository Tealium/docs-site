---
title: Azure storage
description: This article describes how to use the Azure Blob and Azure File Storage to upload and manage files.
url: https://docs.tealium.com/server-side/data-sources/file-import/file-transfer-service/azure/
---
## Azure Blob credentials

You will need the following Azure Blob credentials to configure the file service in the File Import configuration:

* Account name  
The name of your storage account. For example, in the URI `https://myaccount.blob.core.windows.net`, the account name is `myaccount`.
* SAS token  
Your Shared Access Signature (SAS) token. For more information, see [Microsoft Ignite: Create a Service SAS](https://learn.microsoft.com/en-us/rest/api/storageservices/create-service-sas).
* Container name
The name of the container. For example, in the URI `https://myaccount.blob.core.windows.net/mycontainer`, the container name is `mycontainer`.

Additionally, you can add a subdirectory. For example, in the URI `https://myaccount.blob.core.windows.net/mycontainer/mydir`, the subdirectory is `mydir`. The default is the root directory.

## Azure File Storage credentials

You will need the following Azure File Storage credentials to configure the file service in the File Import configuration:

* Account name  
The name of your storage account. For example, in the URI `https://myaccount.file.core.windows.net`, the account name is `myaccount`.
* SAS token  
Your Shared Access Signature (SAS) token. For more information, see [Microsoft Ignite: Create a Service SAS](https://learn.microsoft.com/en-us/rest/api/storageservices/create-service-sas).
* Fileshare name
The name of the share. For example, in the URI `https://myaccount.file.core.windows.net/myshare`, the fileshare name is `myshare`.

Additionally, you can add a subdirectory. For example, in the URI `https://myaccount.file.core.windows.net/myshare/mydir`, the subdirectory is `mydir`. The default is the root directory.

