---
title: AWS Firehose（Tealium提供の資格情報）コネクタ構成ガイド
description: この記事では、AWS Firehose（Tealium提供の資格情報）コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/aws-firehose-tealium-provided-credentials-connector/
---
## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタの追加方法については、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の構成を行います：

* **リージョン**：（必須）リージョンを選択します。
* **Assume Role: ARN**：（必須）引き受けるロールのAmazonリソースネーム（ARN）を提供します。例：`arn:aws:iam::222222222222:role/myrole`。
    * 信頼ポリシーがTealiumのルートアカウント（`arn:aws:iam::757913464184:root`）を外部ID条件付きで許可していることを確認してください。
    * IAMロール名に`TealiumFirehose`をプレフィックスとして含めることを推奨します。
    * 詳細については、[AWS: IAMロールへの切り替え](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)を参照してください。
* **Assume Role: セッション名**：引き受けるロールのセッション名を提供します。
* **Assume Role: 外部ID**：（オプション）外部識別子を提供します。
    * 詳細については、[AWS: 第三者が所有するAWSアカウントへのアクセス](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)を参照してください。

### AWSアカウントにTealiumロールを追加

TealiumのメインAWSアカウントID `757913464184` をプリンシパルとして使用し、外部ID条件を要求します。以下は、AWSアカウントのIAMロールの**信頼**関係タブに追加する信頼ポリシーの例です。**Assume Role: 外部ID**で構成する値と`EXTERNAL_ID`を正確に置き換えてください。

```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Principal&#34;: {
        &#34;AWS&#34;: &#34;arn:aws:iam::757913464184:root&#34;
      },
      &#34;Action&#34;: &#34;sts:AssumeRole&#34;,
      &#34;Condition&#34;: {
        &#34;StringEquals&#34;: {
          &#34;sts:ExternalId&#34;: &#34;EXTERNAL_ID&#34;
        }
      }
    }
  ]
}
```

#### プライベートクラウドの信頼ポリシー

プライベートクラウドのお客様の場合、Tealiumは異なるAWSアカウントID `111879511226` を使用します。以下は、AWSアカウントのIAMロールの**信頼**関係タブに追加する信頼ポリシーの例です。**Assume Role: 外部ID**で構成する値と`EXTERNAL_ID`を正確に置き換えてください。

```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Principal&#34;: {
        &#34;AWS&#34;: &#34;arn:aws:iam::111879511226:root&#34;
      },
      &#34;Action&#34;: &#34;sts:AssumeRole&#34;,
      &#34;Condition&#34;: {
        &#34;StringEquals&#34;: {
          &#34;sts:ExternalId&#34;: &#34;EXTERNAL_ID&#34;
        }
      }
    }
  ]
}
```

### IAM権限ポリシー

以下は、前述の信頼ポリシーと連携する最小権限の単一ストリーム権限ポリシーです。

`Resource`フィールドでは、次のプレースホルダーを置き換えます：

* `REGION`：あなたのAWSリージョン（例：`us-west-2`）。
* `ACCOUNT_ID`：あなたのAWSアカウントID。
* `MY_FIREHOSE_STREAM`：Tealiumが書き込むFirehose配信ストリーム名。

```json
{
  &#34;Version&#34;: &#34;2012-10-17&#34;,
  &#34;Statement&#34;: [
    {
      &#34;Sid&#34;: &#34;AllowListingDeliveryStreams&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;firehose:ListDeliveryStreams&#34;,
        &#34;firehose:DescribeDeliveryStream&#34;
      ],
      &#34;Resource&#34;: &#34;*&#34;
    },
    {
      &#34;Sid&#34;: &#34;AllowWritingToSpecificDeliveryStream&#34;,
      &#34;Effect&#34;: &#34;Allow&#34;,
      &#34;Action&#34;: [
        &#34;firehose:PutRecord&#34;,
        &#34;firehose:PutRecordBatch&#34;
      ],
      &#34;Resource&#34;: &#34;arn:aws:firehose:REGION:ACCOUNT_ID:deliverystream/MY_FIREHOSE_STREAM&#34;
    }
  ]
}
```

