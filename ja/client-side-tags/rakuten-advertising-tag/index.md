---
title: 楽天広告タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントで楽天広告タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/rakuten-advertising-tag/
---
## タグのヒント

* **Extract From Code** フィールドに `affiliateConfig` オブジェクトを貼り付けると、タグは自動的に `ranMID`、`discountType`、`includeStatus` パラメータを自動的に構成します。
* 注文IDが構成されるとコンバージョンが発生します。
* アフィリエイト機能は **Allow Commission** が `True` に構成されている場合のみ利用可能です。
* 以下のEコマース拡張パラメータをサポートします：
  * 注文ID (`_corder`)
  * 小計 (`_csubtotal`)
  * 税額 (`_ctax`)
  * 通貨 (`_ccurrency`)
  * プロモーションコード (`_cpromo`)
  * 顧客ID (`_ccustid`)
  * 製品IDリスト (`_cprod`)
  * 名前リスト (`_cprodname`)
  * 数量リスト (`_cquan`)
  * 価格リスト (`_cprice`)
  * 割引リスト (`_cpdisc`)

### タグの構成

まず、Tealiumのタグマーケットプレイスにアクセスして、楽天マーケティングタグを追加します。詳細については、[タグの管理](https://docs.tealium.com/manage-tags/)を参照してください。

タグを追加した後、以下の構成を構成します：

* **Tracking Key**: 楽天マーケティング統合担当者から発行されるサイト固有のトラッキングキー。
* **楽天アフィリエイトマーチャントID**: 4桁または5桁のマーチャントID。
* **税率**: パーセンテージ値での税率。例えば、イギリスのVATが20%の場合は `20`。
* **楽天ディスプレイマーチャントID**: 4桁のマーチャントID。
* **楽天サーチマーチャントID**: 検索構成 rsMID (`rsMID`)。
* **コンバージョンタイプ**: デフォルト値は `sale` ですが、任意の値に構成できます。
* **割引タイプ**: アフィリエイトセールスの割引タイプ。デフォルト値は `amount` ですが、`percentage` に構成することもできます。
* **Include Status**: タグに注文ステータスを含めるかどうか。デフォルト値は `true` です。

### データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

#### 標準

|変数| 説明|
|---| ---|
|`trackingKey`|  <ul><li>トラッキングキー</li></ul> |
|`siteSection`|  <ul><li>サイトセクション</li></ul> |
|`conversionType`|  <ul><li>コンバージョンタイプ</li></ul> |
|`customerStatus`|  <ul><li>顧客ステータス</li></ul> |
|`discountAmount`|  <ul><li>割引額</li></ul> |
|`optionalData`|  <ul><li>オプショナルデータ</li></ul> |

#### Eコマース

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID。</li><li>`_corder` を上書きします。</li></ul> |
|`order_subtotal`|  <ul><li>小計。</li><li>`_csubtotal` を上書きします。</li></ul> |
|`order_tax`|  <ul><li>税額。</li><li>`_ctax` を上書きします。</li></ul> |
|`order_currency`|  <ul><li>通貨。</li><li>`_ccurrency` を上書きします。</li></ul> |
|`order_coupon_code`|  <ul><li>プロモーションコード。</li><li>`_cpromo` を上書きします。</li></ul> |
|`order_consumed`|  <ul><li>消費済み。</li></ul> |
|`order_shipped_country`|  <ul><li>発送国。</li></ul> |
|`order_status`|  <ul><li>注文ステータス。</li><li>値は以下の通りです：<ul><li>既存</li><li>リターニング</li><li>新規</li></ul> </li></ul> |
| `order_shipped` |  <ul><li>発送済み。</li></ul> |
|`order_site_name`|  <ul><li>サイト名。</li></ul> |
|`customer_id`|  <ul><li>顧客ID。</li><li>`_ccustid` を上書きします。</li></ul> |
|`customer_score`|  <ul><li>顧客スコア。</li></ul> |
|`customer_country`|  <ul><li>顧客国。</li><li>`_ccountry` を上書きします。</li><li>`order_shipped_country` が提供されていない場合は、`order_shipped_country` の代わりに使用されます。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>製品IDリスト。</li><li>`product_sku` が提供されていない場合は、`product_sku` の代わりに使用されます。</li><li>`_cprod` を上書きします。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>名前リスト。</li><li>`_cprodname` を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量リスト。</li><li>`_cquan` を上書きします。</li></ul> |
|`product_sku`|  <ul><li>配列</li><li>SKUリスト。</li><li>`_csku` を上書きします。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格リスト。</li><li>`_cprice` を上書きします。</li></ul> |
|`product_discount`|  <ul><li>配列</li><li>割引リスト。</li><li>`_cpdisc` を上書きします。</li></ul> |
|`product_brand`|  <ul><li>配列</li><li>ブランドリスト。</li><li>`_cbrand` を上書きします。</li></ul> |
|`product_category`|  <ul><li>配列</li><li>カテゴリリスト。</li><li>`_ccat` を上書きします。</li></ul> |
|`product_category_id`|  <ul><li>配列</li><li>カテゴリIDリスト。</li></ul> |
|`product_coupon`|  <ul><li>配列</li><li>クーポンリスト。</li></ul> |
|`product_is_clearance`|  <ul><li>配列</li><li>クリアランスステータスリスト。</li></ul> |
|`product_is_sale`|  <ul><li>配列</li><li>セールスステータスリスト。</li></ul> |
|`product_margin`|  <ul><li>配列</li><li>マージンリスト。</li></ul> |

#### アフィリエイト

|変数| 説明|
|---| ---|
|`allowCommission`|  <ul><li>コミッション許可</li><li>値は `true` または `false`。</li></ul> |
|`affiliateConfig.ranMID`|  <ul><li>ranMID</li></ul> |
| `affiliateConfig.taxRate` |  <ul><li>税率</li></ul> |
| `affiliateConfig.discountType` |  <ul><li>割引タイプ</li></ul> |
|`affiliateConfig.tagType`|  <ul><li>タグタイプ</li></ul> |
|`affiliateConfig.includeStatus`|  <ul><li>ステータスを含む</li><li>値は `true` または `false`。</li></ul> |
|`affiliateConfig.removeOrderTax`|  <ul><li>注文税を除去</li><li>値は `true` または `false`。</li></ul> |
|`affiliateConfig.removeTaxFromProducts`|  <ul><li>製品から税を除去</li><li>値は `true` または `false`。</li></ul> |
|`affiliateConfig.removeTaxFromDiscount`|  <ul><li>割引から税を除去。</li><li>値は `true` または `false`。</li></ul> |
|`affiliateConfig.centValues`|  <ul><li>セント値。</li><li>値は `true` または `false`。</li></ul> |
|`affiliateConfig.nonCentCurrencies`|  <ul><li>非セント通貨。</li><li>通貨の配列またはカンマ区切りの通貨リストを含む文字列を受け入れることができます。</li></ul> |

#### ディスプレイ

|変数| 説明|
|---| ---|
|`displayConfig.rdMID`|  <ul><li>rdMID</li></ul> |
|`displayConfig.domain`|  <ul><li>ドメイン</li></ul> |
|`displayConfig.tagType`|  <ul><li>タグタイプ</li></ul> |
|`displayConfig.includeStatus`|  <ul><li>ステータスを含む</li></ul> |
|`displayConfig.allowCommission`|  <ul><li>コミッション許可</li></ul> |
|`displayConfig.removeTaxFromProducts`|  <ul><li>製品から税を除去</li><li>値は `true` または `false`。</li></ul> |
|`displayConfig.removeTaxFromDiscount`|  <ul><li>割引から税を除去</li><li>値は `true` または `false`。</li></ul> |
|`displayConfig.taxRate`|  <ul><li>税率</li></ul> |

#### 検索

|変数| 説明|
|---| ---|
|`searchConfig.rsMID`|  <ul><li>rsMID</li></ul> |
|`searchConfig.conversionType`|  <ul><li>コンバージョンタイプ</li></ul> |
|`searchConfig.accountID`|  <ul><li>アカウントID</li></ul> |
|`searchConfig.clickID`|  <ul><li>クリックID</li></ul> |
