---
title: Heapコネクタ構成ガイド
description: この記事では、Heapコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/heap-connector/
---
## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|ユーザープロパティを追加| ✓| ✗|
|トラッキング| ✗| ✓|

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - ユーザープロパティを追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アプリID|  <ul><li>いずれかのプロジェクトに対応する`app_id`。</li></ul> |
|ID|  <ul><li>通常は既存のユーザーに対応するID。</li><li>該当するIDが存在しない場合、そのIDを持つ新しいユーザーが作成されます。</li><li>255文字に制限されています。</li><li>詳細については、[Heap：ユーザープロパティを追加](https://developers.heap.io/docs/using-identify)を参照してください。</li></ul> |
|ユーザープロパティ|  <ul><li>ユーザーに関連付けるキーと値のプロパティを含むオブジェクト。</li><li>各キーとプロパティは、数値または1024文字未満の文字列である必要があります。</li><li>詳細については、[Heap：ユーザープロパティを追加](https://developers.heap.io/docs/using-identify)を参照してください。</li></ul> |

### アクション - トラッキング

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アプリID|  <ul><li>いずれかのプロジェクトに対応する`app_id`。</li></ul> |
|ID|  <ul><li>通常は既存のユーザーに対応するID。</li><li>該当するIDが存在しない場合、そのIDを持つ新しいユーザーが作成されます。</li><li>255文字に制限されています。</li><li>詳細については、[Heapドキュメント](https://developers.heap.io/reference#track)を参照してください。</li></ul> |
|イベント|  <ul><li>サーバーサイドイベントの名前。</li><li>1024文字に制限されています。</li><li>詳細については、[Heapドキュメント](https://developers.heap.io/reference#track)を参照してください。</li></ul> |
|プロパティ|  <ul><li>ユーザーに関連付けるキーと値のプロパティを含むオブジェクト。</li><li>各キーとプロパティは、数値または1024文字未満の文字列である必要があります。</li><li>詳細については、[Heapドキュメント](https://developers.heap.io/reference#track)を参照してください。</li></ul> |
|タイムスタンプ|  <ul><li>ISO 8601形式またはUnixエポックからのミリ秒。</li><li>例：`2017-03-10T22:21:56+00:00`</li><li>詳細については、[Heapドキュメント](https://developers.heap.io/reference#track)を参照してください。</li></ul> |