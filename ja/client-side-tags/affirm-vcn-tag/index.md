---
title: Affirmバーチャルカード統合（VCN統合）タグ構成ガイド
description: この記事では、Affirmバーチャルカード統合（VCN統合）タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/affirm-vcn-tag/
---
## タグのヒント

*   すべてのドル値は、小数点とその後の2桁を含む文字列形式である必要があります。
*   マッピングを使用して：
    *   標準の構成値を上書きします。
    *   E-Commerce拡張の値を上書きします。
*   以下のE-Commerce拡張パラメータをサポートしています：
    *   ストア
    *   顧客の都市
    *   顧客の州
    *   顧客のZIP
    *   顧客の国
    *   商品名のリスト
    *   SKUのリスト
    *   価格のリスト
    *   数量のリスト
    *   税額
    *   送料
    *   注文合計
    *   注文ID
*  説明に&#34;E-Commerce拡張を上書き&#34;とある宛先は、E-Commerce拡張が有効で、それらのパラメータに対して構成されている場合、マッピングは必要ありません。

## タグ構成

新しいタグを追加するためにタグマーケットプレイスに移動します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の構成を行います：

* **環境**：このタグがAffirmで使用する環境。
* **Sandbox API Key**：Sandbox環境に必要です。Sandbox Affirmダッシュボードで利用可能です。
* **Production API Key**：Production環境に必要です。Production Affirmダッシュボードで利用可能です。
* **Success Callback Function Name**：必須。チェックアウト成功時のコールバック関数の名前。
* **Error Callback Function Name**：必須。チェックアウトエラー時のコールバック関数の名前。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `environment` | 文字列 | 環境 |

### チェックアウトデータ

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `checkout_data.merchant.name` | 文字列 | マーチャント名 |
| `checkout_data.billing.name.first` | 文字列 | 請求先の名 |
| `checkout_data.billing.name.last` | 文字列 | 請求先の姓 |
| `checkout_data.billing.name.full` | 文字列 | 請求先のフルネーム |
| `checkout_data.billing.address.line1` | 文字列 | 請求先の住所1行目 |
| `checkout_data.billing.address.line2` | 文字列 | 請求先の住所2行目 |
| `checkout_data.billing.address.city` | 文字列 | 請求先の市区町村 |
| `checkout_data.billing.address.state` | 文字列 | 請求先の都道府県 |
| `checkout_data.billing.address.zipcode` | 文字列 | 請求先の郵便番号 |
| `checkout_data.billing.address.country` | 文字列 | 請求先の国 |
| `checkout_data.billing.phone_number` | 文字列 | 請求先の電話番号 |
| `checkout_data.billing.email` | 文字列 | 請求先のメールアドレス |
| `checkout_data.shipping.name.first` | 文字列 | 配送先の名 |
| `checkout_data.shipping.name.last` | 文字列 | 配送先の姓 |
| `checkout_data.shipping.name.full` | 文字列 | 配送先のフルネーム |
| `checkout_data.shipping.address.line1` | 文字列 | 配送先の住所1行目 |
| `checkout_data.shipping.address.line2` | 文字列 | 配送先の住所2行目 |
| `checkout_data.shipping.address.city` | 文字列 | 配送先の市区町村 |
| `checkout_data.shipping.address.state` | 文字列 | 配送先の都道府県 |
| `checkout_data.shipping.address.zipcode` (E-Commerce拡張を上書き) | 文字列 | 配送先の郵便番号 |
| `checkout_data.shipping.address.country` | 文字列 | 配送先の国 |
| `checkout_data.shipping.phone_number` | 文字列 | 配送先の電話番号 |
| `checkout_data.shipping.email` | 文字列 | 配送先のメールアドレス |
| `checkout_data.items.display_name` | 文字列の配列 | 商品表示名のリスト |
| `checkout_data.items.sku` | 文字列の配列 | 商品のSKUのリスト |
| `checkout_data.items.unit_price` | 文字列の配列 | 商品の単価のリスト |
| `checkout_data.items.qty` | 文字列の配列 | 商品の数量のリスト |
| `checkout_data.items.item_image_url` | 文字列の配列 | 商品画像URLのリスト |
| `checkout_data.items.item_url` | 文字列の配列 | 商品URLのリスト |
| `checkout_data.items.categories` | 配列の配列 | 商品カテゴリのリスト |
| `checkout_data.discounts` | オブジェクト | 割引 |
| `checkout_data.tax_amount` | 文字列 | 税額 |
| `checkout_data.shipping_amount` | 文字列 | 送料 |
| `checkout_data.total` | 文字列 | 注文合計 |
| `checkout_data.metadata.custom` | 文字列 | 注文のメタデータ |
| `checkout_data.order_id` | 文字列 | 注文ID |

