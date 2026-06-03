---
title: Amazonコマンドラインインターフェースを使用してファイルをアップロードおよび管理する
description: この記事では、AWSコマンドラインインターフェースを使用してファイルをアップロードおよび管理する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/file-import/file-transfer-service/aws-cli/
---
AWSコマンドラインインターフェース（CLI）をインストールするには、Amazonのドキュメンテーションの[Installing, updating, and uninstalling the AWS CLI](http://docs.aws.amazon.com/cli/latest/userguide/installing.html)を参照してください。AWS CLIの構成については、[Configuration Basics](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)を参照してください。

`aws configure`コマンドを呼び出すと、アクセスキーとアクセスキーIDが求められます。リージョン名と出力形式は空白のままにしておくことができます。

CLIを構成した後は、次のCLIの例に示すように、`s3api`メソッドを使用してクエリを作成します：

## ルートフォルダ内のすべてのオブジェクトをリストする

```bash
aws s3 ls s3://collect-{REGION}.tealium.com/bulk-downloader/{ACCOUNT-PROFILE}/
```

## ファイルをフォルダにコピーする

```bash
aws s3 cp local_file.csv s3://collect-{REGION}.tealium.com/bulk-downloader/{ACCOUNT-PROFILE}/
```

## フォルダからファイルを削除する

```bash
aws s3 rm s3://collect-{REGION}.tealium.com/bulk-downloader/{ACCOUNT-PROFILE}/local_file.csv
```
