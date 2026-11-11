---
title: AWS Firehoseコネクタ構成ガイド
description: この記事では、AWS Firehoseコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/aws-firehose-connector/
---
## 要件

* AWSアカウント。
* （必須）**firehose:PutRecord**権限。
* （任意）**firehose:ListDeliveryStreams**権限。
* データの送信先となる配信ストリーム。

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

ベンダーを構成するには、次の手順に従います。

1. **構成タブ**で、コネクタインスタンスのタイトルを入力します。
1. IAMユーザーのアクセスキーとシークレットキーを入力します。
<blockquote>
IAMユーザーインスタンスにアタッチされているポリシーステートメントには、**firehose:PutRecord**権限を含め、External ID条件を使用してTealiumルートアカウント（`arn:aws:iam::757913464184:root`）を許可する必要があります。Firehoseのポリシーについて詳しくは、[AWS：Amazon Data Firehoseによるアクセスの制御](https://docs.aws.amazon.com/firehose/latest/dev/controlling-access.html)を参照してください。
</blockquote>

1. API呼び出しを行うリージョンを選択します。
1. **ロール引き受けパラメータ**：IAMユーザーに必要な権限がすべて構成されていない場合にのみ必要です。IAMロール名には、`TealiumFirehose`プレフィックスを含める必要があります。詳細については、[AWS：IAMロールへの切り替え](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)を参照してください。
  * **ARN**：（必須）引き受けるロールに割り当てられたAmazonリソースネーム。
  * **セッション名**：（必須）引き受けたロールセッションの一意の識別子。
  * **External ID**：（任意）サードパーティが顧客のアカウントでロールを引き受ける際に使用する一意の識別子。詳細については、[AWS：サードパーティが所有するAWSアカウントへのアクセス](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)を参照してください。
1. **接続をテスト**をクリックし、入力した認証情報でAPIに接続できることを確認します。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| ----------- | :------------: | :---------: |
| イベントデータを配信ストリームに送信 | ✗ | ✓ |
| 訪問データを配信ストリームに送信 | ✓ | ✗ |
| カスタマイズしたデータを配信ストリームに送信（詳細構成） | ✓ | ✓ |
| ログイベントを配信ストリームに送信 | ✗ | ✓ |
| カスタマイズしたデータを配信ストリームに送信（バッチ処理） | ✓ | ✓ |
| イベントデータを配信ストリームに送信（バッチ処理） | ✗ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。次のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### イベントデータを配信ストリームに送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 配信ストリーム | （必須）データの送信先となる配信ストリームを選択します。使用可能なストリームを表示するには、`firehose:ListDeliveryStreams`権限を付与する必要があります。 |
| レコードサフィックス | 区切り文字として各レコードの末尾に追加する値を選択します。<br>オプション：<ul><li>`Newline (\n)`（デフォルト）- レコードの末尾に改行文字を追加します。</li><li>`No Delimiter` - レコードには何も追加しません。</li></ul> |
| 属性名を出力 | メッセージペイロードに各イベントデータ属性の名前を表示するには、このオプションを選択します。 |

### 訪問データを配信ストリームに送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 配信ストリーム | （必須）データの送信先となる配信ストリームを選択します。使用可能なストリームを表示するには、`firehose:ListDeliveryStreams`権限を付与する必要があります。 |
| レコードサフィックス | 区切り文字として各レコードの末尾に追加する値を選択します。<br>オプション：<ul><li>`Newline (\n)`（デフォルト）- レコードの末尾に改行文字を追加します。</li><li>`No Delimiter` - レコードには何も追加しません。</li></ul> |
| 現在の訪問データを含める | 現在の訪問データをペイロードに追加します。「現在の訪問のイベントデータを除外」が選択されていない場合、イベントの訪問データも含まれます。 |
| 現在の訪問のイベントデータを除外 | 現在の訪問データからイベントデータを除外します。 |
| 属性名を出力 | メッセージペイロードに各訪問データ属性の名前を表示するには、このオプションを選択します。 |

### カスタマイズしたデータを配信ストリームに送信（詳細構成）

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 配信ストリーム | （必須）データの送信先となる配信ストリームを選択します。使用可能なストリームを表示するには、`firehose:ListDeliveryStreams`権限を付与する必要があります。 |
| レコードサフィックス | 区切り文字として各レコードの末尾に追加する値を選択します。<br>オプション：<ul><li>`Newline (\n)`（デフォルト）- レコードの末尾に改行文字を追加します。</li><li>`No Delimiter` - レコードには何も追加しません。</li></ul> |
| メッセージデータ | （必須）カスタムメッセージ本文を作成します。シンプルな1階層のJSON形式で属性を名前にマッピングするか、二重波括弧で囲まれたテンプレート名を参照して、**カスタムメッセージ定義**オプションを選択します。 |
| メッセージテンプレート変数 | 属性をテンプレート変数名にマッピングします。テンプレート変数は、すべてのテンプレートで値の置換とレンダリングに使用できます。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| メッセージテンプレート | レンダリングするテンプレートを1つ以上指定します。通常、メッセージデータの作成には単一のテンプレートを使用します。構文と拡張機能について詳しくは、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。 |

### ログイベントを配信ストリームに送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 配信ストリーム | （必須）データの送信先となる配信ストリームを選択します。使用可能なストリームを表示するには、`firehose:ListDeliveryStreams`権限を付与する必要があります。 |
| レコードサフィックス | 区切り文字として各レコードの末尾に追加する値を選択します。<br>オプション：<ul><li>`Newline (\n)`（デフォルト）- レコードの末尾に改行文字を追加します。</li><li>`No Delimiter` - レコードには何も追加しません。</li></ul> |

### カスタマイズしたデータを配信ストリームに送信（バッチ処理）

#### バッチの制限

このアクションでは、ベンダーへの大量データ転送に対応するため、バッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに保持されます。

* リクエストの最大数：500
* 最も古いリクエストからの最大経過時間：10分
* リクエストの最大サイズ：4 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 配信ストリーム | データの送信先となる配信ストリームを選択します。使用可能なストリームを表示するには、`firehose:ListDeliveryStreams`権限を付与する必要があります。Amazon Kinesis Data Firehoseの配信ストリームには制限があります。詳細については、[AWS：Amazon Data Firehoseのクォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。 |
| レコードサフィックス | 区切り文字として各レコードの末尾に追加する値を選択します。<br>オプション：<ul><li>`Newline (\n)`（デフォルト）- レコードの末尾に改行文字を追加します。</li><li>`No Delimiter` - レコードには何も追加しません。</li></ul> |

#### メッセージデータ

| **パラメータ** | **説明** |
| --- | --- |
| メッセージテンプレート変数 | 属性をテンプレート変数名にマッピングします。テンプレート変数は、すべてのテンプレートで値の置換とレンダリングに使用できます。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。 |
| メッセージテンプレート | レンダリングするテンプレートを1つ以上指定します。通常、メッセージデータの作成には単一のテンプレートを使用します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。 |

### イベントデータを配信ストリームに送信（バッチ処理）

#### バッチの制限

このアクションでは、ベンダーへの大量データ転送に対応するため、バッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに保持されます。

* リクエストの最大数：500
* 最も古いリクエストからの最大経過時間：10分
* リクエストの最大サイズ：4 MB
#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| 配信ストリーム | データの送信先となる配信ストリームを選択します。利用可能なストリームを表示するには、`firehose:ListDeliveryStreams` 権限が付与されている必要があります。Amazon Kinesis Data Firehose の配信ストリームには制限があります。詳細については、[AWS：Amazon Data Firehose のクォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)を参照してください。 |
| レコードのサフィックス | 区切り文字として各レコードの末尾に追加する値を選択します。<br>オプション：<ul><li>`Newline (\n)`（デフォルト）- レコードの末尾に改行文字を追加します。</li><li>`No Delimiter` - レコードに何も追加しません。</li></ul> |
| 属性名を出力 | 属性名が更新された場合、ペイロード内の名前にも更新内容が反映されます。 |

## ベンダーのドキュメント

* [AWS：Amazon Data Firehose とは？](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)
* [AWS：Amazon Data Firehose のクォータ](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)
* [AWS：Amazon Data Firehose によるアクセス制御](https://docs.aws.amazon.com/firehose/latest/dev/controlling-access.html)
* [AWS：IAM ロールへの切り替え（AWS API）](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)
* [AWS：第三者が所有する AWS アカウントへのアクセス](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)