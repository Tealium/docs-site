---
title: Xユニバーサルウェブサイトタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでXユニバーサルウェブサイトタグ（UWT）を構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/twitter-universal-website-tag/
---
このタグは現在非推奨です。現在のタグについては、[X Pixelタグ]()を参照してください。

## 必要条件

* X広告アカウント
* X UWTピクセルID
* 完全に構成された[E-Commerce拡張機能]()

## サポートされるバージョン

* v1.0.0

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。タグを追加する一般的な手順については、[タグ概要]()の記事を読んでください。

タグを追加する際には、以下の構成を構成します：

1. **タイトル**: タグを識別するためのユニークな名前を入力します。複数のインスタンスを追加する場合は、この構成が重要です。
1. **XピクセルID**: ユニバーサルウェブサイトタグのコードスニペットからピクセルID値を入力します。例：`twq(&#39;init&#39;,&#39;1a2b3&#39;);`

タグ構成を動的に構成したい場合は、データマッピングを使用してください（下記参照）。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール]()のドキュメントを参照してください。

### データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする手順については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

Xユニバーサルウェブサイトタグの宛先変数は、そのデータマッピングタブに組み込まれています。利用可能なカテゴリは以下の通りです：

### 標準

|宛先名| 説明|
|---| ---|
|XピクセルID| あなたのX広告アカウントに関連付けられたユニバーサルウェブサイトタグのピクセルID、例：&#34;1a2b3&#34; |
|イベント値| このイベントを実行するユーザーの広告主にとっての価値、例：&#34;19.99&#34; |
|アイテム数| このオンサイトイベントに関連するアイテムの数、例：&#34;3&#34; |
|コンテンツタイプ| 値は「product」または「product_group」のいずれかであるべきです。&lt;ul&gt;&lt;li&gt;製品IDが渡される場合、content_typeは「product」であるべきです。&lt;/li&gt;&lt;li&gt;製品グループIDが渡される場合、content_typeは「product_group」であるべきです。&lt;/li&gt;&lt;/ul&gt; |
|イベントステータス| オンサイト登録イベントのステータス、例：&#34;submitted&#34; |

### E-Commerce

XユニバーサルウェブサイトタグはE-Commerceを有効にしているため、デフォルトの[E-Commerce拡張機能]()のマッピングを自動的に使用します。以下の場合を除き、このカテゴリでの手動マッピングは通常必要ありません：

* 拡張機能のマッピングを上書きしたい場合。
* 拡張機能で提供されていないE-Commerce変数が必要な場合。

|宛先名| 説明| E-Commerce拡張変数|
|---| ---| ---|
|注文ID| 購入、サインアップ、またはダウンロードイベントに関連する広告主の注文ID| `corder`|
|注文合計| 購入イベントの場合、このE-Commerce拡張パラメータはイベント値宛先に渡されます| `ctotal`|
|通貨| イベント値属性の通貨（ISO 4217標準）| `ccurrency`|
|製品IDリスト| イベントに関連する製品ID| `cprod`|
|製品名リスト| イベントに関連する製品名| `cprodname`|
|カテゴリリスト| 製品のカテゴリ| `ccat`|
|数量リスト| 購入およびダウンロードイベントの場合、この配列の値（E-Commerce拡張機能から）は合計され、アイテム数の宛先に渡されます| `cquan`|

### **イベントトリガー（および必要なパラメータ）**

特定のイベントをページ上でトリガーするためにこれらの宛先にマッピングします。イベントトリガーの方法は以下の通りです：

1. **トリガー**リストからイベントを選択します。
1. **マッピングされた値**フィールドに、この宛先にマッピングしている変数の値を入力します。マッピングされた変数の値が**マッピングされた値**フィールドに入力した値と一致すると、ページ上でイベントがトリガーされます。
1. さらにイベントをマッピングするには、**&#43;Add**をクリックして手順#1と#2を繰り返します。

PageViewイベントは、各ページのロード時に自動的にトリガーされます。

いくつかのイベントは特定のパラメータを必要とし、それらのパラメータが欠けているか空白の場合にはトリガーされません。以下の表で、アスタリスクでマークされたパラメータは、明示的にマッピングされていない限りE-Commerce拡張機能によって入力されます。

|Xイベント変数| 説明| 必須| オプション|
|---| ---| ---| ---|
|PageView（デフォルト）| より具体的なイベントタイプのないページのための一般的なキャッチオールイベントタイプ。| なし|  &lt;ul&gt;&lt;li&gt;event_value&lt;/li&gt;&lt;li&gt;currency\*&lt;/li&gt;&lt;li&gt;num_items&lt;/li&gt;&lt;/ul&gt; |
|Purchase|  購入が行われたり、チェックアウトフローが完了した場合。 |  &lt;ul&gt;&lt;li&gt;content_ids\*&lt;/li&gt;&lt;li&gt;content_type&lt;/li&gt;&lt;li&gt;event_value\*&lt;/li&gt;&lt;li&gt;currency\*&lt;/li&gt;&lt;/ul&gt; |  &lt;ul&gt;&lt;li&gt;content_name\*&lt;/li&gt;&lt;li&gt;num_items\*&lt;/li&gt;&lt;li&gt;order_id\*&lt;/li&gt;&lt;/ul&gt; |
|Signup| ユーザーのサインアップが完了した場合。| なし|  &lt;ul&gt;&lt;li&gt;content_name\*&lt;/li&gt;&lt;li&gt;content_category\*&lt;/li&gt;&lt;li&gt;event_value&lt;/li&gt;&lt;li&gt;currency\*&lt;/li&gt;&lt;li&gt;order_id\*&lt;/li&gt;&lt;/ul&gt; |
|Download|  ダウンロードリンクがクリックされた場合。例：ソフトウェアのダウンロード、ドキュメントのダウンロード | なし|  &lt;ul&gt;&lt;li&gt;content_ids\*&lt;/li&gt;&lt;li&gt;content_name\*&lt;/li&gt;&lt;li&gt;content_category\*&lt;/li&gt;&lt;li&gt;event_value&lt;/li&gt;&lt;li&gt;currency\*&lt;/li&gt;&lt;li&gt;num_items\*&lt;/li&gt;&lt;li&gt;order_id\*&lt;/li&gt;&lt;/ul&gt; |

## ベンダー文書

* [ウェブサイトのコンバージョントラッキング](https://business.x.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites)
