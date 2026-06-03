---
title: Azure保存
description: この記事では、Azure BlobとAzure File Storageを使用してファイルをアップロードし、管理する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/file-import/file-transfer-service/azure/
---
## Azure Blobの認証情報

ファイルインポート構成でファイルサービスを構成するためには、以下のAzure Blobの認証情報が必要です：

* アカウント名  
保存アカウントの名前。例えば、URI `https://myaccount.blob.core.windows.net`では、アカウント名は`myaccount`です。
* SASトークン  
共有アクセス署名（SAS）トークン。詳細については、[Microsoft Ignite: Create a Service SAS](https://learn.microsoft.com/en-us/rest/api/storageservices/create-service-sas)を参照してください。
* コンテナ名
コンテナの名前。例えば、URI `https://myaccount.blob.core.windows.net/mycontainer`では、コンテナ名は`mycontainer`です。

さらに、サブディレクトリを追加することもできます。例えば、URI `https://myaccount.blob.core.windows.net/mycontainer/mydir`では、サブディレクトリは`mydir`です。デフォルトはルートディレクトリです。

## Azure File Storageの認証情報

ファイルインポート構成でファイルサービスを構成するためには、以下のAzure File Storageの認証情報が必要です：

* アカウント名  
保存アカウントの名前。例えば、URI `https://myaccount.file.core.windows.net`では、アカウント名は`myaccount`です。
* SASトークン  
共有アクセス署名（SAS）トークン。詳細については、[Microsoft Ignite: Create a Service SAS](https://learn.microsoft.com/en-us/rest/api/storageservices/create-service-sas)を参照してください。
* ファイル共有名
共有の名前。例えば、URI `https://myaccount.file.core.windows.net/myshare`では、ファイル共有名は`myshare`です。

さらに、サブディレクトリを追加することもできます。例えば、URI `https://myaccount.file.core.windows.net/myshare/mydir`では、サブディレクトリは`mydir`です。デフォルトはルートディレクトリです。