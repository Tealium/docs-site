---
title: AppsFlyer Smart Banner SDKタグ構成ガイド
description: この記事では、タグ管理アカウントでAppsFlyer Smart Banner SDKタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/appsflyer-smart-banner-sdk-tag/
---
## タグに関するヒント

* AppsFlyer Web SDKまたはAppsFlyer Smart Banner SDKのいずれか一方を使用し、両方を同時に使用しないでください。
* Web Dev Keyを取得するには、AppsFlyerで**My Apps**タブに移動し、**View brand bundles**をクリックします。
* Your Banner Keyを取得するには、AppsFlyerで**Engagement & Deep Linking > Smart Banners**に移動します。
* マッピングは、次の目的で使用します。
  * E-Commerce拡張機能の値を動的に上書きする
  * イベントトリガーを構成する
* 次のE-Commerce拡張機能の値をサポートしています。
  * 注文小計（`_csubtotal`）
  * 注文通貨（`_ccurrency`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **Web Dev Key**
* **Your Banner Key**

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### タグの構成

| 変数 | データ型 | 説明 |
|:---------|:------------|:------------|
| `web_dev_key` | 文字列 | Web開発者キー |
| `your_banner_key` | 文字列 | バナーキー |

### E-Commerce

| 変数 | データ型 | 説明 |
|:---------|:------------|:------------|
| `order_subtotal`（`_csubtotal`を上書き） | 文字列 | 小計 |
| `order_currency`（`_ccurrency`を上書き） | 文字列 | 通貨 |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `search` | 検索 |
| `addToCart` | カートに追加 |
| `removeFromCart` | カートから削除 |
| `purchase` | 購入 |
| `download` | ダウンロード |
| `signup` | サインアップ |
| `subscriptions` | サブスクリプション |
| `Custom` | カスタム |

### イベント固有のパラメーター

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `search` | 検索 |
| `addToCart` | カートに追加 |
| `removeFromCart` | カートから削除 |
| `purchase` | 購入 |
| `download` | ダウンロード |
| `signup` | サインアップ |
| `subscriptions` | サブスクリプション |
| `Custom` | カスタム |