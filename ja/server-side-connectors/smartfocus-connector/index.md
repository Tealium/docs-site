---
title: SmartFocusコネクタ構成ガイド
description: この記事では、SmartFocusコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/smartfocus-connector/
---
## サポートされているアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|メンバーの作成または更新| ✓| ✗|
|メンバーの退会| ✓| ✗|
|メンバーの再登録| ✓| ✗|
|トランザクションメールの送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、SmartFocusコネクタを追加します。コネクタの追加方法については、[コネクタ概要](/ja/server-side/connectors/manage/)の記事を参照してください。

以下の構成項目に値を入力します：

* **タイトル**
  * コネクタインスタンスのタイトル。

* **APIログイン**
  * SmartFocusアカウントのユーザー名。  
専用のAPIログインが必要です。もし持っていない場合は、SmartFocusのアカウントマネージャーに連絡してください。

* **APIパスワード**
  * SmartFocusアカウントのパスワード。

* **APIキー**
  * SmartFocusアカウントのAPIキー。

* **サーバー**
  * SmartFocusアカウントに関連付けられたサーバー。

* **SmartFocusメンバー機能を有効にする**  
メンバーモジュールは、SmartFocusアカウントで有効にする必要があります。そうしないと、接続を試みたときに接続が失敗します。  
これはアカウントレベルの機能で、一度有効にすると、すべてのAPIユーザーに適用され、APIを通じてメンバーのプロフィールにアクセスする方法を提供します。これにより、メンバーテーブルに挿入、更新、取得することができます。メンバーテーブルはSmartFocus DataCenterに保存されている単一のテーブルで、受信者のプロフィール情報（メールアドレス、名前、姓、アカウントのライフタイム中に定義された任意の列など）をすべて含んでいます。

* **ノート**
  * このコネクタに関する追加のノート。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - メンバーの作成または更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|更新タイプ|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;適用可能な更新戦略を選択します。  &lt;ul&gt;&lt;li&gt;**作成のみ** ルックアップなしで新しいメンバーを作成します。&lt;/li&gt;&lt;li&gt;**更新のみ** 既存のメンバーを更新します。&lt;/li&gt;&lt;li&gt;**作成または更新** 既存のメンバーが存在する場合は更新し、存在しない場合は新しいメンバーを作成します。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |

### アクション: メンバーの再登録

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メンバーUID |  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;アクションを実行するメンバーを識別します。&lt;/li&gt;&lt;li&gt;メール、携帯電話番号、またはメンバーIDのみが可能です。&lt;/li&gt;&lt;/ul&gt; |

### アクション: メンバーの退会

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メンバーUID|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;アクションを実行するメンバーを識別します。&lt;/li&gt;&lt;/ul&gt; |

### アクション - トランザクションメッセージの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|メッセージテンプレート|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;メンバーに送信するSmartFocusのトランザクションメッセージテンプレート。&lt;/li&gt;&lt;li&gt;SmartFocus APIからのオプションの読み込みには時間がかかる場合があります。&lt;/li&gt;&lt;li&gt;送信するテンプレートがリストにない場合は、カスタム値を&lt;code&gt;UniqueRandomTag&amp;#124;SecurityTag&lt;/code&gt;として構成します。&lt;/li&gt;&lt;/ul&gt; |
|メンバーメール|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;メッセージを送信したい受信者のメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|送信予定日|  &lt;ul&gt;&lt;li&gt;メッセージを送信する予定の日付。&lt;/li&gt;&lt;li&gt;デフォルトは現在の日付と時間。&lt;/li&gt;&lt;li&gt;日付が未来の場合、その日付/時間にシステムが送信します。&lt;/li&gt;&lt;li&gt;日付が過去の場合、メッセージはすぐに送信されます。&lt;/li&gt;&lt;li&gt;日付属性はSmartFocusの期待する形式`yyyy-MM-dd HH:mm:ss`に変換されます。&lt;/li&gt;&lt;/ul&gt; |
|同期タイプ|  &lt;ul&gt;&lt;li&gt;トランザクションメッセージングプラットフォームとSmartFocusメンバーテーブル間の各SendRequestに対して実行する同期のタイプ。&lt;/li&gt;&lt;li&gt;デフォルト値は`Nothing`です。  &lt;ul&gt;&lt;li&gt;**Nothing** メンバーテーブルは同期されません。&lt;/li&gt;&lt;li&gt;**Insert** 新しいプロフィールとそれに関連するすべてのメンバーコンテンツデータがメンバーテーブルに挿入されます。&lt;/li&gt;&lt;li&gt;**Update** プロフィールとそれに関連するすべてのメンバーコンテンツデータがメンバーテーブルで更新されます。&lt;/li&gt;&lt;li&gt;**Insert or Update** システムはメンバーテーブルのプロフィールを更新しようとします。更新に失敗した場合、関連するメンバーコンテンツデータとともにプロフィールをメンバーテーブルに挿入しようとします。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|同期UIDキー|  &lt;ul&gt;&lt;li&gt;同期がONのときにメンバーテーブルと一致するための列の名前。&lt;/li&gt;&lt;li&gt;同じ名前を持つDYNパラメータと一致し、関連する値を取得します。&lt;/li&gt;&lt;/ul&gt; |

## ベンダー文書

* [SmartFocus APIヘルプ](https://help-developer.smartfocus.com/Content/Home.htm?tocpath=_____1)
* [SmartFocusデータ個別更新](https://help-developer.smartfocus.com/#DATA_INDIVIDUAL_UPDATE_REST/Overview_of_the_Data_Individual_Update_API_-_REST.htm%3FTocPath%3DData%2520Individual%2520Update%2520-%2520REST%7C_____0)
* [SmartFocusトランザクションメッセージングトリガー](https://help-developer.smartfocus.com/#NMP_TRIGGER/sendObject.htm)
