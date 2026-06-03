---
title: AppsFlyer Web SDKタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAppsFlyer Web SDKタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/appsflyer-web-sdk-tag/
---
People-Based AttributionのWeb-S2S APIは、Web SDKの範囲外でウェブサイト上で発生するイベントをマーケターが報告できるように補完します。

## タグのヒント

* Web Dev Keyを取得するには、**AppsFlyer &gt; My Apps &gt; View brand bundles**に移動します。
* マッピングを使用して：
  * E-Commerce拡張値を動的に上書き
  * イベントトリガーの構成

* 以下のE-Commerce拡張値をサポート：
  * 注文小計（`_csubtotal`）
  * 注文通貨（`_ccurrency`）

## タグ構成

まず、タグマーケットプレイスに移動し、AppsFlyer Web SDKタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **Web Dev Key**

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### タグ構成

| 変数                    | 説明 |
|:----------------------------|:------------|
| Web Dev Key (`web_dev_key`) | [文字列]    |

### E-Commerce

| 変数                                              | 説明 |
|:------------------------------------------------------|:------------|
| 小計 (`order_subtotal`) (Overrides `_csubtotal`) | [文字列]    |
| 通貨 (`order_currency`) (Overrides `_ccurrency`)  | [文字列]    |

### イベント

| 変数       | 説明      |
|:---------------|:-----------------|
| 検索         | `search`         |
| カートに追加      | `addToCart`      |
| カートから削除 | `removeFromCart` |
| 購入       | `purchase`       |
| ダウンロード       | `download`       |
| サインアップ         | `signup`         |
| サブスクリプション  | `subscriptions`  |
| カスタム         | `Custom`         |

### イベント固有のパラメータ

| 変数       | 説明      |
|:---------------|:-----------------|
| 検索         | `search`         |
| カートに追加      | `addToCart`      |
| カートから削除 | `removeFromCart` |
| 購入       | `purchase`       |
| ダウンロード       | `download`       |
| サインアップ         | `signup`         |
| サブスクリプション  | `subscriptions`  |
| カスタムイベント   | `Custom_Event`   |
