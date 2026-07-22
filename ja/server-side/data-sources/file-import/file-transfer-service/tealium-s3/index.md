---
title: Tealium S3バケット
description: この記事では、Tealium S3バケットを使用してファイルをアップロードし、管理する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/file-import/file-transfer-service/tealium-s3/
---

<blockquote>
S3バケットに大量のファイルを保存すると、読み取り時間が遅くなる可能性があります。効率的な読み取り時間を維持するために、定期的に処理済みのファイルをS3バケットから削除することをお勧めします。
</blockquote>
 

## 資格情報

ファイルサービスの構成で**Tealium S3バケット**を選択すると、Tealium S3バケットの資格情報が自動的に生成され、以下の内容が含まれます：

* アクセスキー
* シークレットキー
* バケット/プレフィックス

サービスの構成を完了した後、**データソースダッシュボード**でデータソースを展開し、**サービス構成**タブをクリックすることで、Tealium S3の資格情報を見つけることができます。


<blockquote>
これらの資格情報すべてが必要となりますので、Cyberduckを使用してバケットに接続します。Cyberduckを使用してFTP/SFTPまたはAmazon S3経由でファイルをアップロードする方法については、[Use Cyberduck to upload a file via FTP/SFTP or Amazon S3](https://docs.tealium.com/cyberduck/)を参照してください。
</blockquote>

