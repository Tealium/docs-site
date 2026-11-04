---
title: Tealium Shopifyアプリについて
description: この記事では、Shopify MarketplaceのTealiumアプリケーションについて説明します。
url: https://docs.tealium.com/ja/platforms/shopify/about/
---
Shopify MarketplaceのTealiumアプリでは、次のことができます。

* Shopifyサイトでタグ管理を使用できます。このアプリは、サイトの各ページで`utag.js`や`utag.data`などのTealiumアセットを読み込みます。
* ShopifyのイベントデータをEvent Streaming API Hubに送信できます。
* カスタムチェックアウトピクセルを使用して、チェックアウトデータをEvent Streamingに送信できます。
* Shopify Marketsを使用して、単一のShopifyストアで複数の市場地域からのイベントをトラッキングできます。

Shopifyの`purchase`イベントなど、一部のページイベントはタグ管理によって管理されるページではなく、Shopifyが管理するページで発生するため、異なる方法で処理されます。Tealiumアプリは、これらのイベントのデータをEvent Streamingに送信します。

## 要件

* 構成時にShopifyインスタンスへの管理者アクセス権があること。
* Tealiumでデータソースを作成するために必要なTealiumアカウントとプロファイル情報があること。
* ShopifyのイベントデータをEvent Streamingに送信する場合は、Event Streamingを利用できること。

## トラッキングされるイベント

標準データレイヤーはTealiumアプリに含まれており、Shopifyの次の標準イベントをサポートしています。

| イベント | Shopifyでのアクション |
|-------|----------------|
| `cart_add` | 商品がカートに追加された。 |
| `cart_remove` | 商品がカートから削除された。 |
| `cart_view` | 顧客がカートを表示した。 |
| `category_view` | 顧客がカテゴリーを表示した。 |
| `checkout` | 顧客がチェックアウトを開始した。 |
| `checkout_address_info_submitted` | 顧客がチェックアウト時の住所情報を送信した。 |
| `page_view `| 顧客がページを表示した。 |
| `product_view` | 顧客が商品ページを表示した。 |
| `purchase` | 顧客が購入を完了した。 |
| `search` | 顧客が検索を実行した。 |

詳細については、[data-layer-and-events](https://docs.tealium.com/data-layer-and-events/)を参照してください。

ニュースレター登録イベントと割引イベントは、ストアごとにカスタマイズする必要があります。

### Web Pixel Extensionイベント

| Shopifyイベント | Tealiumイベント | トリガー |
|---------------|---------------|---------|
| `page_viewed` | `page_view` | ストアフロントのいずれかのページが読み込まれた。 |
| `product_viewed` | `product_view` | 顧客が商品の詳細ページを表示した。 |
| `collection_viewed` | `category_view` | 顧客がコレクションまたはカテゴリーページを表示した。 |
| `cart_viewed` | `cart_view` | 顧客がカートページを表示した。 |
| `product_added_to_cart` | `cart_add` | 顧客が商品をカートに追加した。 |
| `product_removed_from_cart` | `cart_remove` | 顧客が商品をカートから削除した。 |
| `search_submitted` | `search` | 顧客が検索クエリを実行した。 |

### Checkout Pixelイベント

| Shopifyイベント | Tealiumイベント | トリガー |
|---------------|---------------|---------|
| `checkout_started` | `checkout` | 顧客がチェックアウト処理を開始した。 |
| `checkout_address_info_submitted` | `checkout_address_info_submitted` | 顧客が配送先住所を送信した。 |
| `checkout_completed` | `purchase` | 注文が正常に完了した。 |

## Webhookイベント

データ収集のために、次のWebhookを有効にできます。

| Webhookトピック | Tealiumイベント | トリガー |
|---------------|---------------|---------|
| `CARTS_CREATE` | `cart_create` | 新しいカートが作成された。 |
| `CARTS_UPDATE` | `cart_update` | カートが変更された（追加、削除、数量変更）。 |
| `CHECKOUTS_CREATE` | `checkouts_create` | チェックアウトセッションが開始された。 |
| `ORDERS_CREATE` | `purchase` | 注文が完了し、処理された。 |
| `REFUNDS_CREATE` | `shopify_refund` | 注文に対する返金が行われた。 |
| `CUSTOMERS_CREATE` | `Shopify New Customer` | 新しい顧客アカウントが作成された。 |
| `CUSTOMERS_EMAIL_MARKETING_CONSENT_UPDATE` | `email_consent_change` | メールマーケティングのオプトインまたはオプトアウト構成が変更された。 |
| `CUSTOMERS_MARKETING_CONSENT_UPDATE` | `sms_consent_change` | SMSマーケティングのオプトインまたはオプトアウト構成が変更された。 |

### システム／GDPR Webhook

| Webhookトピック | トリガー |
|---------------|---------|
| `APP_UNINSTALLED` | マーチャントがアプリをアンインストールした。 |
| `CUSTOMERS_DATA_REQUEST` | GDPRに基づくデータアクセス要求が行われた。 |
| `CUSTOMERS_REDACT` | GDPRに基づく顧客データの削除要求が行われた。 |
| `SHOP_REDACT` | GDPRに基づくショップデータの削除要求が行われた。 |

## チェックアウトのトラッキング

現在、カスタムピクセルは、タグ管理を使用してShopifyのチェックアウトをトラッキングするための最適なオプションです。Tealium Shopifyアプリのインストールプロセスには、カスタムピクセルを構成するオプションが含まれています。

詳細については、[Tealium Shopifyアプリのインストール](https://docs.tealium.com/install-tealium-shopify-app/#configure-the-checkout-pixel)を参照してください。