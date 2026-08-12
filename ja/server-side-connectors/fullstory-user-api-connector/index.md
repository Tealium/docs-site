---
title: FullStory APIコネクタ構成ガイド
description: FullStoryでユーザーを作成、更新、または削除するためのFullStory APIコネクタを構成します。
url: https://docs.tealium.com/ja/server-side-connectors/fullstory-user-api-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：FullStory API
* APIバージョン：v2
* APIエンドポイント：`https://api.fullstory.com/v2/users`
* ドキュメント：[FullStory API](https://developer.fullstory.com/server/getting-started/)

## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| ユーザーの作成または更新 | ✓ | ✓ |
| ユーザーの削除 | ✓ | ✓ |

## 構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**
  * （必須）HTTP APIには、FullStoryアプリから生成できるAPIキーが必要です。APIキーはAdminまたはArchitectレベルの権限を持っている必要があります。詳細については、[FullStory: 私のAPIキーはどこで見つけることができますか](https://help.fullstory.com/hc/en-us/articles/360020624834)を参照してください。

## アクション

### ユーザーの作成または更新

#### パラメータ

必要なパラメータ：

| **パラメータ** | **説明** |
| --- | --- |
| UID | ユーザーに与えた一意のID。[FS.identify](https://developer.fullstory.com/identify)ブラウザAPI関数を通じて渡されるID。 |
| 表示名 | FullStoryでユーザーに表示するための人間に優しい名前。 |
| メール | ユーザーのメールアドレス。 |
| プロパティ | ユーザーに関連付けられたカスタムプロパティ。訪問属性を任意にマッピングできます。値はそのネイティブタイプで送信されます。コネクタはマッピングされた属性からFullStoryプロパティタイプを推測します。詳細については、[FullStory: カスタムプロパティ](https://developer.fullstory.com/server/custom-properties/)を参照してください。 |

### ユーザーの削除

#### パラメータ

必要なパラメータ：

| **パラメータ** | **説明** |
| --- | --- |
| UID | ユーザーに与えた一意のID。[FS.identify](https://developer.fullstory.com/identify)ブラウザAPI関数を通じて渡されるID。 |