このポリシーを、外部IDでTealiumアカウントを信頼する構成のIAMロールに添付します（プライベートクラウドの場合：`arn:aws:iam::111879511226:root`、その他の場合は`arn:aws:iam::757913464184:root`）。

Tealiumが複数の配信ストリームに送信する必要がある場合は、次のいずれかを行います：

* `AllowWritingToSpecificDeliveryStream`の`Resource`に追加のARNを配列として追加します。
* 命名規則に合わせてパターンベースのARNを使用します（例：すべてのTealiumストリームに`tealium-`をプレフィックスとして付ける場合）。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| 配信ストリームへのイベントデータ送信 | ✗ | ✓ |
| 配信ストリームへのカスタマイズデータ送信（高度） | ✓ | ✓ |
| 配信ストリームへのログイベント送信 | ✗ | ✓ |
| 配信ストリームへの訪問データ送信 | ✓ | ✗ |
| 配信ストリームへのカスタマイズデータ送信（バッチ処理） | ✓ | ✓ |
| 配信ストリームへのイベントデータ送信（バッチ処理） | ✗ | ✓ |

アクションの名前を入力し、アクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### 配信ストリームへのイベントデータ送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 配信ストリーム | &lt;ul&gt;&lt;li&gt;データを送信する配信ストリームを選択します。&lt;/li&gt;&lt;li&gt;利用可能なストリームを確認するには、`firehose:ListDeliveryStreams`の権限が必要です。&lt;/li&gt;&lt;li&gt;詳細については、[AWS: Amazon Data Firehoseの制限](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。&lt;/ul&gt;&lt;/li&gt; |
| レコードの接尾辞 | &lt;ul&gt;&lt;li&gt;各レコードの末尾に追加される接尾辞で、区切り文字として使用されます。&lt;/li&gt;&lt;li&gt;デフォルトは`Newline`です。&lt;/ul&gt;&lt;/li&gt; |
| 属性名の印刷 | 属性名が更新された場合、ペイロード内の名前が更新を反映します。 |

