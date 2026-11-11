---
title: AWS Firehose（Tealium 提供の認証情報）コネクタ構成ガイド
description: この記事では、AWS Firehose（Tealium 提供の認証情報）コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/aws-firehose-tealium-provided-credentials-connector/
---
## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **リージョン**：（必須）リージョンを選択します。
* **引き受けるロール：ARN**：（必須）引き受けるロールの Amazon リソースネーム（ARN）を指定します。例：`arn:aws:iam::222222222222:role/myrole`
    * 信頼ポリシーで、External ID 条件を使用して Tealium ルートアカウント（`arn:aws:iam::757913464184:root`）が許可されていることを確認します。
    * IAM ロール名のプレフィックスに `TealiumFirehose` を含めることをお勧めします。
    * 詳細については、[AWS：IAM ロールへの切り替え](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)を参照してください。
* **引き受けるロール：セッション名**：引き受けるロールのセッション名を指定します。
* **引き受けるロール：External ID**：（任意）外部識別子を指定します。
    * 詳細については、[AWS：第三者が所有する AWS アカウントへのアクセス](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)を参照してください。

### AWS アカウントへの Tealium ロールの追加

Tealium のメイン AWS アカウント ID `757913464184` をプリンシパルとして使用し、External ID 条件を必須にします。以下は、AWS アカウント内の IAM ロールの **信頼関係** タブに追加する信頼ポリシーの例です。`EXTERNAL_ID` を、**引き受けるロール：External ID** で構成した正確な値に置き換えます。

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::757913464184:root"
      },
      "Action": "sts:AssumeRole",
      "Condition": {
        "StringEquals": {
          "sts:ExternalId": "EXTERNAL_ID"
        }
      }
    }
  ]
}
```

#### プライベートクラウドの信頼ポリシー

プライベートクラウドのお客様の場合、Tealium は別の AWS アカウント ID `111879511226` を使用します。以下は、AWS アカウント内の IAM ロールの **信頼関係** タブに追加する信頼ポリシーの例です。`EXTERNAL_ID` を、**引き受けるロール：External ID** で構成した正確な値に置き換えます。

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::111879511226:root"
      },
      "Action": "sts:AssumeRole",
      "Condition": {
        "StringEquals": {
          "sts:ExternalId": "EXTERNAL_ID"
        }
      }
    }
  ]
}
```

### IAM アクセス許可ポリシー

以下は、前述の信頼ポリシーで使用できる、単一ストリーム向けの最小権限アクセス許可ポリシーです。

`Resource` フィールドで、次のプレースホルダーを置き換えます。

