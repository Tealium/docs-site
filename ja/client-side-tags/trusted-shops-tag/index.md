---
title: Trusted Shopsタグ構成ガイド
description: この記事では、Trusted Shopsタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/trusted-shops-tag/
---
## タグ構成のヒント

* マッピングを使用すると、標準構成値を動的に上書きできます。
* 注文IDが構成されている場合（通常は注文確認ページ）、非表示の`trustedShopsCheckout` `<div>`がページに追加されます。Eコマース拡張機能またはマッピングによって値が構成されている場合、次の`<span>`タグが`<div>`内に作成されます。
    * `tsCheckoutOrderNr`
    * `tsCheckoutBuyerEmail`
    * `tsCheckoutOrderAmount`
    * `tsCheckoutOrderCurrency`
    * `tsCheckoutOrderPaymentType`
    * `tsCheckoutOrderEstDeliveryDate`

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の項目を構成します。

* **Trusted Shops ID**：Trusted Shopsから提供されるID。
* **Y-Offset**：ページ下端からのオフセット。
* **Variant**：`custom`および`custom_reviews`バリアントでは、カスタム要素IDが必要です。
* **Custom Element ID**：`custom`および`custom_reviews`バリアントでは必須です。
* **Trustcard Direction**：カスタムバリアントで使用するトラストカードの方向。
* **Disable Responsive Behaviour**：購入に対するレビュー依頼を無効にします。
* **Disable Trust Badge**：トラストバッジの表示を無効にします。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `_tsid`| Trusted Shops ID |
| `_tsConfig.yOffset`| Yオフセット |
| `_tsConfig.variant` | バリアント。この値には、`text`、`default`、`small`、`reviews`、`custom`、または`custom_reviews`を指定できます。 |
| `_tsConfig.customElementId` | カスタム要素ID。 |
| `_tsConfig.trustcardDirection` | トラストカードの方向。この値には、`topRight`、`topLeft`、`bottomRight`、または`bottomLeft`を指定できます。 |
| `_tsConfig.disableResponsive` | レスポンシブ動作を無効にします。この値には、`false`または`true`を指定できます。 |
| `_tsConfig.disableTrustBadge`| トラストバッジを無効にします。この値には、`false`または`true`を指定できます。 |

### Eコマース

| 変数 | 説明 |
|:---------|:------------|
| `order_id`（`_corder`を上書き）| 注文ID |
| `order_total`（`_ctotal`を上書き）| 注文合計 |
| `order_currency`（`_ccurrency`を上書き）| 通貨 |
| `customer_id`（`_ccustid`を上書き）| 顧客ID |
| `tsCheckoutOrderPaymentType`| 注文の支払い方法 |
| `tsCheckoutOrderEstDeliveryDate`| 注文の配達予定日 |