### 配信ストリームへのカスタマイズデータ送信（高度）

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 配信ストリーム | &lt;ul&gt;&lt;li&gt;データを送信する配信ストリームを選択します。&lt;/li&gt;&lt;li&gt;利用可能なストリームを確認するには、`firehose:ListDeliveryStreams`の権限が必要です。&lt;/li&gt;&lt;li&gt;詳細については、[AWS: Amazon Data Firehoseの制限](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。&lt;/ul&gt;&lt;/li&gt; |

#### メッセージデータ

| **パラメータ** | **説明** |
| --- | --- |
| レコードの接尾辞 | &lt;ul&gt;&lt;li&gt;各レコードの末尾に追加する接尾辞で、区切り文字として使用されます。&lt;/li&gt;&lt;li&gt;デフォルトは`Newline`です。&lt;/ul&gt;&lt;/li&gt; |
| メッセージテンプレート変数 | &lt;ul&gt;&lt;li&gt;（オプション）テンプレートにデータ入力としてテンプレート変数を提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;例えば、`items.name`のようにドット表記でネストされたテンプレート変数を名前付けします。&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/ul&gt;&lt;/li&gt; |
| メッセージテンプレート | &lt;ul&gt;&lt;li&gt;（オプション）`URL`、`URL`パラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは、サポートされるフィールドに名前で二重中括弧で注入されます。&lt;/li&gt;&lt;li&gt;例：`{{SomeTemplateName}}`。&lt;/ul&gt;&lt;/li&gt; |

### 配信ストリームへのログイベント送信

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| 配信ストリーム | &lt;ul&gt;&lt;li&gt;データを送信する配信ストリームを選択します。&lt;/li&gt;&lt;li&gt;利用可能なストリームを確認するには、`firehose:ListDeliveryStreams`の権限が必要です。&lt;/li&gt;&lt;li&gt;詳細については、[AWS: Amazon Data Firehoseの制限](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。&lt;/ul&gt;&lt;/li&gt; |
| レコードの接尾辞 | &lt;ul&gt;&lt;li&gt;各レコードの末尾に追加される接尾辞で、区切り文字として使用されます。&lt;/li&gt;&lt;li&gt;デフォルトは`Newline`です。&lt;/ul&gt;&lt;/li&gt; |

### 配信ストリームへの訪問データ送信


#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 配信ストリーム | &lt;ul&gt;&lt;li&gt;データを送信する配信ストリームを選択します。&lt;/li&gt;&lt;li&gt;利用可能なストリームを表示するには、`firehose:ListDeliveryStreams` 権限が必要です。&lt;/li&gt;&lt;li&gt;詳細については、[AWS: Amazon Data Firehose クォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。&lt;/ul&gt;&lt;/li&gt; |
| レコードサフィックス | &lt;ul&gt;&lt;li&gt;各レコードの末尾に追加するサフィックスとしての区切り文字。&lt;/li&gt;&lt;li&gt;デフォルトは `Newline` です。&lt;/ul&gt;&lt;/li&gt; |
| 現在の訪問データを含む | 現在の訪問データをペイロードに追加します。これには、現在の訪問イベントデータの除外が選択されていない場合のイベント訪問データが含まれます。 |
| 現在の訪問イベントデータを除外 | 現在の訪問データからイベントデータを除外します。 |
| 属性名を印刷 | 属性名が更新された場合、ペイロードの名前が更新を反映します。 |

### 配信ストリームへのカスタマイズデータの送信（バッチ処理）

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 配信ストリーム | &lt;ul&gt;&lt;li&gt;データを送信する配信ストリームを選択します。&lt;/li&gt;&lt;li&gt;利用可能なストリームを表示するには、`firehose:ListDeliveryStreams` 権限が必要です。&lt;/li&gt;&lt;li&gt;詳細については、[AWS: Amazon Data Firehose クォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。&lt;/ul&gt;&lt;/li&gt; |

#### メッセージデータ


| **パラメータ** | **説明** |
| --- | --- |
| レコードサフィックス | &lt;ul&gt;&lt;li&gt;各レコードの末尾に追加するサフィックスとしての区切り文字。&lt;/li&gt;&lt;li&gt;デフォルトは `Newline` です。&lt;/ul&gt;&lt;/li&gt; |
| メッセージテンプレート変数 | &lt;ul&gt;&lt;li&gt;（オプション）テンプレートにデータ入力としてテンプレート変数を提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記を使用してネストされたテンプレート変数を名前付けします。例えば、`items.name`。&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/ul&gt;&lt;/li&gt; |
| メッセージテンプレート | &lt;ul&gt;&lt;li&gt;（オプション）`URL`、`URL` パラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは、サポートされるフィールドに名前で二重中括弧を使用して注入されます。&lt;/li&gt;&lt;li&gt;例えば、`{{SomeTemplateName}}`。&lt;/ul&gt;&lt;/li&gt; |

### 配信ストリームへのイベントデータの送信（バッチ処理）

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 配信ストリーム | &lt;ul&gt;&lt;li&gt;データを送信する配信ストリームを選択します。&lt;/li&gt;&lt;li&gt;利用可能なストリームを表示するには、`firehose:ListDeliveryStreams` 権限が必要です。&lt;/li&gt;&lt;li&gt;詳細については、[AWS: Amazon Data Firehose クォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。&lt;/ul&gt;&lt;/li&gt; |
| レコードサフィックス | &lt;ul&gt;&lt;li&gt;各レコードの末尾に追加するサフィックスとしての区切り文字。&lt;/li&gt;&lt;li&gt;デフォルトは `Newline` です。&lt;/ul&gt;&lt;/li&gt; |
| 属性名を印刷 | 属性名が更新された場合、ペイロードの名前が更新を反映します。 |