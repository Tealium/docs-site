---
title: サービスへのファイルのアップロード
description: この記事では、ファイルサービスへのファイルのアップロードを開始する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/file-import/file-transfer-service/upload-files/
---
Tealium は、ファイルをインポートするために以下のファイル転送サービスをサポートしています。

* Amazon S3
  * [AWS S3 バケット](https://docs.tealium.com/aws-s3/)
  * [Tealium S3 バケット](https://docs.tealium.com/tealium-s3/)
* [Microsoft Azure File/Blob Storage](https://docs.tealium.com/azure/)
* [SFTP](https://docs.tealium.com/sftp/)

## Cyberduck と Amazon CLI を使用したファイルのアップロードと管理

データソースを構成した後、サードパーティ製アプリを使用して CSV ファイルをファイルサービスにアップロードします。この目的には任意のクライアントを使用できますが、無料で SFTP と Amazon S3 をサポートしている Cyberduck を推奨します。

ファイルのアップロードと管理を開始するには、以下の記事を参照してください。

* [Cyberduck を使用して SFTP または Amazon S3 にファイルをアップロードする](https://docs.tealium.com/cyberduck/)
* [Amazon Command Line Interface を使用してファイルをアップロードおよび管理する](https://docs.tealium.com/aws-cli/)


## 使用状況レポート

ファイルインポート用データソースを構成した後、使用状況レポートを使用して、Customer Data Platform（CDP）にインポートされたファイルインポートの行数を確認します。詳細については、[使用状況レポートについて](https://docs.tealium.com/understanding-the-usage-report/)を参照してください。

## ファイルアップロードエラー

ファイル処理に失敗した場合、そのファイルは無視されます。システムは、そのファイルを再度処理しようとはしません。一般的な失敗の原因は以下のとおりです。

* CSV ファイルの形式が不適切であるため、有効な CSV ファイルではない。
* CSV ファイルが BOM なしの UTF-8 形式ではない。
* ファイル定義で使用されている列名がファイル内に存在しない。
* File Service の構成で同じ列名が複数回使用されている。


<blockquote>
CDP がファイル転送サービスを使用したファイルのコピーに失敗した場合、10 分後に再試行します。
</blockquote>
