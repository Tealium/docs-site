---
title: Trusted Shopsタグ構成ガイド
description: この記事では、Trusted Shopsタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/trusted-shops-tag/
---
## タグのヒント

* マッピングを使用して、標準の構成値を動的に上書きします。
* 注文IDが構成されると（通常は注文確認ページで）、非表示の`trustedShopsCheckout` `&lt;div&gt;`がページに追加されます。以下の`&lt;span&gt;`タグは、E-Commerce拡張機能またはマッピングを介して値が構成されている場合、`&lt;div&gt;`内に作成されます：
    * `tsCheckoutOrderNr`
    * `tsCheckoutBuyerEmail`
    * `tsCheckoutOrderAmount`
    * `tsCheckoutOrderCurrency`
    * `tsCheckoutOrderPaymentType`
    * `tsCheckoutOrderEstDeliveryDate`

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の構成を行います：

* **Trusted Shops ID**: Trusted Shopsから提供されます。
* **Y-Offset**: ページ下部からのオフセット。
* **Variant**: `custom`および`custom_reviews`バリアントにはカスタム要素IDが必要です。
* **Custom Element ID**: `custom`および`custom_reviews`バリアントに必要です。
* **Trustcard Direction**: カスタムバリアント用。
* **Disable Responsive Behaviour**: 購入に対するレビューのリクエストを無効にします。
* **Disable Trust Badge**: 信頼バッジの表示を無効にします。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリーは以下の通りです：

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `_tsid`| Trusted Shops ID   |
| `_tsConfig.yOffset`| Y-offset   |
|  `_tsConfig.variant`  | Variant. この値は`text`, `default`, `small`, `reviews`, `custom`, `custom_reviews`のいずれかになります。 |
| `_tsConfig.customElementId` | カスタム要素ID。  |
| `_tsConfig.trustcardDirection`   | Trustcard direction. この値は`topRight`, `topLeft`, `bottomRight`, `bottomLeft`のいずれかになります。 |
| `_tsConfig.disableResponsive` | レスポンシブな動作を無効にします。この値は`false`または`true`になります。 |
| `_tsConfig.disableTrustBadge`| 信頼バッジを無効にします。この値は`false`または`true`になります。 |

### E-Commerce

| 変数 | 説明 |
|:---------|:------------|
| `order_id` (`_corder`を上書き)| 注文ID   |
| `order_total` (`_ctotal`を上書き)| 注文合計   |
| `order_currency` (`_ccurrency`を上書き)| 通貨   |
| `customer_id` (`_ccustid`を上書き)| 顧客ID   |
| `tsCheckoutOrderPaymentType`| 注文の支払いタイプ   |
| `tsCheckoutOrderEstDeliveryDate`| 注文の推定配達日   |

