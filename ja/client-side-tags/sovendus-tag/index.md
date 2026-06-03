---
title: Sovendusタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでSovendusタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/sovendus-tag/
---
## タグのヒント

* 以下のE-commerce拡張パラメータをサポートしています:
  * 注文ID (`_corder`)
  * 注文小計 (`_csubtotal`)
  * 通貨 (`_ccurrency`)
  * プロモーションコード (`_cpromo`)
  * 顧客の郵便番号 (`_czip`)

### タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Sovendusタグを追加します([タグの追加方法]()について詳しくはこちら)。

タグを追加したら、以下の構成を行います:

* **トラフィックソース番号**
  * Sovendusがあなたのショップをシステム内で割り当てるのを可能にします。

* **トラフィック媒体番号**
  * 複数のトラフィック媒体を使用している場合は、ここにアクティブなトラフィック媒体を入力します。

* **IframeコンテナID**
  * 生成されたiframeがページ上のどの位置に実装されるべきかを決定します。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです:

### Iframe構成

| 変数                                                      | 説明                   |
|:----------------------------------------------------------|:------------------------|
| トラフィックソース番号                                     | (`trafficSourceNumber`) |
| トラフィック媒体番号                                     | (`trafficMediumNumber`) |
| IframeコンテナID                                         | (`iframeContainerId`)   |
| セッションID                                              | (`sessionId`)           |
| タイムスタンプ                                           | (`timestamp`)           |
| 注文ID (`orderId`) ( `_corder`を上書き)                  | [文字列]                |
| 注文価格 (`orderValue`) ( `_csubtotal`を上書き)          | [文字列]                |
| 注文通貨 (`orderCurrency`) ( `_ccurrency`を上書き)       | [文字列]                |
| 使用クーポンコード (`usedCouponCode`) ( `_cpromo`を上書き) | [文字列]                |

### 消費者データ

| 変数                                                     | 説明                  |
|:---------------------------------------------------------|:-----------------------|
| 消費者敬称                                               | (`consumerSalutation`) |
| 消費者名                                                 | (`consumerFirstName`)  |
| 消費者姓                                                 | (`consumerLastName`)   |
| 消費者メール                                             | (`consumerEmail`)      |
| 消費者郵便番号 (`consumerZipcode`) ( `_czip`を上書き)    | [文字列]               |
