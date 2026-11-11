---
title: CJ Universalタグ構成ガイド
description: この記事では、CJ Universalタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/cj-universal-tag/
---
CJ Universalタグは、Chrome、Safari、Firefoxなど、トラッキング制限のあるブラウザー全体で完全なトラッキング保護を提供し、プログラムの整合性を維持します。この次世代タグは、状況に応じたコミッション構成のためのVertical Attributesやトランザクションレベルのインサイトなど、高度なトラッキング機能を有効にすることで、CJネットワークでの成功を支援します。Universalタグは、Affiliate Incrementalityやクロスチャネルのカスタマージャーニーレポートなど、将来の機能エンリッチメントの基盤としても機能します。

## タグに関するヒント

* 注文IDが構成されている場合、コンバージョンタグが存在します。
* CJのClient Integrationチームは、このタグをバンドルしないことを推奨しています。
* 次のEコマース拡張パラメーターをサポートしています。
    * 注文ID（`_corder`）
    * 小計（`_csubtotal`）
    * 通貨（`_ccurrency`）
    * 顧客ID（`_ccustid`）
    * 商品IDのリスト（`_cprod`）
    * 数量のリスト（`_cquan`）
    * 価格のリスト（`_cprice`）
    * 割引のリスト（`_cpdisc`）
* マッピングを使用して、タグ構成を上書きまたは動的に構成します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **プロキシパス**：  
この統合のメリットを最大限に活用するには、CJのサーバーへのリバースプロキシを構成します。例：`//yourdomain.com/proxydir/tags/<YOUR_TAG_ID>/tag.js`。
* **CJホストタグID**：  
リバースプロキシを構成できない場合は、CJホストタグを使用するためにCJホストタグIDを入力します。この値はCJのClient Integrationチームから提供されます。
例：`//www.mczbf.com/tags/<TAG_ID>/tag.js`。
* **アクショントラッカーID**：  
CJのClient Integrationチームから提供される静的な値です。
* **CJ Enterprise ID**：  
CJのClient Integrationチームから提供される静的な値です。
* **ページ訪問を有効化**：  
コンバージョンページを除くすべてのページで、CJページ訪問タグを有効にします。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `proxyPath` | プロキシパス。 |
| `tagId` | CJホストタグID。 |
| `actionTrackerId` | アクショントラッカーID。 |
| `enterpriseId` | CJ Enterprise ID。 |
| `enablePageVisit` | ブール値。ページ訪問タグを有効にします。 |
| `bypassChannel.name` | バイパスチャネル名。 |
| `bypassChannel.timestamp` | バイパスチャネルのタイムスタンプ。 |

### ページ訪問

| 変数 | 説明 |
|:---------|:------------|
| `pageType` | ページタイプ。 |
| `emailHash` | メールアドレスのSHA-256ハッシュ。 |
| `referringChannel` | 参照元チャネル。 |

### Eコマース

| 変数 | 説明 |
|:---------|:------------|
| `order_id` | 注文ID（`_corder`を上書き）。 |
| `order_subtotal` | 小計（`_csubtotal`を上書き）。 |
| `order_currency` | 通貨（`_ccurrency`を上書き）。 |
| `order_coupon_code` | プロモーションコード（`_cpromo`を上書き）。 |
| `order_discount` | 割引。 |
| `customer_id` | ユーザーIDまたは顧客ID（`_ccustid`を上書き）。 |
| `product_id` | 商品IDの配列（`_cprod`を上書き）。 |
| `product_quantity` | 商品数量の配列（`_cquan`を上書き）。 |
| `product_unit_price` | 商品単価の配列（`_cprice`を上書き）。 |
| `product_discount` | 商品割引の配列（`_cpdisc`を上書き）。 |
| `brand` | 購入商品のブランド。 |
| `brandId` | ブランド識別子。 |
| `category` | 購入商品のカテゴリー。 |
| `customerStatus` | 顧客ステータス。 |
| `delivery` | 配送方法。 |
| `marketingChannel` | マーケティングチャネル。 |

### ロイヤルティ

| 変数 | 説明 |
|:---------|:------------|
| `loyaltyEarned` | 獲得したロイヤルティポイント。 |
| `loyaltyFirstTimeSignup` | ロイヤルティプログラムへの初回登録。 |
| `loyaltyLevel` | ロイヤルティレベル。 |
| `loyaltyRedeemed` | 使用したロイヤルティポイント。 |
| `loyaltyStatus` | ロイヤルティステータス。 |