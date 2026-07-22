---
title: APSISコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでAPSISコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/apsis-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|Create Subscriber and Add to Mailing List (Queued)| ✓| ✗|
|Update Subscriber (Queued)| ✓| ✗|
|Add Subscriber to Mailing List| ✓| ✗|
|Remove Subscriber from Mailing List| ✓| ✗|
|Delete Subscriber (Queued)| ✓| ✗|
|Send Transactional Email| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[Connector Overview](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**
  * APIキーを取得するには、APSIS Proアカウントにログインし、**アカウント**セクションを選択します。
  * **APIキー**リンクを見つけて、新しいAPIキーを生成します。
  * 1つのアカウントで複数のAPIキーを持つことができます。
  * **アカウント構成**セクションでキーを管理できます。
  * 詳細については、[APSIS: Getting Started](http://se.apidoc.anpdm.com/Help/GettingStarted/Getting%20started)を参照してください。

## アクション構成 - パラメータとオプション

**Next**をクリックするか、**Actions**タブに進みます。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - Create Subscriber and Add to Mailing List (Queued)

##### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[Batched Actions](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数：10
* 最古のリクエストからの最大時間：1分
* リクエストの最大サイズ：1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Mailing List|  <ul><li>追加するメーリングリストのID。</li><li>メーリングリストIDを知っている場合は、カスタム値として入力できます。</li><li>追加するリストを選択するか、リストIDを直接提供します。</li><li>詳細については、[SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber)を参照してください。</li></ul> |
|Create Mode|  <ul><li>登録者のアカウントがすでに存在している場合、このパラメータが「Create or Update」に構成されていると、登録者のデータが更新されます。</li><li>ダブルオプトインで登録する場合、既存の登録者を更新することはできません。</li></ul> |
|Country code|  <ul><li>登録者の国コード。</li></ul> |
|Desired format|  <ul><li>登録者が希望するフォーマット。</li></ul> |
|Email address|  <ul><li>(必須) 登録者のメールアドレス。</li></ul> |
|External ID|  <ul><li>登録者の外部ID。</li></ul> |
|Name|  <ul><li>登録者の名前。</li></ul> |
|Password|  <ul><li>登録者のパスワード。</li></ul> |
|Phone number|  <ul><li>登録者の電話番号。</li></ul> |
|Demographic Data|  <ul><li>登録者のデモグラフィックデータフィールドのリスト。</li><li>データフィールドのキーと可能な値は、APSISアカウント管理コンソールで定義されています。</li></ul> |
|Template Variables|  <ul><li>(オプション) デモグラフィックデータ用のテンプレート変数を提供します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記でネストされたテンプレート変数を命名します。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul> |
|Templates|  <ul><li>(オプション) デモグラフィックデータで参照するテンプレートを提供します。</li><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、サポートされるフィールドに名前で二重中括弧を使用して挿入されます。</li><li>例：`{{SomeTemplateName}}`。</li></ul> |

### アクション - Update Subscriber (Queued)

##### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[Batched Actions](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数：10
* 最古のリクエストからの最大時間：1分
* リクエストの最大サイズ：1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Country code|  <ul><li>登録者の国コード。</li></ul> |
|Desired format|  <ul><li>登録者が希望するフォーマット。</li></ul> |
|Email address|  <ul><li>(必須) 登録者のメールアドレス。</li></ul> |
|Name|  <ul><li>登録者の名前。</li></ul> |
|Password|  <ul><li>登録者のパスワード。</li></ul> |
|Phone number|  <ul><li>登録者の電話番号。</li></ul> |
|User ID|  <ul><li>登録者のID。</li><li>詳細については、[Update Subscribers](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)を参照してください。</li></ul> |
|Demographic Data|  <ul><li>登録者のデモグラフィックデータフィールドのリスト。</li><li>データフィールドのキーと可能な値は、アカウント管理コンソールで定義されています。</li></ul> |
|Template Variables|  <ul><li>(オプション) デモグラフィックデータ用のテンプレート変数を提供します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記でネストされたテンプレート変数を命名します。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul> |
|Templates|  <ul><li>(オプション) デモグラフィックデータで参照するテンプレートを提供します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>テンプレートは、サポートされるフィールドに名前で二重中括弧を使用して挿入されます。</li><li>例：`{{SomeTemplateName}}`。</li></ul> |

### アクション - Add Subscriber to Mailing List

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Mailing List|  <ul><li>追加するメーリングリストを選択するか、リストIDを直接提供します。</li><li>詳細については、[SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber)を参照してください。</li><li>メーリングリストIDを知っている場合は、カスタム値として入力できます。</li></ul> |
|Subscriber's Email|  <ul><li>(必須) 登録者のメールアドレス。</li></ul> |
|Subscriber's ID|  <ul><li>登録者のID。</li><li>詳細については、[Update Subscribers](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)を参照してください。</li></ul> |

### アクション - Remove Subscriber from Mailing List

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Mailing List|  <ul><li>追加するメーリングリストを選択するか、リストIDを直接提供します。</li><li>詳細については、[SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber)を参照してください。</li><li>メーリングリストIDを知っている場合は、カスタム値として入力できます。</li></ul> |
|Subscriber's Email|  <ul><li>(必須) 登録者のメールアドレス。</li></ul> |
|Subscriber's Id|  <ul><li>登録者のID。</li><li>詳細については、[Update Subscribers](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)を参照してください。</li></ul> |

### アクション - Delete Subscriber (Queued)

##### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[Batched Actions](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数：10
* 最古のリクエストからの最大時間：1分
* リクエストの最大サイズ：1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Subscriber's Email|  <ul><li>(必須) 登録者のメールアドレス。</li></ul> |

### アクション - Send Transactional Email


#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|トランザクショナルプロジェクト|  <ul><li>トランザクショナルプロジェクトを選択します。</li><li>プロジェクトのID。</li><li>詳細については、[トランザクショナルメールの送信](http://se.apidoc.anpdm.com/Browse/Method/TransactionalService/SendTransactionalEmail)を参照してください。</li></ul> |
|非アクティブプロジェクトの無効化|  <ul><li>プロジェクトが非アクティブの場合に送信を許可するかどうかを示す真偽値</li><li>デフォルト値は **true** です。</li></ul> |
|国コード|  <ul><li>加入者の国コード。</li></ul> |
|HTML用のデモグラフィックデータ|  <ul><li>加入者のデモグラフィックデータフィールドのリスト。</li><li>データフィールドのキーと可能な値は、APSISアカウント管理コンソールで定義されています。</li></ul> |
|希望の形式|  <ul><li>加入者が希望する形式。</li></ul> |
|メールアドレス|  <ul><li>(必須) 加入者のメールアドレス</li></ul> |
|外部ID|  <ul><li>加入者の外部ID。</li></ul> |
|名前|  <ul><li>加入者の名前。</li></ul> |
|電話番号|  <ul><li>加入者の電話番号。</li></ul> |
|送信日|  <ul><li>送信日。</li></ul> |
|送信タイプ|  <ul><li>可能な値:  <ul><li>**m** - マーケティング</li><li>**t** - トランザクショナル（デフォルト）</li></ul> </li></ul> |
|デモグラフィックデータ|  <ul><li>加入者のデモグラフィックデータフィールドのリスト。</li><li>データフィールドのキーと可能な値は、APSISアカウント管理コンソールで定義されています。</li></ul> |
|テンプレート変数|  <ul><li>(オプション) デモグラフィックデータ用のテンプレート変数を提供します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記でネストされたテンプレート変数を名付けます。</li><li>例: `items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul> |
|テンプレート|  <ul><li>(オプション) デモグラフィックデータで参照されるテンプレートを提供します。</li><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは名前で指定され、サポートされるフィールドに二重中括弧で注入されます。</li><li>例: `{{SomeTemplateName}}`。</li></ul> |