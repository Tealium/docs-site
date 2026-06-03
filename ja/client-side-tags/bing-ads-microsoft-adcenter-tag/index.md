---
title: Bing Ads - Microsoft adCenter タグの構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでBing Ads - Microsoft adCenterタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/bing-ads-microsoft-adcenter-tag/
---
Bing Adsはこのタグを廃止し、[Bing Ads Universal Event Tracking Tag](/ja/client-side-tags/microsoft-advertising-universal-event-tracking-uet-tag/)に置き換えることを推奨しています。

## タグのヒント

* アナリティクスタグは、追加の変数をマッピングすることを可能にします（`actionid`、`revenue`、`nonadvertisingcost`、`taxcost`、`shippingcost`）
* 以下の変数の一つ以上にカンマ区切りのリストを使用して、複数のトラッキングリクエストを送信します（iframeタグのみ）：
  * `siteid`
  * `actionid`
  * `domainId`
  * `cp`

## タグの構成

まず、タグマーケットプレイスに移動し、Bing Ads - Microsoft adCenterタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **タグ**：確信がない場合はデフォルト（スクリプト）を使用します。
* **タイプ**：コンバージョンタイプを使用すると`cp`値が追加されますが、収益は送信されません。
* **サイトID**：サイトIDは`flex.msn.com/mstag/site/`に続く長い文字列です（例：`d2c3d50f-6f6a-3f2c-a303-6f032aece46c`）
* **アクションID**：デフォルトのアクションID。マッピングを通じて上書き可能です。
* **ドメインID**：デフォルトのドメインID。マッピングを通じて上書き可能です。
* **CP**：コンバージョンタグのみに使用されます（デフォルトの場合は`5050`に構成します。）
* **収益**：アナリティクスタグのみ。空白のままにすると、自動的に`_csubtotal`値が送信されます。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは以下の通りです：

### スタンダード

| 変数                  | 説明 |
|:---------------------|:------------|
| アクションID            |             |
| 収益                  |             |
| 非広告コスト |             |
| 税金コスト             |             |
| 送料                |             |
| サイトID              |             |
| ドメインID            |             |
| cp                   |             |

