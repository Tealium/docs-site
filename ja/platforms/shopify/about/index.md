---
title: Tealium Shopifyアプリについて
description: この記事では、ShopifyマーケットプレイスのTealiumアプリケーションについての情報を提供します。
url: https://docs.tealium.com/ja/platforms/shopify/about/
---
ShopifyマーケットプレイスのTealiumアプリを使用すると、以下のことができます：

* ShopifyサイトでTealium iQタグ管理を使用します。このアプリは、各ページに`utag.js`や`utag.data`などのTealiumアセットをロードします。
* ShopifyイベントデータをTealium EventStream API Hubに送信します。
* カスタムチェックアウトピクセルを使用して、EventStreamにチェックアウトデータを送信します。
* Shopify Marketsを使用して、単一のShopifyストアで複数の市場地域からのイベントを追跡します。

Shopifyの`purchase`イベントなど、一部のページイベントは、iQタグ管理ではなくShopifyによって管理されるページで発生するイベントであるため、異なる方法で処理されます。Tealiumアプリは、これらのイベントのデータをTealium EventStreamに送信します。

## 要件

* 構成中にShopifyインスタンスへの管理アクセス。
* Tealiumでデータソースを作成するためのTealiumアカウントとプロファイル情報。
* ShopifyイベントデータをEventStreamに送信する場合はTealium EventStreamが必要です。

## 追跡されるイベント

Tealiumアプリには標準データレイヤーが含まれており、Shopifyからの以下の標準イベントをサポートしています：

| イベント | Shopifyアクション |
|-------|----------------|
| `cart_add` | カートに商品を追加。 |
| `cart_remove` | カートから商品を削除。 |
| `cart_view` | カートを閲覧した顧客。 |
| `category_view` | カテゴリを閲覧した顧客。 |
| `checkout` | チェックアウトを開始した顧客。 |
| `checkout_address_info_submitted` | チェックアウトの住所情報を提出した顧客。 |
| `page_view `| ページを閲覧した顧客。 |
| `product_view` | 商品ページを閲覧した顧客。 |
| `purchase` | 購入を完了した顧客。 |
| `search` | 検索を実行した顧客。 |

詳細については、を参照してください。

ニュースレターのサインアップイベントや割引イベントは、各店舗でカスタマイズする必要があります。

### Web Pixel Extensionイベント

| Shopifyイベント | Tealiumイベント | トリガー |
|---------------|---------------|---------|
| `page_viewed` | `page_view` | 任意のストアフロントページがロードされる。 |
| `product_viewed` | `product_view` | 顧客が商品詳細ページを閲覧する。 |
| `collection_viewed` | `category_view` | 顧客がコレクション/カテゴリページを閲覧する。 |
| `cart_viewed` | `cart_view` | 顧客がカートページを閲覧する。 |
| `product_added_to_cart` | `cart_add` | 顧客が商品をカートに追加する。 |
| `product_removed_from_cart` | `cart_remove` | 顧客がカートから商品を削除する。 |
| `search_submitted` | `search` | 顧客が検索クエリを実行する。 |

### チェックアウトピクセルイベント

| Shopifyイベント | Tealiumイベント | トリガー |
|---------------|---------------|---------|
| `checkout_started` | `checkout` | 顧客がチェックアウトプロセスを開始する。 |
| `checkout_address_info_submitted` | `checkout_address_info_submitted` | 顧客が配送先住所を提出する。 |
| `checkout_completed` | `purchase` | 注文が成功裏に完了する。 |

## Webhookイベント

次のwebhookを有効にしてデータを収集することができます：

| Webhookトピック | Tealiumイベント | トリガー |
|---------------|---------------|---------|
| `CARTS_CREATE` | `cart_create` | 新しいカートが作成される。 |
| `CARTS_UPDATE` | `cart_update` | カートが変更される（追加/削除/数量変更）。 |
| `CHECKOUTS_CREATE` | `checkouts_create` | チェックアウトセッションが開始される。 |
| `ORDERS_CREATE` | `purchase` | 注文が完了し処理される。 |
| `REFUNDS_CREATE` | `shopify_refund` | 注文に対して払い戻しが行われる。 |
| `CUSTOMERS_CREATE` | `Shopify New Customer` | 新しい顧客アカウントが作成される。 |
| `CUSTOMERS_EMAIL_MARKETING_CONSENT_UPDATE` | `email_consent_change` | メールマーケティングのオプトイン/オプトアウトが変更される。 |
| `CUSTOMERS_MARKETING_CONSENT_UPDATE` | `sms_consent_change` | SMSマーケティングのオプトイン/オプトアウトが変更される。 |

### システム/GDPR webhooks

| Webhookトピック | トリガー |
|---------------|---------|
| `APP_UNINSTALLED` | マーチャントがアプリをアンインストールする。 |
| `CUSTOMERS_DATA_REQUEST` | GDPRデータアクセスリクエスト。 |
| `CUSTOMERS_REDACT` | GDPR顧客データ削除リクエスト。 |
| `SHOP_REDACT` | GDPRショップデータ削除リクエスト。 |

## チェックアウト追跡

現在、Tealium iQタグ管理でShopifyチェックアウトを追跡するための最良のオプションはカスタムピクセルです。Tealium Shopifyアプリのインストールプロセスには、カスタムピクセルを構成するオプションが含まれています。

詳細については、[Tealium Shopifyアプリのインストール]()を参照してください。