---
title: Amazon AWS SQSコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでAWS SQSコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/amazon-aws-sqs-connector/
---
Amazon SQSは、マイクロサービス、分散システム、サーバーレスアプリケーション用の完全に管理されたメッセージキューを提供します。

## 要件

* AWSアカウント
* 必須: `sqs:SendMessage` 権限
* 任意: `sqs:ListQueues` 権限
* データを送信するキュー

## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|キューへのイベントデータ送信| ✗| ✓|
|キューへのイベントデータ送信（バッチ）| ✗| ✓|
|キューへの訪問データ送信| ✓| ✗|
|キューへの訪問データ送信（バッチ）| ✓| ✗|
|キューへのカスタマイズデータ送信（高度）| ✓| ✓|
|キューへのカスタマイズデータ送信（高度バッチ）| ✓| ✓| 

## 構成の構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **アクセスキー**
  * 必須。IAMユーザーのアクセスキーを提供してください。関連するIAMポリシー（IAMユーザーまたは想定されるロール用）は`sqs:SendMessage`権限を付与する必要があります。
  * 詳細については、[Amazon SQSのアクセス制御](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-authentication-and-access-control.htm)を参照してください。

* **シークレットキー**
  * 必須。IAMユーザーのシークレットキーを提供してください

* **リージョン**
  * 必須。リージョンを選択してください。

* **ロールの想定: ARN**
  * 任意: 想定するロールのAmazonリソースネーム（ARN）を提供してください。  
例: `arn:aws:iam::222222222222:role/myrole`
  * 詳細については、[IAMロールへの切り替え](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)を参照してください。

* **ロールの想定: セッション名**
  * 任意: 想定されるロールセッションの識別子を提供してください。

* **ロールの想定: 外部ID**
  * 任意: 外部識別子を提供してください。
  * 詳細については、[外部IDの使用方法](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - キューへのイベントデータ送信およびキューへのイベントデータ送信（バッチ）

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数: 10
* 最古のリクエストからの最大時間: 5分
* リクエストの最大サイズ: 1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Queue|  <ul><li>必須。データを送信するキューを選択してください。</li><li>IAMポリシーが`sqs:ListQueues`権限を付与していない場合、カスタム値を手動で入力する必要があります。</li><li>カスタム値はURLである必要があります。例: `https://sqs.us-west-2.amazonaws.com/0123456789/queue_name`</li></ul> |
|MessageGroupId|メッセージが特定のメッセージグループに属していることを指定します（FIFOキューのみ）。|
|DelaySeconds|特定のメッセージを遅延させる時間（秒）（0から900）。|
|Print Attribute Names|属性名が更新された場合、ペイロード内の名前が更新を反映します。|


<blockquote>
[Amazon SQSメッセージ属性の使用](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-message-attributes.html)を参照してください。
</blockquote>


### アクション - キューへの訪問データ送信およびキューへの訪問データ送信（バッチ）

#### バッチ制限

キューへの訪問データ送信（バッチ）アクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。リクエストは、次のいずれかの閾値に達するまでキューに入れられます：

* 最大リクエスト数: 10
* 最古のリクエストからの最大時間: 5分
* リクエストの最大サイズ: 1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Queue|  <ul><li>必須。データを送信するキューを選択してください。</li><li>IAMポリシーが`sqs:ListQueues`権限を付与していない場合、カスタム値を手動で入力する必要があります。</li><li>カスタム値はURLである必要があります。例: `https://sqs.us-west-2.amazonaws.com/0123456789/queue_name`</li></ul>|
|MessageGroupId|メッセージが特定のメッセージグループに属していることを指定します（FIFOキューのみ）。|
|DelaySeconds|特定のメッセージを遅延させる時間（秒）（0から900）。|
| Include Current Visit Data With Visitor Data | 訪問データに現在の訪問データを追加します。これには、Exclude Current Visit Event Dataが選択されていない場合のイベント訪問データが含まれます。 |
| Exclude Current Visit Event Data | 現在の訪問データからイベントデータを除外します。 |
|Print Attribute Names| 属性名が更新された場合、ペイロード内の名前が更新を反映します。|

### アクション - キューへのカスタマイズデータ送信（高度）およびキューへのカスタマイズデータ送信（高度バッチ）

#### バッチ制限

キューへのカスタマイズデータ送信（高度バッチ）アクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。リクエストは、次のいずれかの閾値に達するまでキューに入れられます：

* 最大リクエスト数: 10
* 最古のリクエストからの最大時間: 5分
* リクエストの最大サイズ: 1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Queue|  <ul><li>必須。データを送信するキューを選択してください。</li><li>IAMポリシーが`sqs:ListQueues`権限を付与していない場合、カスタム値を手動で入力する必要があります。カスタム値はURLである必要があります。例: `https://sqs.us-west-2.amazonaws.com/0123456789/queue_name`</li></ul>|
|MessageGroupId|メッセージが特定のメッセージグループに属していることを指定します（FIFOキューのみ）。|
|DelaySeconds|特定のメッセージを遅延させる時間（秒）（0から900）。|
|Custom Message Definition||
|Message Template Variables|<ul><li>任意: テンプレート変数をテンプレートのデータ入力として提供してください。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記でネストされたテンプレート変数を名前付けしてください。例: `items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul> |
|Message Templates|  <ul><li>任意: URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供してください。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、名前でサポートされるフィールドに二重中括弧で注入されます。例: `{{SomeTemplateName}}`。</li></ul> |
|Message Template Variables|<ul><li>任意: テンプレート変数をテンプレートのデータ入力として提供してください。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記でネストされたテンプレート変数を名前付けしてください。例: `items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul> |
|Message Templates|  <ul><li>任意: URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供してください。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、名前でサポートされるフィールドに二重中括弧で注入されます。例: `{{SomeTemplateName}}`。</li></ul> |


<blockquote>
[Amazon SQSメッセージ属性の使用](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-message-attributes.html)を参照してください。
</blockquote>

## ベンダー文書

* [Amazon SQSのアクセス制御](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-authentication-and-access-control.html)
* [IAMロールへの切り替え](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)
* [外部IDの使用方法](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)
* [Amazon SQSメッセージ属性の使用](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-message-attributes.html)
* [Amazon SQSキューの仕組み](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-how-it-works.html)
