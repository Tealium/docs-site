---
title: Heap コネクタ構成ガイド
description: この記事では、ヒープコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/heap-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ユーザープロパティを追加| ✓| ✗|
|トラック| ✗| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ユーザープロパティを追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|App ID|  <ul><li>プロジェクトの1つに対応する `app_id`。</li></ul> |
|Identity|  <ul><li>通常は既存のユーザーに対応するアイデンティティ。</li><li>そのようなアイデンティティが存在しない場合、そのアイデンティティを持つ新しいユーザーが作成されます。</li><li>255文字に制限。</li><li>詳細については、[Heap: ユーザープロパティを追加](https://developers.heap.io/docs/using-identify)を参照してください。</li></ul> |
|User Properties|  <ul><li>ユーザーに関連付けたいキーと値のプロパティを持つオブジェクト。</li><li>各キーとプロパティは、1024文字未満の数値または文字列でなければなりません。</li><li>詳細については、[Heap: ユーザープロパティを追加](https://developers.heap.io/docs/using-identify)を参照してください。</li></ul> |

### アクション - トラック

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|App ID|  <ul><li>プロジェクトの1つに対応する `app_id`。</li></ul> |
|Identity|  <ul><li>通常は既存のユーザーに対応するアイデンティティ。</li><li>そのようなアイデンティティが存在しない場合、そのアイデンティティを持つ新しいユーザーが作成されます。</li><li>255文字に制限。</li><li>詳細については、[Heap ドキュメンテーション](https://developers.heap.io/reference#track)を参照してください。</li></ul> |
|Event|  <ul><li>サーバーサイドイベントの名前。</li><li>1024文字に制限。</li><li>詳細については、[Heap ドキュメンテーション](https://developers.heap.io/reference#track)を参照してください。</li></ul> |
|Properties|  <ul><li>ユーザーに関連付けたいキーと値のプロパティを持つオブジェクト。</li><li>各キーとプロパティは、1024文字未満の数値または文字列でなければなりません。</li><li>詳細については、[Heap ドキュメンテーション](https://developers.heap.io/reference#track)を参照してください。</li></ul> |
|Timestamp|  <ul><li>ISO 8601またはUnixエポックミリ秒。</li><li>例：`2017-03-10T22:21:56+00:00`</li><li>詳細については、[Heap ドキュメンテーション](https://developers.heap.io/reference#track)を参照してください。</li></ul> |
