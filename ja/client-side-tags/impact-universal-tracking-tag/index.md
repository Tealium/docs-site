---
title: Impact ユニバーサルトラッキングタグ構成ガイド
description: この記事では、Impact ユニバーサルトラッキングタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/impact-universal-tracking-tag/
---
## タグのヒント

* 顧客のメールアドレスのSHA1ハッシュが含まれる変数を `customerEmail` にマッピングします。ハッシュ化されていないメールアドレスはImpactのトラッキングコールから削除されます。
* カスタムマッピングはImpactトラッキングコールのプロパティオブジェクトに渡されます。
* このタグは以下のEコマース拡張パラメータをサポートしています：
    * 注文ID (`_corder`)
    * 注文小計 (`_csubtotal`)
    * 注文送料 (`_cship`)
    * 注文税金 (`_ctax`)
    * 注文通貨 (`_ccurrency`)
    * 注文プロモコード (`_cpromo`)
    * 顧客ID (`_ccustid`)
    * 顧客の市町村区 (`_ccity`)
    * 顧客の州 (`_cstate`)
    * 顧客の郵便番号 (`_czip`)
    * 顧客の国 (`_ccountry`)
    * 商品名のリスト (`_cprodname`)
    * 商品SKUのリスト (`_csku`)
    * 商品ブランドのリスト (`_cbrand`)
    * 商品カテゴリのリスト (`_ccat`)
    * 商品サブカテゴリのリスト (`_ccat2`)
    * 商品数量のリスト (`_cquan`)
    * 商品価格のリスト (`_cprice`)

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグの追加方法についての詳細は、[タグの管理]()を参照してください。

タグを追加する際には、以下の構成を構成します：

* **ユニークID**：あなたのImpactユニークID。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信プロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `acid` | ユニークID |
| `actionTrackerId` | アクショントラッカーID |

### Eコマースプロパティ

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `currencyCode` | 文字列 | 通貨コード（`_ccurrency`を上書き）。 |
| `orderDiscount` | 文字列 | 注文割引。 |
| `orderId` | 文字列 | 注文ID（`_corder`を上書き）。 |
| `orderPromoCode` | 文字列 | 注文プロモコード（`_cpromo`を上書き）。 |
| `orderPromoCodeDesc` | 文字列 | 注文プロモコード説明。 |
| `orderRebate` | 文字列 | 注文リベート。 |
| `orderShipping` | 文字列 | 注文送料（`_cship`を上書き）。 |
| `orderSubTotalPostDiscount` | 文字列 | 割引後の注文小計。 |
| `orderSubTotalPreDiscount` | 文字列 | 割引前の注文小計（`_csubtotal`を上書き）。 |
| `orderTax` | 文字列 | 注文税金（`_ctax`を上書き）。 |
| `paymentType` | 文字列 | 支払いタイプ。 |
| `product_brand` | `配列` | 商品ブランドのリスト（`_cbrand`を上書き）。 |
| `product_category` | `配列` | 商品カテゴリのリスト（`_ccat`を上書き）。 |
| `product_deliveryType` | `配列` | 商品配送タイプのリスト。 |
| `product_discount` | `配列` | 商品割引のリスト。 |
| `product_mpn` | `配列` | 商品MPNのリスト。 |
| `product_name` | `配列` | 商品名のリスト（`_cprodname`を上書き）。 |
| `product_quantity` | `配列` | 商品数量のリスト（`_cquan`を上書き）。 |
| `product_referenceId` | `配列` | 商品参照IDのリスト。 |
| `product_sku` | `配列` | 商品SKUのリスト（`_csku`を上書き）。 |
| `product_subcategory` | `配列` | 商品サブカテゴリのリスト（`_ccat2`を上書き）。 |
| `product_subTotal` | `配列` | 商品小計/価格のリスト（`_cprice`を上書き）。 |
| `product_promoCode` | `配列` | 商品プロモコードのリスト。 |
| `product_promoCodeDesc` | `配列` | 商品プロモコード説明のリスト。 |
| `product_totalDiscount` | `配列` | 商品総割引のリスト。 |
| `product_totalRebate` | `配列` | 商品総リベートのリスト。 |

### 一般プロパティ

| 変数 | 説明 |
|:---------|:------------|
| `callerId` | コーラーID。 |
| `clickId` | クリックID。 |
| `customerCity` | 顧客の市町村区（`_ccity`を上書き）。 |
| `customerCountry` | 顧客の国（`_ccountry`を上書き）。 |
| `customerEmail` | 顧客メール。 |
| `customerId` | 顧客ID（`_ccustid`を上書き）。 |
| `customerPostCode` | 顧客の郵便番号（`_czip`を上書き）。 |
| `customerRegion` | 顧客の地域（`_cstate`を上書き）。 |
| `customerStatus` | 顧客ステータス。 |
| `date1` | 日付パラメータ1。 |
| `date2` | 日付パラメータ2。 |
| `date3` | 日付パラメータ3。 |
| `dispositionCode` | 処分コード。 |
| `giftPurchase` | ギフト購入。 |
| `hearAboutUs` | 私たちのことを知ったきっかけ。 |
| `locationName` | ロケーション名。 |
| `locationType` | ロケーションタイプ。 |
| `money1` | 金額パラメータ1。 |
| `money2` | 金額パラメータ2。 |
| `money3` | 金額パラメータ3。 |
| `note` | ノート。 |
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
| `domReady` | DOM準備完了。 |
| `tag` | タグ。 |
