---
title: Taboola Pixel タグ構成ガイド
description: この記事では、Taboola Pixel タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/taboola-pixel-tag/
---
## タグのヒント

* このタグはイベントトリガーとパラメータを使用してデータを送信します。
* 複数のTaboola IDを使用する場合、同一のデータが各IDに送信されます。
* マッピングを使用してパラメータ値を上書きしたり、カスタムデータを送信します。
* カスタム変数を追加する前に、Taboolaサポートに確認してください。

## タグの構成

まず、TealiumのタグマーケットプレイスにアクセスしてTaboola Pixelタグを追加します（[タグの追加方法についてはこちら](https://docs.tealium.com/manage-tags/)を参照）。

タグを追加した後、以下の構成を構成します：

* **Taboola ID(s)**: これは数値です。複数のIDはコンマで区切ります。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`client_name`|  Taboola ID。 |
|`orderid`|  注文ID、`_corder`を上書きします。 |
|`revenue`|  注文合計、`_ctotal`を上書きします。 |
|`currency`|  通貨、`_ccurrency`を上書きします。 |
|`quantity`|  数量。 |
| `item-url` |  ページURL、`document.location.href`を上書きします。 |

### イベント

|変数| 説明|
|---| ---|
|`page_view`|  ページビュー。 |
|`view_content`|  コンテンツ表示。 |
|`lead`|  リード。 |
|`complete_registration`|  登録完了。 |
|`make_purchase`|  購入。 |
|`search`|  検索。 |
|`add_to_cart`|  カートに追加。 |
|`add_to_wishlist`|  ほしい物リストに追加。 |
|`start_checkout`|  チェックアウト開始。 |
|`add_payment_info`|  支払情報の追加。 |
|`app_install`|  アプリインストール。 |
|`custom`|  カスタム。 |

### イベントパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください

|変数| 説明|
|---| ---|
|`orderid`|  注文ID。 |
|`revenue`|  注文合計。 |
|`currency`|  通貨。 |
|`quantity`|  数量。 |
|`custom`|  カスタム。 |

### Eコマースイベント

|変数| 説明|
|---| ---|
| `HOME_PAGE_VISIT` | ホームページ訪問。| 
| `CATEGORY_VIEW` | カテゴリ表示。 | 
| `PRODUCT_VIEW` | 商品表示。 | 
| `ADD_TO_CART` | カートに追加。 | 
| `REMOVE_FROM_CART` | カートから削除。 | 
| `CHECKOUT` | チェックアウト。 | 
| `PURCHASE` | 購入。 | 
| `SEARCH` | 検索。 | 
| `ADD_TO_WISH_LIST` | ほしい物リストに追加。 | 
| `REMOVE_FROM_WISH_LIST` | ほしい物リストから削除。 |

### Eコマースイベントパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください

| イベント | 説明 |
|:------|:------------|
| `productIds` | 商品ID。 |
| `category` | カテゴリ。 |
| `categoryId` | カテゴリID。 |
| `searchTerm` | 検索語。 |
| `orderId` | 注文ID。 |
| `value` | 値。 |
| `currency` | 通貨。 |
| `cartDetails.productId` | カート商品。 |
| `cartDetails.quantity` | カート数量。 |
| `cartDetails.price` | カート価格。 |