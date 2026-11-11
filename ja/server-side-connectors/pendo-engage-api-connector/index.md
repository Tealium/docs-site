---
title: Pendo Engage APIコネクタ構成ガイド
description: この記事では、Pendo Engage APIコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/pendo-engage-api-connector/
---
## API情報

このコネクタでは、次のベンダーAPIを使用します。

* API名：Pendo API
* APIバージョン：v1.0
* APIエンドポイント：`https://app.pendo.io/data/track`
* ドキュメント：[Pendo API](https://engageapi.pendo.io/?bash#e45be48e-e01f-4f0a-acaa-73ef6851c4ac)

## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| トラックイベントを送信 | ✗ | ✓ |

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の構成を構成します。

* **トラックイベントのシークレットキー**  
 （必須）トラックイベントのシークレットキーを取得するには、次の手順に従います。Pendoダッシュボードに移動し、**Settings**を選択します。メニューで**Subscription Settings**をクリックします。アプリを選択し、**App Details**で**Track Event Shared Secret**をコピーします。

## アクション構成 - パラメーターとオプション

アクションの名前を入力し、ドロップダウンリストからアクションタイプを選択します。

以下のセクションでは、各アクションのパラメーターとオプションを構成する方法について説明します。

### アクション - トラックイベントを送信

#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| Event | （必須）ユーザーが実行したアクションの名前。 |
| Visitor ID | （必須）訪問を識別する一意の文字列。 |
| Timestamp | （必須）イベントが発生した時刻（エポックからの経過時間をミリ秒単位で指定）。 |
| Account ID | （推奨）訪問が属するアカウントを識別する一意の文字列。 |
| Properties | イベントのプロパティを格納する自由形式のオブジェクト。 |
| IP | （推奨）現在のユーザーのIPアドレス。 |
| User Agent | （推奨）リクエストを行うデバイスのユーザーエージェント。 |
| URL | ブラウザーで現在表示されているページのURL。 |
| Title | ブラウザーで現在表示されているページのタイトル。 |