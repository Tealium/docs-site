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

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[Connector Overview]()の記事を参照してください。

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

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[Batched Actions]()を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数：10
* 最古のリクエストからの最大時間：1分
* リクエストの最大サイズ：1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Mailing List|  &lt;ul&gt;&lt;li&gt;追加するメーリングリストのID。&lt;/li&gt;&lt;li&gt;メーリングリストIDを知っている場合は、カスタム値として入力できます。&lt;/li&gt;&lt;li&gt;追加するリストを選択するか、リストIDを直接提供します。&lt;/li&gt;&lt;li&gt;詳細については、[SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Create Mode|  &lt;ul&gt;&lt;li&gt;登録者のアカウントがすでに存在している場合、このパラメータが「Create or Update」に構成されていると、登録者のデータが更新されます。&lt;/li&gt;&lt;li&gt;ダブルオプトインで登録する場合、既存の登録者を更新することはできません。&lt;/li&gt;&lt;/ul&gt; |
|Country code|  &lt;ul&gt;&lt;li&gt;登録者の国コード。&lt;/li&gt;&lt;/ul&gt; |
|Desired format|  &lt;ul&gt;&lt;li&gt;登録者が希望するフォーマット。&lt;/li&gt;&lt;/ul&gt; |
|Email address|  &lt;ul&gt;&lt;li&gt;(必須) 登録者のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|External ID|  &lt;ul&gt;&lt;li&gt;登録者の外部ID。&lt;/li&gt;&lt;/ul&gt; |
|Name|  &lt;ul&gt;&lt;li&gt;登録者の名前。&lt;/li&gt;&lt;/ul&gt; |
|Password|  &lt;ul&gt;&lt;li&gt;登録者のパスワード。&lt;/li&gt;&lt;/ul&gt; |
|Phone number|  &lt;ul&gt;&lt;li&gt;登録者の電話番号。&lt;/li&gt;&lt;/ul&gt; |
|Demographic Data|  &lt;ul&gt;&lt;li&gt;登録者のデモグラフィックデータフィールドのリスト。&lt;/li&gt;&lt;li&gt;データフィールドのキーと可能な値は、APSISアカウント管理コンソールで定義されています。&lt;/li&gt;&lt;/ul&gt; |
|Template Variables|  &lt;ul&gt;&lt;li&gt;(オプション) デモグラフィックデータ用のテンプレート変数を提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を命名します。&lt;/li&gt;&lt;li&gt;例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;(オプション) デモグラフィックデータで参照するテンプレートを提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは、サポートされるフィールドに名前で二重中括弧を使用して挿入されます。&lt;/li&gt;&lt;li&gt;例：`{{SomeTemplateName}}`。&lt;/li&gt;&lt;/ul&gt; |

### アクション - Update Subscriber (Queued)

##### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[Batched Actions]()を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数：10
* 最古のリクエストからの最大時間：1分
* リクエストの最大サイズ：1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Country code|  &lt;ul&gt;&lt;li&gt;登録者の国コード。&lt;/li&gt;&lt;/ul&gt; |
|Desired format|  &lt;ul&gt;&lt;li&gt;登録者が希望するフォーマット。&lt;/li&gt;&lt;/ul&gt; |
|Email address|  &lt;ul&gt;&lt;li&gt;(必須) 登録者のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|Name|  &lt;ul&gt;&lt;li&gt;登録者の名前。&lt;/li&gt;&lt;/ul&gt; |
|Password|  &lt;ul&gt;&lt;li&gt;登録者のパスワード。&lt;/li&gt;&lt;/ul&gt; |
|Phone number|  &lt;ul&gt;&lt;li&gt;登録者の電話番号。&lt;/li&gt;&lt;/ul&gt; |
|User ID|  &lt;ul&gt;&lt;li&gt;登録者のID。&lt;/li&gt;&lt;li&gt;詳細については、[Update Subscribers](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Demographic Data|  &lt;ul&gt;&lt;li&gt;登録者のデモグラフィックデータフィールドのリスト。&lt;/li&gt;&lt;li&gt;データフィールドのキーと可能な値は、アカウント管理コンソールで定義されています。&lt;/li&gt;&lt;/ul&gt; |
|Template Variables|  &lt;ul&gt;&lt;li&gt;(オプション) デモグラフィックデータ用のテンプレート変数を提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を命名します。&lt;/li&gt;&lt;li&gt;例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;(オプション) デモグラフィックデータで参照するテンプレートを提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは、サポートされるフィールドに名前で二重中括弧を使用して挿入されます。&lt;/li&gt;&lt;li&gt;例：`{{SomeTemplateName}}`。&lt;/li&gt;&lt;/ul&gt; |

### アクション - Add Subscriber to Mailing List

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Mailing List|  &lt;ul&gt;&lt;li&gt;追加するメーリングリストを選択するか、リストIDを直接提供します。&lt;/li&gt;&lt;li&gt;詳細については、[SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber)を参照してください。&lt;/li&gt;&lt;li&gt;メーリングリストIDを知っている場合は、カスタム値として入力できます。&lt;/li&gt;&lt;/ul&gt; |
|Subscriber&#39;s Email|  &lt;ul&gt;&lt;li&gt;(必須) 登録者のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|Subscriber&#39;s ID|  &lt;ul&gt;&lt;li&gt;登録者のID。&lt;/li&gt;&lt;li&gt;詳細については、[Update Subscribers](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)を参照してください。&lt;/li&gt;&lt;/ul&gt; |

### アクション - Remove Subscriber from Mailing List

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Mailing List|  &lt;ul&gt;&lt;li&gt;追加するメーリングリストを選択するか、リストIDを直接提供します。&lt;/li&gt;&lt;li&gt;詳細については、[SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber)を参照してください。&lt;/li&gt;&lt;li&gt;メーリングリストIDを知っている場合は、カスタム値として入力できます。&lt;/li&gt;&lt;/ul&gt; |
|Subscriber&#39;s Email|  &lt;ul&gt;&lt;li&gt;(必須) 登録者のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|Subscriber&#39;s Id|  &lt;ul&gt;&lt;li&gt;登録者のID。&lt;/li&gt;&lt;li&gt;詳細については、[Update Subscribers](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)を参照してください。&lt;/li&gt;&lt;/ul&gt; |

### アクション - Delete Subscriber (Queued)

##### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[Batched Actions]()を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数：10
* 最古のリクエストからの最大時間：1分
* リクエストの最大サイズ：1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|Subscriber&#39;s Email|  &lt;ul&gt;&lt;li&gt;(必須) 登録者のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |

### アクション - Send Transactional Email


#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|トランザクショナルプロジェクト|  &lt;ul&gt;&lt;li&gt;トランザクショナルプロジェクトを選択します。&lt;/li&gt;&lt;li&gt;プロジェクトのID。&lt;/li&gt;&lt;li&gt;詳細については、[トランザクショナルメールの送信](http://se.apidoc.anpdm.com/Browse/Method/TransactionalService/SendTransactionalEmail)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|非アクティブプロジェクトの無効化|  &lt;ul&gt;&lt;li&gt;プロジェクトが非アクティブの場合に送信を許可するかどうかを示す真偽値&lt;/li&gt;&lt;li&gt;デフォルト値は **true** です。&lt;/li&gt;&lt;/ul&gt; |
|国コード|  &lt;ul&gt;&lt;li&gt;加入者の国コード。&lt;/li&gt;&lt;/ul&gt; |
|HTML用のデモグラフィックデータ|  &lt;ul&gt;&lt;li&gt;加入者のデモグラフィックデータフィールドのリスト。&lt;/li&gt;&lt;li&gt;データフィールドのキーと可能な値は、APSISアカウント管理コンソールで定義されています。&lt;/li&gt;&lt;/ul&gt; |
|希望の形式|  &lt;ul&gt;&lt;li&gt;加入者が希望する形式。&lt;/li&gt;&lt;/ul&gt; |
|メールアドレス|  &lt;ul&gt;&lt;li&gt;(必須) 加入者のメールアドレス&lt;/li&gt;&lt;/ul&gt; |
|外部ID|  &lt;ul&gt;&lt;li&gt;加入者の外部ID。&lt;/li&gt;&lt;/ul&gt; |
|名前|  &lt;ul&gt;&lt;li&gt;加入者の名前。&lt;/li&gt;&lt;/ul&gt; |
|電話番号|  &lt;ul&gt;&lt;li&gt;加入者の電話番号。&lt;/li&gt;&lt;/ul&gt; |
|送信日|  &lt;ul&gt;&lt;li&gt;送信日。&lt;/li&gt;&lt;/ul&gt; |
|送信タイプ|  &lt;ul&gt;&lt;li&gt;可能な値:  &lt;ul&gt;&lt;li&gt;**m** - マーケティング&lt;/li&gt;&lt;li&gt;**t** - トランザクショナル（デフォルト）&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|デモグラフィックデータ|  &lt;ul&gt;&lt;li&gt;加入者のデモグラフィックデータフィールドのリスト。&lt;/li&gt;&lt;li&gt;データフィールドのキーと可能な値は、APSISアカウント管理コンソールで定義されています。&lt;/li&gt;&lt;/ul&gt; |
|テンプレート変数|  &lt;ul&gt;&lt;li&gt;(オプション) デモグラフィックデータ用のテンプレート変数を提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を名付けます。&lt;/li&gt;&lt;li&gt;例: `items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt; |
|テンプレート|  &lt;ul&gt;&lt;li&gt;(オプション) デモグラフィックデータで参照されるテンプレートを提供します。&lt;/li&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で指定され、サポートされるフィールドに二重中括弧で注入されます。&lt;/li&gt;&lt;li&gt;例: `{{SomeTemplateName}}`。&lt;/li&gt;&lt;/ul&gt; |