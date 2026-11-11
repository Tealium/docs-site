---
title: Taboola Pixelタグ構成ガイド
description: この記事では、Taboola Pixelタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/taboola-pixel-tag/
---
## タグに関するヒント

* このタグは、イベントトリガーとパラメータを使用してデータを送信します。
* 複数のTaboola IDを使用する場合、各IDに同一のデータが送信されます。
* マッピングを使用してパラメータ値を上書きまたは構成し、カスタムデータを送信します。
* カスタム変数を追加する前に、Taboolaサポートに確認してください。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **Taboola ID**：数値を指定します。複数のIDはカンマで区切ります。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`client_name`| Taboola ID。 |
|`orderid`| 注文ID。`_corder`を上書きします。 |
|`revenue`| 注文合計。`_ctotal`を上書きします。 |
|`currency`| 通貨。`_ccurrency`を上書きします。 |
|`quantity`| 数量。 |
| `item-url` | ページURL。`document.location.href`を上書きします。 |

### イベント

|変数| 説明|
|---| ---|
|`page_view`| ページビュー。 |
|`view_content`| コンテンツの表示。 |
|`lead`| リード。 |
|`complete_registration`| 登録完了。 |
|`make_purchase`| 購入。 |
|`search`| 検索。 |
|`add_to_cart`| カートに追加。 |
|`add_to_wishlist`| ウィッシュリストに追加。 |
|`start_checkout`| チェックアウト開始。 |
|`add_payment_info`| 支払い情報を追加。 |
|`app_install`| アプリのインストール。 |
|`custom`| カスタム。 |

### イベントパラメータ

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

|変数| 説明|
|---| ---|
|`orderid`| 注文ID。 |
|`revenue`| 注文合計。 |
|`currency`| 通貨。 |
|`quantity`| 数量。 |
|`custom`| カスタム。 |

### Eコマースイベント

|変数| 説明|
|---| ---|
| `HOME_PAGE_VISIT` | ホームページへのアクセス。| 
| `CATEGORY_VIEW` | カテゴリーの表示。 | 
| `PRODUCT_VIEW` | 商品の表示。 | 
| `ADD_TO_CART` | カートに追加。 | 
| `REMOVE_FROM_CART` | カートから削除。 | 
| `CHECKOUT` | チェックアウト。 | 
| `PURCHASE` | 購入。 | 
| `SEARCH` | 検索。 | 
| `ADD_TO_WISH_LIST` | ウィッシュリストに追加。 | 
| `REMOVE_FROM_WISH_LIST` | ウィッシュリストから削除。 |

### Eコマースイベントパラメータ

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `productIds` | 商品ID。 |
| `category` | カテゴリー。 |
| `categoryId` | カテゴリーID。 |
| `searchTerm` | 検索語句。 |
| `orderId` | 注文ID。 |
| `value` | 値。 |
| `currency` | 通貨。 |
| `cartDetails.productId` | カート内の商品。 |
| `cartDetails.quantity` | カート内商品の数量。 |
| `cartDetails.price` | カート内商品の価格。 |