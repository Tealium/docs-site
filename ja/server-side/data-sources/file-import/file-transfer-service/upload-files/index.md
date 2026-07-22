---
title: サービスにファイルをアップロードする
description: この記事では、ファイルサービスにファイルをアップロードする方法を説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/file-import/file-transfer-service/upload-files/
---
Tealiumは、ファイルのインポートに以下のファイル転送サービスをサポートしています：

* Amazon S3
  * [AWS S3バケット](https://docs.tealium.com/aws-s3/)
  * [Tealium S3バケット](https://docs.tealium.com/tealium-s3/)
* [Microsoft Azure File/Blob Storage](https://docs.tealium.com/azure/)
* [SFTP](https://docs.tealium.com/sftp/)

## CyberduckとAmazon CLIを使用してファイルをアップロードし、管理する

データソースを構成した後、サードパーティのアプリを使用してCSVファイルをファイルサービスにアップロードします。この目的のために任意のクライアントを使用することができますが、CyberduckはSFTPとAmazon S3をサポートしており、無料のため、おすすめです。

ファイルのアップロードと管理を開始するための以下の記事をご覧ください：

* [Cyberduckを使用してSFTPまたはAmazon S3経由でファイルをアップロードする](https://docs.tealium.com/cyberduck/)
* [Amazon Command Line Interfaceを使用してファイルをアップロードし、管理する](https://docs.tealium.com/aws-cli/)


## 使用レポート

ファイルインポートデータソースを構成した後、使用レポートを使用して、AudienceStreamにインポートされたファイルインポート行または行の数を確認します。詳細については、[使用レポートの理解](https://docs.tealium.com/understanding-the-usage-report/)を参照してください。

## ファイルアップロードエラー

ファイル処理の失敗が発生すると、そのファイルは無視されます。システムは再度ファイルを処理しようとはしません。失敗の最も一般的な理由は以下の通りです：

* CSVファイルが不適切にフォーマットされており、有効なCSVファイルではありません。
* CSVファイルは、BOMエンコーディングなしのUTF-8形式でなければなりません。
* ファイル定義で使用されている列名がファイルに存在しません。
* 列名がファイルサービスの構成で複数回使用されています。


<blockquote>
AudienceStreamがファイル転送サービスを使用してファイルのコピーに失敗した場合、10分後に再試行します。
</blockquote>

