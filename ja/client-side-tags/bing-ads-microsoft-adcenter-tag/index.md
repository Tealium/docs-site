---
title: Bing Ads - Microsoft adCenterタグリファレンスガイド
description: この記事では、タグ管理アカウントでBing Ads - Microsoft adCenterタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/bing-ads-microsoft-adcenter-tag/
---


<blockquote>
Bing Adsではこのタグは非推奨となっており、[Bing Ads Universal Event Trackingタグ](https://docs.tealium.com/ja/client-side-tags/microsoft-advertising-universal-event-tracking-uet-tag/)への置き換えが推奨されています。
</blockquote>


## タグに関するヒント

* Analyticsタグでは、追加の変数をマッピングできます（`actionid`、`revenue`、`nonadvertisingcost`、`taxcost`、`shippingcost`）
* 複数のトラッキングリクエストを送信するには、次の1つ以上の変数でカンマ区切りのリストを使用します（iframeタグのみ）。
  * `siteid`
  * `actionid`
  * `domainId`
  * `cp`

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **タグ**：不明な場合は、デフォルト（スクリプト）を使用します。
* **タイプ**：コンバージョンタイプを使用すると`cp`値が追加されますが、収益は送信されません。
* **サイトID**：サイトIDは、`flex.msn.com/mstag/site/`の後に続く英数字の長い文字列です（例：`d2c3d50f-6f6a-3f2c-a303-6f032aece46c`）。
* **アクションID**：デフォルトのアクションIDです。マッピングで上書きできます。
* **ドメインID**：デフォルトのドメインIDです。マッピングで上書きできます。
* **CP**：コンバージョンタグでのみ使用します（デフォルトでは`5050`に構成します）。
* **収益**：Analyticsタグでのみ使用します。`_csubtotal`値を自動的に送信するには、空白のままにします。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数         | 説明 |
|:-------------|:-----|
| アクションID |      |
| 収益         |      |
| 広告外費用   |      |
| 税金         |      |
| 配送料       |      |
| サイトID     |      |
| ドメインID   |      |
| cp           |      |