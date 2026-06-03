---
title: Pipedriveコネクタ構成ガイド
description: この記事では、Pipedriveコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/pipedrive-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|人物を作成する| ✓| ✗|
|人物を更新する| ✓| ✗|
|二人の人物を統合する| ✓| ✗|
|人物を削除する| ✓| ✗|

## 構成を構成する

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **サブドメイン**
  * あなたのPipedriveアカウントのサブドメイン。

* **APIトークン**
  * 手動で統合を行っている場合、APIトークンはすべてのリクエストのクエリ文字列の一部として提供する必要があります。これは`api_token`変数を使用します。
  * APIトークンは、Pipedriveアプリから手動で取得するか、Authorizationsのオブジェクトを取得することで取得できます。
  * 詳細については、[Pipedriveのドキュメンテーション](https://pipedrive.readme.io/docs/core-api-concepts-authentication)を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - 人物を作成する

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|名前|  &lt;ul&gt;&lt;li&gt;作成する人物の名前。&lt;/li&gt;&lt;li&gt;詳細については、[人物を追加する](https://developers.pipedrive.com/docs/api/v1/#!/Persons/post_persons)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|オーナーID|  &lt;ul&gt;&lt;li&gt;この人物のオーナーとしてマークされるユーザーのID。&lt;/li&gt;&lt;li&gt;省略した場合、認証されたユーザーIDが使用されます。&lt;/li&gt;&lt;/ul&gt; |
|組織ID| この人物が所属する組織のID。|
|メール| 人物のメールアドレス。|
|電話| 人物の電話番号。|
|表示先|  &lt;ul&gt;&lt;li&gt;人物の可視性。&lt;/li&gt;&lt;li&gt;省略した場合、可視性は認証されたユーザーのこのアイテムタイプのデフォルトの可視性構成に構成されます。&lt;/li&gt;&lt;/ul&gt; |
|追加時間|  &lt;ul&gt;&lt;li&gt;人物の作成日時を協定世界時（UTC）形式でオプションで構成します。&lt;/li&gt;&lt;li&gt;例：`YYYY-MM-DD HH:MM:SS`。&lt;/li&gt;&lt;li&gt;管理者ユーザーのAPIトークンが必要です。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 人物を更新する

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ID|  &lt;ul&gt;&lt;li&gt;人物のID。&lt;/li&gt;&lt;li&gt;詳細については、[人物を更新する](https://developers.pipedrive.com/docs/api/v1/#!/Persons/put_persons_id)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|名前| 作成する人物の名前。|
|オーナーID|  &lt;ul&gt;&lt;li&gt;この人物のオーナーとしてマークされるユーザーのID。&lt;/li&gt;&lt;li&gt;省略した場合、認証されたユーザーIDが使用されます。&lt;/li&gt;&lt;/ul&gt; |
|組織ID| この人物が所属する組織のID。|
|メール| 人物のメールアドレス。|
|電話| 人物の電話番号。|
|表示先|  &lt;ul&gt;&lt;li&gt;人物の可視性。&lt;/li&gt;&lt;li&gt;省略した場合、可視性は認証されたユーザーのこのアイテムタイプのデフォルトの可視性構成に構成されます。&lt;/li&gt;&lt;/ul&gt; |
|追加時間|  &lt;ul&gt;&lt;li&gt;人物の作成日時を協定世界時（UTC）形式でオプションで構成します。&lt;/li&gt;&lt;li&gt;例：`YYYY-MM-DD HH:MM:SS`&lt;/li&gt;&lt;li&gt;管理者ユーザーのAPIトークンが必要です。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 二人の人物を統合する

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ID|  &lt;ul&gt;&lt;li&gt;統合される人物のID。&lt;/li&gt;&lt;li&gt;詳細については、[二人の人物を統合する](https://developers.pipedrive.com/docs/api/v1/#!/Persons/put_persons_id_merge)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|統合先ID| 人物が統合される人物のID。|

### アクション - 人物を削除する

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ID|  &lt;ul&gt;&lt;li&gt;削除する人物のID。&lt;/li&gt;&lt;li&gt;詳細については、[人物を削除する](https://developers.pipedrive.com/docs/api/v1/#!/Persons/delete_persons_id)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
