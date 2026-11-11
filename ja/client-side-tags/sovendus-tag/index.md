---
title: Sovendusタグ構成ガイド
description: この記事では、タグ管理アカウントでSovendusタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/sovendus-tag/
---
## タグに関するヒント

* 以下のEコマース拡張パラメータをサポートしています。
  * 注文ID（`_corder`）
  * 注文小計（`_csubtotal`）
  * 通貨（`_ccurrency`）
  * プロモーションコード（`_cpromo`）
  * 顧客の郵便番号（`_czip`）

### タグの構成

タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を行います。

* **トラフィックソース番号**
  * Sovendusがシステム内でショップを割り当てられるようにします。

* **トラフィックメディア番号**
  * 複数のトラフィックメディアを使用している場合は、ここに有効なトラフィックメディアを入力します。

* **iframeコンテナID**
  * 生成されたiframeをページ上のどの位置に実装するかを指定します。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### iframe構成

| 変数                                                      | 説明                    |
|:----------------------------------------------------------|:------------------------|
| トラフィックソース番号                                    | (`trafficSourceNumber`) |
| トラフィックメディア番号                                  | (`trafficMediumNumber`) |
| iframeコンテナID                                          | (`iframeContainerId`)   |
| セッションID                                              | (`sessionId`)           |
| タイムスタンプ                                            | (`timestamp`)           |
| 注文ID（`orderId`）（`_corder`を上書き）                  | [文字列]                |
| 注文金額（`orderValue`）（`_csubtotal`を上書き）          | [文字列]                |
| 注文通貨（`orderCurrency`）（`_ccurrency`を上書き）       | [文字列]                |
| 使用済みクーポンコード（`usedCouponCode`）（`_cpromo`を上書き） | [文字列]          |

### 消費者データ

| 変数                                                     | 説明                   |
|:---------------------------------------------------------|:-----------------------|
| 消費者の敬称                                             | (`consumerSalutation`) |
| 消費者の名                                               | (`consumerFirstName`)  |
| 消費者の姓                                               | (`consumerLastName`)   |
| 消費者のメールアドレス                                   | (`consumerEmail`)      |
| 消費者の郵便番号（`consumerZipcode`）（`_czip`を上書き） | [文字列]               |