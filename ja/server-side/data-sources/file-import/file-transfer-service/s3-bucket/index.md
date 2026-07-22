---
title: 空のS3バケットにファイルをアップロードするためのAmazon CLIの使用
description: この記事では、空のS3バケットにファイルをアップロードする方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/file-import/file-transfer-service/s3-bucket/
---
S3バケットが最初に作成されると、それは空です。空のS3バケットにアクセスしようとすると、次のメッセージが表示されることがあります：

`ACCOUNT-PROFILEの属性の読み取りに失敗しました`

CSVファイルをアップロードする前に、次の`aws s3api`コマンドを使用して空のバケットにファイルをアップロードします：

```bash
aws s3api put-object --bucket <bucket> --key <key> --body <body>
```

* `bucket`の値は、`collect-REGION.tealium.com`の形式でリージョンドメインを指定します。
* `key`の値は、ファイルに割り当てるファイル名を指定します。これにはファイルプレフィックスも含まれます。
* `body`の値は、ローカルシステム上のファイルの場所を指定します。

例えば：

```bash
aws s3api put-object --bucket collect-us-east-1.tealium.com \
  --key bulk-downloader/ACCOUNT-PROFILE/test_fileimp_01.csv \
  --body ./test_fileimp_01.csv
```

詳細については、[AWS Command Line Interface (CLI): How to Connect to Your S3 Bucket and Other Common Commands](https://support.tealiumiq.com/en/support/solutions/articles/36000363516-aws-command-line-interface-cli-how-to-connect-to-your-s3-bucket-and-other-common-commands)を参照してください。
