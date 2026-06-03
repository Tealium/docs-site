---
title: FullStory APIコネクタ構成ガイド
description: この記事では、FullStory APIコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/fullstory-user-api-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：FullStory API
* APIバージョン：v1.0
* APIエンドポイント：`https://api.fullstory.com/users/v1/`
* ドキュメンテーション：[FullStory API](https://developer.fullstory.com/server/v1/users/introduction/)

## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| サーバーイベント | ✓ | ✓ |
| ユーザープロパティの構成 | ✓ | ✓ |
| ユーザーの削除 | ✓ | ✓ |

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタについて]()を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**
  * 必須。HTTP APIは、FullStoryアプリから生成できるAPIキーを必要とします。APIキーは、AdminまたはArchitectレベルの権限を持つ必要があります。詳細については、&lt;a target=&#34;_blank&#34; href=&#34;https://help.fullstory.com/hc/en-us/articles/360020624834&#34;&gt;APIキーはどこで見つけることができますか&lt;/a&gt;を参照してください。

## アクション

**アクション名**を入力し、ドロップダウンメニューから**アクションタイプ**を選択します。

以下のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### サーバーイベント

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| UID | 必須。ユーザーに与えられた一意のユーザーIDで、`FS.identify`ブラウザAPI関数を通じて渡されます。 |
| イベント名 | 必須。カスタムイベントの一意の名前。 |
| タイムスタンプ | イベントが発生した時間を&lt;a target=&#34;_blank&#34; href=&#34;https://en.wikipedia.org/wiki/ISO_8601&#34;&gt;ISO 8601形式&lt;/a&gt;で表現します。提供されていない場合、現在のFullStoryサーバー時間が使用されます。 |
| 最近のセッションを使用 | カスタムイベントがユーザーの最近のセッションに関連付けられるべき場合は`true`に構成します。最近のセッションは、過去30分以内に活動があった必要があります。`session_url`または`device_session`が定義されている場合は使用できません。 |
| ID |  |
| 優先度 |  |
| ソース |  |
| タイトル |  |

### ユーザープロパティの構成

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| UID | 必須。ユーザーに与えられた一意のユーザーIDで、`FS.identify`ブラウザAPI関数を通じて渡されます。 |
| ボディ | ユーザーに関連付けられたカスタムプロパティ。クライアントは任意の訪問属性をマップすることが許可されるべきです。プロパティ名は、&lt;a target=&#34;_blank&#34; href=&#34;https://help.fullstory.com/hc/en-us/articles/4446290296599-Setting-custom-API-properties&#34;&gt;ここ&lt;/a&gt;で文書化されているカスタムフィールド形式に従う必要があります。&lt;br&gt; |

### ユーザーの削除

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| UID | 必須。ユーザーに与えられた一意のユーザーIDで、`FS.identify`ブラウザAPI関数を通じて渡されます。 |

