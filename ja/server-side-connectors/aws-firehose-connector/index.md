---
title: AWS Firehoseコネクタ構成ガイド
description: この記事では、AWS Firehoseコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/aws-firehose-connector/
---
## 要件

* AWSアカウント。
* （必須）**firehose:PutRecord** 権限。
* （オプション）**firehose:ListDeliveryStreams** 権限。
* データを送信するデリバリーストリーム。

## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

ベンダーを構成するには、以下の手順に従います：

1. **構成タブ**で、コネクタインスタンスのタイトルを入力します。
1. IAMユーザーのアクセスキーとシークレットキーを提供します。
<blockquote>
IAMユーザーインスタンスに添付されたポリシーステートメントには**firehose:PutRecord**権限が含まれ、外部ID条件でTealiumルートアカウント（`arn:aws:iam::757913464184:root`）を許可する必要があります。Firehoseのポリシーについての詳細は、[AWS: Amazon Data Firehoseでのアクセス制御](https://docs.aws.amazon.com/firehose/latest/dev/controlling-access.html)を参照してください。
</blockquote>

1. API呼び出しを行いたいリージョンを選択します。
1. **Assume Role Parameters**: IAMユーザーが必要なすべての権限を構成していない場合のみ必要です。IAMロール名には`TealiumFirehose`プレフィックスが含まれている必要があります。詳細については、[AWS: IAMロールへの切り替え](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)を参照してください。
  * **ARN**: （必須）ロールを引き受けるために割り当てられたAmazonリソース名。
  * **Session Name**: （必須）引き受けたロールセッションの一意の識別子。
  * **External ID**: （オプション）第三者が顧客のアカウントでロールを引き受ける際に使用する一意の識別子。詳細については、[AWS: 第三者が所有するAWSアカウントへのアクセス](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)を参照してください。
1. **Test Connection**をクリックして、提供された認証情報でAPI接続性を確認します。

## アクション

| アクション名 | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| デリバリーストリームへのイベントデータ送信 | ✗ | ✓ |
| デリバリーストリームへの訪問データ送信 | ✓ | ✗ |
| デリバリーストリームへのカスタマイズデータ送信（高度） | ✓ | ✓ |
| デリバリーストリームへのログイベント送信 | ✗ | ✓ |
| デリバリーストリームへのカスタマイズデータ送信（バッチ処理） | ✓ | ✓ |
| デリバリーストリームへのイベントデータ送信（バッチ処理） | ✗ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### デリバリーストリームへのイベントデータ送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| デリバリーストリーム | （必須）データを送信するデリバリーストリームを選択します。利用可能なストリームを表示するには、`firehose:ListDeliveryStreams`権限が必要です。 |
| レコードサフィックス | 各レコードに追加する値を選択します。<br>オプション：<ul><li>`Newline (\n)`（デフォルト） - レコードの最後にリターン文字を追加します。</li><li>`No Delimiter` - レコードに何も追加しません。</li></ul> |
| 属性名の表示 | 各イベントデータ属性の名前をメッセージペイロードに表示するオプションを選択します。 |

### デリバリーストリームへの訪問データ送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| デリバリーストリーム | （必須）データを送信するデリバリーストリームを選択します。利用可能なストリームを表示するには、`firehose:ListDeliveryStreams`権限が必要です。 |
| レコードサフィックス | 各レコードに追加する値を選択します。<br>オプション：<ul><li>`Newline (\n)`（デフォルト） - レコードの最後にリターン文字を追加します。</li><li>`No Delimiter` - レコードに何も追加しません。</li></ul> |
| 現在の訪問データの含有 | ペイロードに現在の訪問データを追加します。これには、現在の訪問イベントデータが除外されていない場合のイベント訪問データが含まれます。 |
| 現在の訪問イベントデータの除外 | 現在の訪問データからイベントデータを除外します。 |
| 属性名の表示 | 各訪問データ属性の名前をメッセージペイロードに表示するオプションを選択します。 |

### デリバリーストリームへのカスタマイズデータ送信（高度）

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| デリバリーストリーム | （必須）データを送信するデリバリーストリームを選択します。利用可能なストリームを表示するには、`firehose:ListDeliveryStreams`権限が必要です。 |
| レコードサフィックス | 各レコードに追加する値を選択します。<br>オプション：<ul><li>`Newline (\n)`（デフォルト） - レコードの最後にリターン文字を追加します。</li><li>`No Delimiter` - レコードに何も追加しません。</li></ul> |
| メッセージデータ | （必須）カスタムメッセージ本文を構築します。属性を単純な1レベルのJSON形式で名前にマッピングするか、二重中括弧で囲まれたテンプレート名を参照し、**カスタムメッセージ定義**オプションを選択します。 |
| メッセージテンプレート変数 | 属性をテンプレート変数名にマッピングします。テンプレート変数は、すべてのテンプレートの置換およびレンダリングに使用できます。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| メッセージテンプレート | レンダリングに使用する1つ以上のテンプレートを提供します。通常、単一のテンプレートがメッセージデータの構築に使用されます。構文と拡張についての詳細は、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。 |

### デリバリーストリームへのログイベント送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| デリバリーストリーム | （必須）データを送信するデリバリーストリームを選択します。利用可能なストリームを表示するには、`firehose:ListDeliveryStreams`権限が必要です。 |
| レコードサフィックス | 各レコードに追加する値を選択します。<br>オプション：<ul><li>`Newline (\n)`（デフォルト） - レコードの最後にリターン文字を追加します。</li><li>`No Delimiter` - レコードに何も追加しません。</li></ul> |

### デリバリーストリームへのカスタマイズデータ送信（バッチ処理）

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：500
* 最古のリクエストからの最大時間：10分
* リクエストの最大サイズ：4 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| デリバリーストリーム | データを送信するデリバリーストリームを選択します。利用可能なストリームを表示するには、`firehose:ListDeliveryStreams`権限が必要です。Amazon Kinesis Data Firehoseデリバリーストリームには制限があります。詳細については、[AWS: Amazon Data Firehoseの制限](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。 |
| レコードサフィックス | 各レコードに追加する値を選択します。<br>オプション：<ul><li>`Newline (\n)`（デフォルト） - レコードの最後にリターン文字を追加します。</li><li>`No Delimiter` - レコードに何も追加しません。</li></ul> |

#### メッセージデータ

| **パラメータ** | **説明** |
| --- | --- |
| メッセージテンプレート変数 | 属性をテンプレート変数名にマッピングします。テンプレート変数は、すべてのテンプレートの置換およびレンダリングに使用できます。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| メッセージテンプレート | レンダリングに使用する1つ以上のテンプレートを提供します。通常、単一のテンプレートがメッセージデータの構築に使用されます。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。 |

### デリバリーストリームへのイベントデータ送信（バッチ処理）

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：500
* 最古のリクエストからの最大時間：10分
* リクエストの最大サイズ：4 MB
#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 配信ストリーム | データを送信する配信ストリームを選択します。利用可能なストリームを表示するには、`firehose:ListDeliveryStreams` 権限が必要です。Amazon Kinesis Data Firehose 配信ストリームには制限があります。詳細については、[AWS: Amazon Data Firehose クォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。 |
| レコードサフィックス | 各レコードの末尾に追加する値を選択します。<br>オプション：<ul><li>`Newline (\n)`（デフォルト） - レコードの最後にリターン文字を追加します。</li><li>`No Delimiter` - レコードに何も追加されません。</li></ul> |
| 属性名の印刷 | 属性名が更新された場合、ペイロード内の名前が更新を反映します。 |

## ベンダー文書

* [AWS: Amazon Data Firehose とは？](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)
* [AWS: Amazon Data Firehose クォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)
* [AWS: Amazon Data Firehose でのアクセス制御](https://docs.aws.amazon.com/firehose/latest/dev/controlling-access.html)
* [AWS: IAM ロールへの切り替え (AWS API)](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)
* [AWS: 第三者が所有する AWS アカウントへのアクセス](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)