---
title: Userlistコネクタ構成ガイド
description: この記事では、Userlistコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/userlist-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ユーザーデータの追跡| ✓| ✓|
|イベントの追跡| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **Push APIキー**
  * Userlistにデータを送信するためには、まずPush APIキーを取得する必要があります。これは、Push APIへのリクエストを認証し、データをアカウントに接続するために使用されます。
  * このPush APIキーは安全に保管してください。
  * 詳細については、[システムにユーザーデータを取り込む](https://docs.userlist.io/article/15-integration-guide)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ユーザーデータの追跡

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|識別子|  &lt;ul&gt;&lt;li&gt;このユーザーの一意の識別子。&lt;/li&gt;&lt;li&gt;これは、データベースのユーザーの主キー、生成された追跡識別子、またはそのメールアドレスのいずれかです。&lt;/li&gt;&lt;li&gt;詳細については、[システムにユーザーデータを取り込む統合ガイド](https://docs.userlist.io/article/15-integration-guide)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|メール|  &lt;ul&gt;&lt;li&gt;このユーザーにメッセージを送信するために使用されるメールアドレス。&lt;/li&gt;&lt;/ul&gt; |
|登録日時|  &lt;ul&gt;&lt;li&gt;ユーザーが登録した時間、ISO 8601を使用してフォーマット。&lt;/li&gt;&lt;li&gt;構成されていない場合、Userlistは現在の時間を使用します。&lt;/li&gt;&lt;/ul&gt; |
|最終訪問日時|  &lt;ul&gt;&lt;li&gt;ユーザーが最後にアプリケーション内で見られた時間。&lt;/li&gt;&lt;li&gt;ISO 8601を使用してフォーマット。&lt;/li&gt;&lt;li&gt;構成されていない場合、Userlistは現在の時間を使用します。&lt;/li&gt;&lt;li&gt;このユーザーに対するイベントが発生するたびに、Userlistはこのプロパティを更新します。&lt;/li&gt;&lt;/ul&gt; |
|プロパティ|  &lt;ul&gt;&lt;li&gt;ユーザーをさらに説明するカスタムプロパティ。&lt;/li&gt;&lt;li&gt;ここに保存する内容は完全にあなた次第です。&lt;/li&gt;&lt;li&gt;オブジェクトのキーは`snake_case`に正規化されます。&lt;/li&gt;&lt;li&gt;構成されている場合、`name`、または`first_name`と`last_name`を使用してUserlist内でユーザーを表現します。&lt;/li&gt;&lt;/ul&gt; |

### アクション - イベントの追跡

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|名前|  &lt;ul&gt;&lt;li&gt;トリガーされるイベントの名前。&lt;/li&gt;&lt;li&gt;名前は`snake_case`に正規化されます。&lt;/li&gt;&lt;li&gt;詳細については、[システムにユーザーデータを取り込む](https://docs.userlist.io/article/15-integration-guide)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|ユーザー|  &lt;ul&gt;&lt;li&gt;識別子がシステムに認識されていない場合、新しいユーザーを作成します。&lt;/li&gt;&lt;li&gt;ユーザーが既に存在する場合は、与えられた情報を使用して更新します。&lt;/li&gt;&lt;/ul&gt; |
|発生日時|  &lt;ul&gt;&lt;li&gt;イベントが発生した時間。&lt;/li&gt;&lt;li&gt;ISO 8601を使用してフォーマット。&lt;/li&gt;&lt;li&gt;入力を提供しない場合、システムは現在の時間を使用します。&lt;/li&gt;&lt;/ul&gt; |
|プロパティ|  &lt;ul&gt;&lt;li&gt;イベントをさらに説明するカスタムプロパティ。&lt;/li&gt;&lt;li&gt;ここに保存する内容は完全にあなた次第です。&lt;/li&gt;&lt;li&gt;オブジェクトのキーは`snake_case`に正規化されます。&lt;/li&gt;&lt;/ul&gt; |
