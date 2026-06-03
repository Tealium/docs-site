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

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要]()の記事を参照してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ユーザープロパティを追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|App ID|  &lt;ul&gt;&lt;li&gt;プロジェクトの1つに対応する `app_id`。&lt;/li&gt;&lt;/ul&gt; |
|Identity|  &lt;ul&gt;&lt;li&gt;通常は既存のユーザーに対応するアイデンティティ。&lt;/li&gt;&lt;li&gt;そのようなアイデンティティが存在しない場合、そのアイデンティティを持つ新しいユーザーが作成されます。&lt;/li&gt;&lt;li&gt;255文字に制限。&lt;/li&gt;&lt;li&gt;詳細については、[Heap: ユーザープロパティを追加](https://developers.heap.io/docs/using-identify)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|User Properties|  &lt;ul&gt;&lt;li&gt;ユーザーに関連付けたいキーと値のプロパティを持つオブジェクト。&lt;/li&gt;&lt;li&gt;各キーとプロパティは、1024文字未満の数値または文字列でなければなりません。&lt;/li&gt;&lt;li&gt;詳細については、[Heap: ユーザープロパティを追加](https://developers.heap.io/docs/using-identify)を参照してください。&lt;/li&gt;&lt;/ul&gt; |

### アクション - トラック

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|App ID|  &lt;ul&gt;&lt;li&gt;プロジェクトの1つに対応する `app_id`。&lt;/li&gt;&lt;/ul&gt; |
|Identity|  &lt;ul&gt;&lt;li&gt;通常は既存のユーザーに対応するアイデンティティ。&lt;/li&gt;&lt;li&gt;そのようなアイデンティティが存在しない場合、そのアイデンティティを持つ新しいユーザーが作成されます。&lt;/li&gt;&lt;li&gt;255文字に制限。&lt;/li&gt;&lt;li&gt;詳細については、[Heap ドキュメンテーション](https://developers.heap.io/reference#track)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Event|  &lt;ul&gt;&lt;li&gt;サーバーサイドイベントの名前。&lt;/li&gt;&lt;li&gt;1024文字に制限。&lt;/li&gt;&lt;li&gt;詳細については、[Heap ドキュメンテーション](https://developers.heap.io/reference#track)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Properties|  &lt;ul&gt;&lt;li&gt;ユーザーに関連付けたいキーと値のプロパティを持つオブジェクト。&lt;/li&gt;&lt;li&gt;各キーとプロパティは、1024文字未満の数値または文字列でなければなりません。&lt;/li&gt;&lt;li&gt;詳細については、[Heap ドキュメンテーション](https://developers.heap.io/reference#track)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|Timestamp|  &lt;ul&gt;&lt;li&gt;ISO 8601またはUnixエポックミリ秒。&lt;/li&gt;&lt;li&gt;例：`2017-03-10T22:21:56&#43;00:00`&lt;/li&gt;&lt;li&gt;詳細については、[Heap ドキュメンテーション](https://developers.heap.io/reference#track)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
