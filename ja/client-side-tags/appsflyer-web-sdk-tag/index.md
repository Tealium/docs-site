---
title: AppsFlyer Web SDKタグ構成ガイド
description: この記事では、タグ管理アカウントでAppsFlyer Web SDKタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/appsflyer-web-sdk-tag/
---
People-Based Attribution向けWeb-S2S APIはWeb SDKを補完し、マーケターがWebサイト上で発生した、Web SDKの対象範囲外のイベントをレポートできるようにします。

## タグに関するヒント

* Web Dev Keyを取得するには、**AppsFlyer &gt; My Apps &gt; View brand bundles**に移動します。
* マッピングを使用すると、以下のことができます。
  * E-Commerce拡張機能の値を動的に上書きする
  * イベントトリガーを構成する

* 以下のE-Commerce拡張機能の値をサポートしています。
  * 注文小計（`_csubtotal`）
  * 注文通貨（`_ccurrency`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を構成します。

* **Web Dev Key**

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下のとおりです。

### タグの構成

| 変数                        | 説明         |
|:----------------------------|:-------------|
| Web Dev Key (`web_dev_key`) | [文字列]     |

### E-Commerce

| 変数                                                  | 説明         |
|:------------------------------------------------------|:-------------|
| 小計（`order_subtotal`）（`_csubtotal`を上書き）      | [文字列]     |
| 通貨（`order_currency`）（`_ccurrency`を上書き）      | [文字列]     |

### イベント

| 変数             | 説明             |
|:-----------------|:-----------------|
| 検索             | `search`         |
| カートに追加     | `addToCart`      |
| カートから削除   | `removeFromCart` |
| 購入             | `purchase`       |
| ダウンロード     | `download`       |
| 登録             | `signup`         |
| サブスクリプション | `subscriptions`  |
| カスタム         | `Custom`         |

### イベント固有のパラメータ

| 変数             | 説明             |
|:-----------------|:-----------------|
| 検索             | `search`         |
| カートに追加     | `addToCart`      |
| カートから削除   | `removeFromCart` |
| 購入             | `purchase`       |
| ダウンロード     | `download`       |
| 登録             | `signup`         |
| サブスクリプション | `subscriptions`  |
| カスタムイベント | `Custom_Event`   |