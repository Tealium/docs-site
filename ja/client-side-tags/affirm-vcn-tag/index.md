---
title: Affirm 仮想カード連携（VCN 連携）タグ構成ガイド
description: この記事では、Affirm 仮想カード連携（VCN 連携）タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/affirm-vcn-tag/
---
## タグに関するヒント

*   すべての金額値は、小数点以下2桁を含む文字列形式にする必要があります。
*   マッピングは、次の目的で使用します。
    *   標準構成値を上書きする。
    *   E コマース拡張機能の値を上書きする。
*   次の E コマース拡張機能パラメーターをサポートしています。
    *   ストア
    *   顧客の市区町村
    *   顧客の州
    *   顧客の郵便番号
    *   顧客の国
    *   商品名のリスト
    *   SKU のリスト
    *   価格のリスト
    *   数量のリスト
    *   税額
    *   配送料
    *   注文合計
    *   注文 ID
*  説明に「E コマース拡張機能を上書き」と記載されている送信先については、E コマース拡張機能を有効にし、該当するパラメーターを構成している場合、マッピングは必要ありません。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を行います。

* **環境**：Affirm でこのタグが使用する環境。
* **サンドボックス API キー**：（サンドボックス環境では必須）サンドボックスの Affirm ダッシュボードで確認できます。
* **本番 API キー**：（本番環境では必須）本番環境の Affirm ダッシュボードで確認できます。
* **成功コールバック関数名**：（必須）チェックアウト成功時に呼び出すコールバック関数の名前。
* **エラーコールバック関数名**：（必須）チェックアウトエラー時に呼び出すコールバック関数の名前。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `environment` | 文字列 | 環境 |

### チェックアウトデータ

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `checkout_data.merchant.name` | 文字列 | 販売者名 |
| `checkout_data.billing.name.first` | 文字列 | 請求先の名 |
| `checkout_data.billing.name.last` | 文字列 | 請求先の姓 |
| `checkout_data.billing.name.full` | 文字列 | 請求先の氏名 |
| `checkout_data.billing.address.line1` | 文字列 | 請求先住所の1行目 |
| `checkout_data.billing.address.line2` | 文字列 | 請求先住所の2行目 |
| `checkout_data.billing.address.city` | 文字列 | 請求先住所の市区町村 |
| `checkout_data.billing.address.state` | 文字列 | 請求先住所の州 |
| `checkout_data.billing.address.zipcode` | 文字列 | 請求先住所の郵便番号 |
| `checkout_data.billing.address.country` | 文字列 | 請求先住所の国 |
| `checkout_data.billing.phone_number` | 文字列 | 請求先の電話番号 |
| `checkout_data.billing.email` | 文字列 | 請求先のメールアドレス |
| `checkout_data.shipping.name.first` | 文字列 | 配送先の名 |
| `checkout_data.shipping.name.last` | 文字列 | 配送先の姓 |
| `checkout_data.shipping.name.full` | 文字列 | 配送先の氏名 |
| `checkout_data.shipping.address.line1` | 文字列 | 配送先住所の1行目 |
| `checkout_data.shipping.address.line2` | 文字列 | 配送先住所の2行目 |
| `checkout_data.shipping.address.city` | 文字列 | 配送先住所の市区町村 |
| `checkout_data.shipping.address.state` | 文字列 | 配送先住所の州 |
| `checkout_data.shipping.address.zipcode`（E コマース拡張機能を上書き） | 文字列 | 配送先住所の郵便番号 |
| `checkout_data.shipping.address.country` | 文字列 | 配送先住所の国 |
| `checkout_data.shipping.phone_number` | 文字列 | 配送先の電話番号 |
| `checkout_data.shipping.email` | 文字列 | 配送先のメールアドレス |
| `checkout_data.items.display_name` | 文字列の配列 | 商品表示名のリスト |
| `checkout_data.items.sku` | 文字列の配列 | 商品 SKU のリスト |
| `checkout_data.items.unit_price` | 文字列の配列 | 商品単価のリスト |
| `checkout_data.items.qty` | 文字列の配列 | 商品数量のリスト |
| `checkout_data.items.item_image_url` | 文字列の配列 | 商品画像 URL のリスト |
| `checkout_data.items.item_url` | 文字列の配列 | 商品 URL のリスト |
| `checkout_data.items.categories` | 配列の配列 | 商品カテゴリーのリスト |
| `checkout_data.discounts` | オブジェクト | 割引 |
| `checkout_data.tax_amount` | 文字列 | 税額 |
| `checkout_data.shipping_amount` | 文字列 | 配送料 |
| `checkout_data.total` | 文字列 | 注文合計 |
| `checkout_data.metadata.custom` | 文字列 | 注文メタデータ |
| `checkout_data.order_id` | 文字列 | 注文 ID |