* `REGION`：AWS リージョン（例：`us-west-2`）。
* `ACCOUNT_ID`：AWS アカウント ID。
* `MY_FIREHOSE_STREAM`：Tealium に書き込みを許可する Firehose 配信ストリームの名前。

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowListingDeliveryStreams",
      "Effect": "Allow",
      "Action": [
        "firehose:ListDeliveryStreams",
        "firehose:DescribeDeliveryStream"
      ],
      "Resource": "*"
    },
    {
      "Sid": "AllowWritingToSpecificDeliveryStream",
      "Effect": "Allow",
      "Action": [
        "firehose:PutRecord",
        "firehose:PutRecordBatch"
      ],
      "Resource": "arn:aws:firehose:REGION:ACCOUNT_ID:deliverystream/MY_FIREHOSE_STREAM"
    }
  ]
}
```

このポリシーを、External ID を使用して Tealium アカウントを信頼するように信頼ポリシーが構成されている同じ IAM ロールにアタッチします（プライベートクラウドの場合：`arn:aws:iam::111879511226:root`、その他すべての場合：`arn:aws:iam::757913464184:root`）。

Tealium から複数の配信ストリームに送信する必要がある場合は、次のいずれかを実行します。

* `AllowWritingToSpecificDeliveryStream` の `Resource` に、追加の ARN を配列として追加します。
* 命名規則に合う場合は、パターンベースの ARN（例：`tealium-` というプレフィックスが付いたすべての Tealium ストリーム）を使用します。

コネクタを構成したら、**完了**をクリックします。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| イベントデータを配信ストリームに送信 | ✗ | ✓ |
| カスタマイズしたデータを配信ストリームに送信（詳細） | ✓ | ✓ |
| ログイベントを配信ストリームに送信 | ✗ | ✓ |
| 訪問データを配信ストリームに送信 | ✓ | ✗ |
| カスタマイズしたデータを配信ストリームに送信（バッチ） | ✓ | ✓ |
| イベントデータを配信ストリームに送信（バッチ） | ✗ | ✓ |

アクションの名前を入力し、アクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### イベントデータを配信ストリームに送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 配信ストリーム | <ul><li>データの送信先となる配信ストリームを選択します。</li><li>利用可能なストリームを表示するには、`firehose:ListDeliveryStreams` アクセス許可を付与する必要があります。</li><li>詳細については、[AWS：Amazon Data Firehose のクォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。</ul></li> |
| レコードサフィックス | <ul><li>区切り文字として使用するために、各レコードの末尾に追加されるサフィックスです。</li><li>デフォルトは `Newline` です。</ul></li> |
| 属性名を出力 | 属性名が更新された場合、ペイロード内の名前に更新内容が反映されます。 |

### カスタマイズしたデータを配信ストリームに送信（詳細）

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 配信ストリーム | <ul><li>データの送信先となる配信ストリームを選択します。</li><li>利用可能なストリームを表示するには、`firehose:ListDeliveryStreams` アクセス許可を付与する必要があります。</li><li>詳細については、[AWS：Amazon Data Firehose のクォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。</ul></li> |

#### メッセージデータ

| **パラメータ** | **説明** |
| --- | --- |
| レコードサフィックス | <ul><li>区切り文字として各レコードの末尾に追加するサフィックスです。</li><li>デフォルトは `Newline` です。</ul></li> |
| メッセージテンプレート変数 | <ul><li>（任意）テンプレートへのデータ入力としてテンプレート変数を指定します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数にはドット表記で名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。</ul></li> |
| メッセージテンプレート | <ul><li>（任意）`URL`、`URL` パラメータ、ヘッダー、または本文データで参照するテンプレートを指定します。</li><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、サポートされているフィールドに二重波括弧で名前を指定して挿入します。</li><li>例：`{{SomeTemplateName}}`</ul></li> |

### ログイベントを配信ストリームに送信

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| 配信ストリーム | <ul><li>データの送信先となる配信ストリームを選択します。</li><li>利用可能なストリームを表示するには、`firehose:ListDeliveryStreams` アクセス許可を付与する必要があります。</li><li>詳細については、[AWS：Amazon Data Firehose のクォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。</ul></li> |
| レコードサフィックス | <ul><li>区切り文字として使用するために、各レコードの末尾に追加されるサフィックスです。</li><li>デフォルトは `Newline` です。</ul></li> |

### 訪問データを配信ストリームに送信
#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| 配信ストリーム | <ul><li>データの送信先となる配信ストリームを選択します。</li><li>利用可能なストリームを表示するには、`firehose:ListDeliveryStreams` 権限が付与されている必要があります。</li><li>詳細については、[AWS: Amazon Data Firehose のクォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。</ul></li> |
| レコードサフィックス | <ul><li>区切り文字として各レコードの末尾に追加するサフィックスです。</li><li>デフォルトは `Newline` です。</ul></li> |
| 現在の訪問データを含める | 現在の訪問データをペイロードに追加します。「現在の訪問のイベントデータを除外」が選択されていない場合は、イベントの訪問データも含まれます。 |
| 現在の訪問のイベントデータを除外 | 現在の訪問データからイベントデータを除外します。 |
| 属性名を出力 | 属性名が更新された場合、ペイロード内の名前に更新内容が反映されます。 |

### カスタマイズしたデータを配信ストリームに送信（バッチ処理）

#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| 配信ストリーム | <ul><li>データの送信先となる配信ストリームを選択します。</li><li>利用可能なストリームを表示するには、`firehose:ListDeliveryStreams` 権限が付与されている必要があります。</li><li>詳細については、[AWS: Amazon Data Firehose のクォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。</ul></li> |

#### メッセージデータ

| **パラメーター** | **説明** |
| --- | --- |
| レコードサフィックス | <ul><li>区切り文字として各レコードの末尾に追加するサフィックスです。</li><li>デフォルトは `Newline` です。</ul></li> |
| メッセージテンプレート変数 | <ul><li>（任意）テンプレートのデータ入力としてテンプレート変数を指定します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数には、ドット表記を使用して名前を付けます。例：`items.name`。</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。</ul></li> |
| メッセージテンプレート | <ul><li>（任意）`URL`、`URL` パラメーター、ヘッダー、または本文データで参照するテンプレートを指定します。</li><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、サポートされているフィールドに二重波括弧で囲んだ名前を使用して挿入します。</li><li>例：`{{SomeTemplateName}}`。</ul></li> |

### イベントデータを配信ストリームに送信（バッチ処理）

#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| 配信ストリーム | <ul><li>データの送信先となる配信ストリームを選択します。</li><li>利用可能なストリームを表示するには、`firehose:ListDeliveryStreams` 権限が付与されている必要があります。</li><li>詳細については、[AWS: Amazon Data Firehose のクォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。</ul></li> |
| レコードサフィックス | <ul><li>区切り文字として各レコードの末尾に追加するサフィックスです。</li><li>デフォルトは `Newline` です。</ul></li> |
| 属性名を出力 | 属性名が更新された場合、ペイロード内の名前に更新内容が反映されます。 |