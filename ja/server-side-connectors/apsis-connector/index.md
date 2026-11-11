---
title: APSISコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでAPSISコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/apsis-connector/
---
## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|購読者を作成してメーリングリストに追加（キュー処理）| ✓| ✗|
|購読者を更新（キュー処理）| ✓| ✗|
|購読者をメーリングリストに追加| ✓| ✗|
|購読者をメーリングリストから削除| ✓| ✗|
|購読者を削除（キュー処理）| ✓| ✗|
|トランザクションメールを送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の構成を構成します。

* **APIキー**
  * APIキーを取得するには、APSIS Proアカウントにログインし、**Account**セクションを選択します。
  * **API Keys**リンクを見つけ、クリックして新しいAPIキーを生成します。
  * 1つのアカウントに複数のAPIキーを構成できます。
  * APSIS Proの**Account Settings**セクションでキーを管理できます。
  * 詳細については、[APSIS：はじめに](http://se.apidoc.anpdm.com/Help/GettingStarted/Getting%20started)を参照してください。

## アクション構成：パラメータとオプション

**Continue**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション：購読者を作成してメーリングリストに追加（キュー処理）

##### バッチ制限

このアクションでは、ベンダーへの大量データ転送をサポートするために、バッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに保持されます。

* リクエストの最大数：10
* 最も古いリクエストからの最大経過時間：1分
* リクエストの最大サイズ：1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メーリングリスト|  <ul><li>購読者の追加先となるリストのID。</li><li>メーリングリストIDが分かっている場合は、カスタム値として入力できます。</li><li>購読者の追加先となるリストを選択するか、リストIDを直接指定します。</li><li>詳細については、[SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber)を参照してください。</li></ul> |
|作成モード|  <ul><li>購読者のアカウントがすでに存在し、このパラメータが「作成または更新」に構成されている場合、購読者のデータが更新されます。</li><li>ダブルオプトインで購読登録する場合、既存の購読者を更新することはできません。</li></ul> |
|国コード|  <ul><li>購読者の国コード。</li></ul> |
|希望する形式|  <ul><li>購読者が希望する形式。</li></ul> |
|メールアドレス|  <ul><li>（必須）購読者のメールアドレス。</li></ul> |
|外部ID|  <ul><li>購読者の外部ID。</li></ul> |
|名前|  <ul><li>購読者の名前。</li></ul> |
|パスワード|  <ul><li>購読者のパスワード。</li></ul> |
|電話番号|  <ul><li>購読者の電話番号。</li></ul> |
|デモグラフィックデータ|  <ul><li>購読者のデモグラフィックデータフィールドのリスト。</li><li>データフィールドのキーと指定可能な値は、APSISアカウント管理コンソールで定義されます。</li></ul> |
|テンプレート変数|  <ul><li>（任意）デモグラフィックデータ用のテンプレート変数を指定します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数には、ドット表記で名前を付けます。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。</li></ul> |
|テンプレート|  <ul><li>（任意）デモグラフィックデータで参照するテンプレートを指定します。</li><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、サポートされているフィールドに二重波括弧で囲んだ名前を使用して挿入されます。</li><li>例：`{{SomeTemplateName}}`。</li></ul> |

### アクション：購読者を更新（キュー処理）

##### バッチ制限

このアクションでは、ベンダーへの大量データ転送をサポートするために、バッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに保持されます。

* リクエストの最大数：10
* 最も古いリクエストからの最大経過時間：1分
* リクエストの最大サイズ：1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|国コード|  <ul><li>購読者の国コード。</li></ul> |
|希望する形式|  <ul><li>購読者が希望する形式。</li></ul> |
|メールアドレス|  <ul><li>（必須）購読者のメールアドレス</li></ul> |
|名前|  <ul><li>購読者の名前。</li></ul> |
|パスワード|  <ul><li>購読者のパスワード。</li></ul> |
|電話番号|  <ul><li>購読者の電話番号。</li></ul> |
|ユーザーID|  <ul><li>購読者のID。</li><li>詳細については、[購読者の更新](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)を参照してください。</li></ul> |
|デモグラフィックデータ|  <ul><li>購読者のデモグラフィックデータフィールドのリスト。</li><li>データフィールドのキーと指定可能な値は、アカウント管理コンソールで定義されます。</li></ul> |
|テンプレート変数|  <ul><li>（任意）デモグラフィックデータ用のテンプレート変数を指定します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数には、ドット表記で名前を付けます。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。</li></ul> |
|テンプレート|  <ul><li>（任意）デモグラフィックデータで参照するテンプレートを指定します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>テンプレートは、サポートされているフィールドに二重波括弧で囲んだ名前を使用して挿入されます。</li><li>例：`{{SomeTemplateName}}`。</li></ul> |

### アクション：購読者をメーリングリストに追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メーリングリスト|  <ul><li>購読者の追加先となるリストを選択するか、リストIDを直接指定します。</li><li>詳細については、[SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber)を参照してください。</li><li>メーリングリストIDが分かっている場合は、カスタム値として入力できます。</li></ul> |
|購読者のメールアドレス|  <ul><li>（必須）購読者のメールアドレス</li></ul> |
|購読者ID|  <ul><li>購読者のID。</li><li>詳細については、[購読者の更新](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)を参照してください。</li></ul> |

### アクション：購読者をメーリングリストから削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メーリングリスト|  <ul><li>購読者の追加先となるリストを選択するか、リストIDを直接指定します。</li><li>詳細については、[SubscriberService.CreateSubscriber](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/CreateSubscriber)を参照してください。</li><li>メーリングリストIDが分かっている場合は、カスタム値として入力できます。</li></ul> |
|購読者のメールアドレス|  <ul><li>（必須）購読者のメールアドレス</li></ul> |
|購読者ID|  <ul><li>購読者のID。</li><li>詳細については、[購読者の更新](http://se.apidoc.anpdm.com/Browse/Method/SubscriberService/UpdateSubscribers)を参照してください。</li></ul> |

### アクション：購読者を削除（キュー処理）

##### バッチ制限

このアクションでは、ベンダーへの大量データ転送をサポートするために、バッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに保持されます。

* リクエストの最大数：10
* 最も古いリクエストからの最大経過時間：1分
* リクエストの最大サイズ：1 MB

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|購読者のメールアドレス|  <ul><li>（必須）購読者のメールアドレス</li></ul> |

### アクション：トランザクションメールを送信
#### パラメーター

|**パラメーター**| **説明**|
|---| ---|
|トランザクショナルプロジェクト|  <ul><li>トランザクショナルプロジェクトを選択します。</li><li>プロジェクトのID。</li><li>詳細については、[トランザクショナルメールの送信](http://se.apidoc.anpdm.com/Browse/Method/TransactionalService/SendTransactionalEmail)を参照してください。</li></ul> |
|非アクティブなプロジェクトを無効化|  <ul><li>プロジェクトが非アクティブな場合に送信を許可するかどうかを示す真偽値。</li><li>デフォルト値は**true**です。</li></ul> |
|国コード|  <ul><li>購読者の国コード。</li></ul> |
|HTML用のデモグラフィックデータ|  <ul><li>購読者のデモグラフィックデータフィールドのリスト。</li><li>データフィールドのキーと指定可能な値は、APSISアカウント管理コンソールで定義されます。</li></ul> |
|希望する形式|  <ul><li>購読者が希望する形式。</li></ul> |
|メールアドレス|  <ul><li>（必須）購読者のメールアドレス。</li></ul> |
|外部ID|  <ul><li>購読者の外部ID。</li></ul> |
|名前|  <ul><li>購読者の名前。</li></ul> |
|電話番号|  <ul><li>購読者の電話番号。</li></ul> |
|送信日|  <ul><li>送信日。</li></ul> |
|送信タイプ|  <ul><li>指定可能な値：<ul><li>**m** - マーケティング</li><li>**t** - トランザクショナル（デフォルト）</li></ul> </li></ul> |
|デモグラフィックデータ|  <ul><li>購読者のデモグラフィックデータフィールドのリスト。</li><li>データフィールドのキーと指定可能な値は、APSISアカウント管理コンソールで定義されます。</li></ul> |
|テンプレート変数|  <ul><li>（任意）デモグラフィックデータ用のテンプレート変数を指定します。</li><li>>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数には、ドット表記で名前を付けます。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。</li></ul> |
|テンプレート|  <ul><li>（任意）デモグラフィックデータで参照するテンプレートを指定します。</li><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、サポートされているフィールドに二重波括弧を使用して名前で挿入されます。</li><li>例：`{{SomeTemplateName}}`。</li></ul> |