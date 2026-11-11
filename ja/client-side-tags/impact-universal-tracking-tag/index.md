---
title: Impact Universal Trackingタグ構成ガイド
description: この記事では、Impact Universal Trackingタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/impact-universal-tracking-tag/
---
## タグに関するヒント

* 顧客のメールアドレスのSHA1ハッシュを含む変数を`customerEmail`にマッピングします。ハッシュ化されていないメールアドレスは、Impactのトラッキング呼び出しから削除されます。
* カスタムマッピングは、Impactのトラッキング呼び出しのpropertiesオブジェクトに渡されます。
* このタグは、以下のE-Commerce拡張パラメータをサポートしています。
    * 注文ID（`_corder`）
    * 注文小計（`_csubtotal`）
    * 注文の送料（`_cship`）
    * 注文の税額（`_ctax`）
    * 注文通貨（`_ccurrency`）
    * 注文プロモーションコード（`_cpromo`）
    * 顧客ID（`_ccustid`）
    * 顧客の市区町村（`_ccity`）
    * 顧客の州（`_cstate`）
    * 顧客の郵便番号（`_czip`）
    * 顧客の国（`_ccountry`）
    * 商品名のリスト（`_cprodname`）
    * 商品SKUのリスト（`_csku`）
    * 商品ブランドのリスト（`_cbrand`）
    * 商品カテゴリのリスト（`_ccat`）
    * 商品サブカテゴリのリスト（`_ccat2`）
    * 商品数量のリスト（`_cquan`）
    * 商品価格のリスト（`_cprice`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときは、以下の構成を構成します。

* **一意のID**：Impactの一意のID。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数からベンダータグ内の対応する変数に値を送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `acid` | 一意のID |
| `actionTrackerId` | アクショントラッカーID |

### Eコマースプロパティ

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `currencyCode` | 文字列 | 通貨コード（`_ccurrency`を上書きします）。 |
| `orderDiscount` | 文字列 | 注文の割引額。 |
| `orderId` | 文字列 | 注文ID（`_corder`を上書きします）。 |
| `orderPromoCode` | 文字列 | 注文プロモーションコード（`_cpromo`を上書きします）。 |
| `orderPromoCodeDesc` | 文字列 | 注文プロモーションコードの説明。 |
| `orderRebate` | 文字列 | 注文のリベート。 |
| `orderShipping` | 文字列 | 注文の送料（`_cship`を上書きします）。 |
| `orderSubTotalPostDiscount` | 文字列 | 割引後の注文小計。 |
| `orderSubTotalPreDiscount` | 文字列 | 割引前の注文小計（`_csubtotal`を上書きします）。 |
| `orderTax` | 文字列 | 注文の税額（`_ctax`を上書きします）。 |
| `paymentType` | 文字列 | 支払いタイプ。 |
| `product_brand` | `Array` | 商品ブランドのリスト（`_cbrand`を上書きします）。 |
| `product_category` | `Array` | 商品カテゴリのリスト（`_ccat`を上書きします）。 |
| `product_deliveryType` | `Array` | 商品配送タイプのリスト。 |
| `product_discount` | `Array` | 商品割引のリスト。 |
| `product_mpn` | `Array` | 商品MPNのリスト。 |
| `product_name` | `Array` | 商品名のリスト（`_cprodname`を上書きします）。 |
| `product_quantity` | `Array` | 商品数量のリスト（`_cquan`を上書きします）。 |
| `product_referenceId` | `Array` | 商品参照IDのリスト。 |
| `product_sku` | `Array` | 商品SKUのリスト（`_csku`を上書きします）。 |
| `product_subcategory` | `Array` | 商品サブカテゴリのリスト（`_ccat2`を上書きします）。 |
| `product_subTotal` | `Array` | 商品小計／価格のリスト（`_cprice`を上書きします）。 |
| `product_promoCode` | `Array` | 商品プロモーションコードのリスト。 |
| `product_promoCodeDesc` | `Array` | 商品プロモーションコードの説明のリスト。 |
| `product_totalDiscount` | `Array` | 商品の合計割引額のリスト。 |
| `product_totalRebate` | `Array` | 商品の合計リベート額のリスト。 |

### 一般プロパティ

| 変数 | 説明 |
|:---------|:------------|
| `callerId` | 呼び出し元ID。 |
| `clickId` | クリックID。 |
| `customerCity` | 顧客の市区町村（`_ccity`を上書きします）。 |
| `customerCountry` | 顧客の国（`_ccountry`を上書きします）。 |
| `customerEmail` | 顧客のメールアドレス。 |
| `customerId` | 顧客ID（`_ccustid`を上書きします）。 |
| `customerPostCode` | 顧客の郵便番号（`_czip`を上書きします）。 |
| `customerRegion` | 顧客の地域（`_cstate`を上書きします）。 |
| `customerStatus` | 顧客ステータス。 |
| `date1` | 日付パラメータ1。 |
| `date2` | 日付パラメータ2。 |
| `date3` | 日付パラメータ3。 |
| `dispositionCode` | 処理コード。 |
| `giftPurchase` | ギフト購入。 |
| `hearAboutUs` | 認知経路。 |
| `locationName` | 場所名。 |
| `locationType` | 場所タイプ。 |
| `money1` | 金額パラメータ1。 |
| `money2` | 金額パラメータ2。 |
| `money3` | 金額パラメータ3。 |
| `note` | 注記。 |
| `numeric1` | 数値パラメータ1。 |
| `numeric2` | 数値パラメータ2。 |
| `numeric3` | 数値パラメータ3。 |
| `phoneNumber` | 電話番号。 |
| `referenceId` | 参照ID。 |
| `siteCategory` | サイトカテゴリ。 |
| `siteVersion` | サイトバージョン。 |
| `test` | テストフラグ。 |
| `text1` | テキストパラメータ1。 |
| `text2` | テキストパラメータ2。 |
| `text3` | テキストパラメータ3。 |

### オプション

| 変数 | 説明 |
|:---------|:------------|
| `domReady` | DOMの準備完了。 |
| `tag` | タグ。 |