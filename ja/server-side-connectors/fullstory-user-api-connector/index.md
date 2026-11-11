---
title: FullStory APIコネクタ構成ガイド
description: FullStoryでユーザーを作成、更新、または削除するためのFullStory APIコネクタを構成します。
url: https://docs.tealium.com/ja/server-side-connectors/fullstory-user-api-connector/
---
## API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：FullStory API
* APIバージョン：v2
* APIエンドポイント：`https://api.fullstory.com/v2/users`
* ドキュメント：[FullStory API](https://developer.fullstory.com/server/getting-started/)

## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| ユーザーの作成または更新 | ✓ | ✓ |
| ユーザーの削除 | ✓ | ✓ |

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を行います。

* **APIキー**
  * （必須）HTTP APIを使用するには、FullStoryアプリで生成できるAPIキーが必要です。APIキーには、AdminまたはArchitectレベルの権限が必要です。詳細については、[FullStory：APIキーの確認場所](https://help.fullstory.com/hc/en-us/articles/360020624834)を参照してください。

コネクタの構成後、**完了**をクリックします。

## アクション

### ユーザーの作成または更新

#### パラメータ

必須パラメータ：

| **パラメータ** | **説明** |
| --- | --- |
| UID | ユーザーに付与した一意のIDです。[FS.identify](https://developer.fullstory.com/identify) Browser API関数を介して渡されるIDです。 |
| 表示名 | FullStoryでユーザーについて表示する、人が理解しやすい名前です。 |
| メールアドレス | ユーザーのメールアドレスです。 |
| プロパティ | ユーザーに関連付けられたカスタムプロパティです。任意の訪問属性をマッピングできます。値はネイティブ型のまま送信されます。コネクタは、マッピングされた属性からFullStoryのプロパティ型を推測します。詳細については、[FullStory：カスタムプロパティ](https://developer.fullstory.com/server/custom-properties/)を参照してください。 |

### ユーザーの削除

#### パラメータ

必須パラメータ：

| **パラメータ** | **説明** |
| --- | --- |
| UID | ユーザーに付与した一意のIDです。[FS.identify](https://developer.fullstory.com/identify) Browser API関数を介して渡されるIDです。 |