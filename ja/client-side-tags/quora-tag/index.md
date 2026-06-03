---
title: Quoraタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでQuoraタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/quora-tag/
---
## タグのヒント

* マッピングを使用して：
  * 標準構成値を上書きする
  * イベントトリガーを構成する

## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Quoraタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* `pixel_id`
ピクセルを一意に識別するQuoraが提供する英数字の文字列

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数   | 説明                      |
|:-----------|:---------------------------------|
| `pixel_id` | &lt;ul&gt;&lt;li&gt;Quora Pixel ID&lt;/li&gt;&lt;/ul&gt; |

### イベント

| 変数               | 説明                                      |
|:-----------------------|:-------------------------------------------------|
| `ViewContent`          | &lt;ul&gt;&lt;li&gt;ページビュー&lt;/li&gt;&lt;li&gt;コンテンツ表示&lt;/li&gt;&lt;/ul&gt; |
| `Generic`              | &lt;ul&gt;&lt;li&gt;一般&lt;/li&gt;&lt;/ul&gt;                        |
| `Purchase`             | &lt;ul&gt;&lt;li&gt;購入&lt;/li&gt;&lt;/ul&gt;                       |
| `GenerateLead`         | &lt;ul&gt;&lt;li&gt;リード生成&lt;/li&gt;&lt;/ul&gt;                  |
| `CompleteRegistration` | &lt;ul&gt;&lt;li&gt;登録完了&lt;/li&gt;&lt;/ul&gt;          |
| `AddPaymentInfo`       | &lt;ul&gt;&lt;li&gt;支払い情報追加&lt;/li&gt;&lt;/ul&gt;        |
| `AddToCart`            | &lt;ul&gt;&lt;li&gt;カートに追加&lt;/li&gt;&lt;/ul&gt;                    |
| `AddToWishlist`        | &lt;ul&gt;&lt;li&gt;ウィッシュリストに追加&lt;/li&gt;&lt;/ul&gt;               |
| `InitiateCheckout`     | &lt;ul&gt;&lt;li&gt;チェックアウト開始&lt;/li&gt;&lt;/ul&gt;              |
| `Search`               | &lt;ul&gt;&lt;li&gt;検索&lt;/li&gt;&lt;/ul&gt;                         |
| `Custom`               | &lt;ul&gt;&lt;li&gt;カスタム&lt;/li&gt;&lt;/ul&gt;                         |
