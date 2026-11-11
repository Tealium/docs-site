---
title: Amazon AWS SQSコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでAWS SQSコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/amazon-aws-sqs-connector/
---
Amazon SQSは、マイクロサービス、分散システム、サーバーレスアプリケーション向けのフルマネージド型メッセージキューを提供します。

## 要件

* AWSアカウント
* （必須）`sqs:SendMessage`権限
* （任意）`sqs:ListQueues`権限
* データの送信先となるキュー

## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|イベントデータをキューに送信| ✗| ✓|
|イベントデータをキューに送信（バッチ）| ✗| ✓|
|訪問データをキューに送信| ✓| ✗|
|訪問データをキューに送信（バッチ）| ✓| ✗|
|カスタマイズしたデータをキューに送信（詳細）| ✓| ✓|
|カスタマイズしたデータをキューに送信（詳細バッチ）| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **アクセスキー**
  * （必須）IAMユーザーのアクセスキーを指定します。関連付けられたIAMポリシー（IAMユーザーまたは引き受けるロールのいずれか）で、`sqs:SendMessage`権限が付与されている必要があります。
  * 詳細については、[Amazon SQSのアクセス制御](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-authentication-and-access-control.htm)を参照してください。

* **シークレットキー**
  * （必須）IAMユーザーのシークレットキーを指定します。

* **リージョン**
  * （必須）リージョンを選択します。

* **引き受けるロール：ARN**
  * （任意）引き受けるロールのAmazonリソースネーム（ARN）を指定します。  
例：`arn:aws:iam::222222222222:role/myrole`
  * 詳細については、[IAMロールへの切り替え](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)を参照してください。

* **引き受けるロール：セッション名**
  * （任意）引き受けるロールセッションの識別子を指定します。

* **引き受けるロール：外部ID**
  * （任意）外部識別子を指定します。
  * 詳細については、[外部IDの使用方法](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)を参照してください。

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

以下のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### アクション - イベントデータをキューに送信、およびイベントデータをキューに送信（バッチ）

#### バッチ制限

このアクションでは、ベンダーへの大量データ転送に対応するため、バッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。以下のいずれかのしきい値に達するか、プロファイルが公開されるまで、リクエストはキューに保持されます。

* リクエストの最大数：10
* 最も古いリクエストからの最大経過時間：5分
* リクエストの最大サイズ：1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|キュー| <ul><li>（必須）データの送信先となるキューを選択します。</li><li>IAMポリシーで`sqs:ListQueues`権限が付与されていない場合は、カスタム値を手動で入力する必要があります。</li><li>カスタム値にはURLを指定します。例：`https://sqs.us-west-2.amazonaws.com/0123456789/queue_name`</li></ul> |
|MessageGroupId|メッセージが特定のメッセージグループに属することを指定します（FIFOキューのみ）。|
|DelaySeconds|特定のメッセージを遅延させる時間（秒単位、0～900）。|
|属性名を出力|属性名が更新された場合、ペイロード内の名前にも更新が反映されます。|


<blockquote>
[Amazon SQSメッセージ属性の使用](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-message-attributes.html)を参照してください。
</blockquote>


### アクション - 訪問データをキューに送信、および訪問データをキューに送信（バッチ）

#### バッチ制限

「訪問データをキューに送信（バッチ）」アクションでは、ベンダーへの大量データ転送に対応するため、バッチリクエストを使用します。以下のいずれかのしきい値に達するまで、リクエストはキューに保持されます。

* リクエストの最大数：10
* 最も古いリクエストからの最大経過時間：5分
* リクエストの最大サイズ：1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|キュー| <ul><li>（必須）データの送信先となるキューを選択します。</li><li>IAMポリシーで`sqs:ListQueues`権限が付与されていない場合は、カスタム値を手動で入力する必要があります。</li><li>カスタム値にはURLを指定します。例：`https://sqs.us-west-2.amazonaws.com/0123456789/queue_name`</li></ul>|
|MessageGroupId|メッセージが特定のメッセージグループに属することを指定します（FIFOキューのみ）。|
|DelaySeconds|特定のメッセージを遅延させる時間（秒単位、0～900）。|
| 訪問データに現在の訪問データを含める | 現在の訪問データをペイロードに追加します。「現在の訪問のイベントデータを除外」が選択されていない場合は、訪問のイベントデータも含まれます。 |
| 現在の訪問のイベントデータを除外 | 現在の訪問データからイベントデータを除外します。 |
|属性名を出力| 属性名が更新された場合、ペイロード内の名前にも更新が反映されます。|

### アクション - カスタマイズしたデータをキューに送信（詳細）、およびカスタマイズしたデータをキューに送信（詳細バッチ）

#### バッチ制限

「カスタマイズしたデータをキューに送信（詳細バッチ）」アクションでは、ベンダーへの大量データ転送に対応するため、バッチリクエストを使用します。以下のいずれかのしきい値に達するまで、リクエストはキューに保持されます。

* リクエストの最大数：10
* 最も古いリクエストからの最大経過時間：5分
* リクエストの最大サイズ：1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|キュー| <ul><li>（必須）データの送信先となるキューを選択します。</li><li>IAMポリシーで`sqs:ListQueues`権限が付与されていない場合は、カスタム値を手動で入力する必要があります。カスタム値にはURLを指定します。例：`https://sqs.us-west-2.amazonaws.com/0123456789/queue_name`</li></ul>|
|MessageGroupId|メッセージが特定のメッセージグループに属することを指定します（FIFOキューのみ）。|
|DelaySeconds|特定のメッセージを遅延させる時間（秒単位、0～900）。|
|カスタムメッセージ定義||
|メッセージテンプレート変数|<ul><li>（任意）テンプレートのデータ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数にはドット表記で名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は、通常、データレイヤーのリスト属性から構築されます。</li></ul> |
|メッセージテンプレート| <ul><li>（任意）URL、URLパラメータ、ヘッダー、または本文データで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、二重波括弧で囲んだ名前を使用して、サポートされているフィールドに挿入されます。例：`{{SomeTemplateName}}`。</li></ul> |
|メッセージテンプレート変数|<ul><li>（任意）テンプレートのデータ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数にはドット表記で名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は、通常、データレイヤーのリスト属性から構築されます。</li></ul> |
|メッセージテンプレート| <ul><li>（任意）URL、URLパラメータ、ヘッダー、または本文データで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、二重波括弧で囲んだ名前を使用して、サポートされているフィールドに挿入されます。例：`{{SomeTemplateName}}`。</li></ul> |


<blockquote>
[Amazon SQSメッセージ属性の使用](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-message-attributes.html)を参照してください。
</blockquote>

## ベンダーのドキュメント

* [Amazon SQSのアクセス制御](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-authentication-and-access-control.html)
* [IAMロールへの切り替え](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-api.html)
* [外部IDの使用方法](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user_externalid.html)
* [Amazon SQSメッセージ属性の使用](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-message-attributes.html)
* [Amazon SQSキューの仕組み](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-how-it-works.html)