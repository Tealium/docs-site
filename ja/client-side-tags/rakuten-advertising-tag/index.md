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

まず、Tealiumのタグマーケットプレイスにアクセスして、楽天マーケティングタグを追加します。詳細については、[タグの管理]()を参照してください。

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

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

#### 標準

|変数| 説明|
|---| ---|
|`trackingKey`|  &lt;ul&gt;&lt;li&gt;トラッキングキー&lt;/li&gt;&lt;/ul&gt; |
|`siteSection`|  &lt;ul&gt;&lt;li&gt;サイトセクション&lt;/li&gt;&lt;/ul&gt; |
|`conversionType`|  &lt;ul&gt;&lt;li&gt;コンバージョンタイプ&lt;/li&gt;&lt;/ul&gt; |
|`customerStatus`|  &lt;ul&gt;&lt;li&gt;顧客ステータス&lt;/li&gt;&lt;/ul&gt; |
|`discountAmount`|  &lt;ul&gt;&lt;li&gt;割引額&lt;/li&gt;&lt;/ul&gt; |
|`optionalData`|  &lt;ul&gt;&lt;li&gt;オプショナルデータ&lt;/li&gt;&lt;/ul&gt; |

#### Eコマース

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文ID。&lt;/li&gt;&lt;li&gt;`_corder` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;小計。&lt;/li&gt;&lt;li&gt;`_csubtotal` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;税額。&lt;/li&gt;&lt;li&gt;`_ctax` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_currency`|  &lt;ul&gt;&lt;li&gt;通貨。&lt;/li&gt;&lt;li&gt;`_ccurrency` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_coupon_code`|  &lt;ul&gt;&lt;li&gt;プロモーションコード。&lt;/li&gt;&lt;li&gt;`_cpromo` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`order_consumed`|  &lt;ul&gt;&lt;li&gt;消費済み。&lt;/li&gt;&lt;/ul&gt; |
|`order_shipped_country`|  &lt;ul&gt;&lt;li&gt;発送国。&lt;/li&gt;&lt;/ul&gt; |
|`order_status`|  &lt;ul&gt;&lt;li&gt;注文ステータス。&lt;/li&gt;&lt;li&gt;値は以下の通りです：&lt;ul&gt;&lt;li&gt;既存&lt;/li&gt;&lt;li&gt;リターニング&lt;/li&gt;&lt;li&gt;新規&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
| `order_shipped` |  &lt;ul&gt;&lt;li&gt;発送済み。&lt;/li&gt;&lt;/ul&gt; |
|`order_site_name`|  &lt;ul&gt;&lt;li&gt;サイト名。&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;顧客ID。&lt;/li&gt;&lt;li&gt;`_ccustid` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`customer_score`|  &lt;ul&gt;&lt;li&gt;顧客スコア。&lt;/li&gt;&lt;/ul&gt; |
|`customer_country`|  &lt;ul&gt;&lt;li&gt;顧客国。&lt;/li&gt;&lt;li&gt;`_ccountry` を上書きします。&lt;/li&gt;&lt;li&gt;`order_shipped_country` が提供されていない場合は、`order_shipped_country` の代わりに使用されます。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品IDリスト。&lt;/li&gt;&lt;li&gt;`product_sku` が提供されていない場合は、`product_sku` の代わりに使用されます。&lt;/li&gt;&lt;li&gt;`_cprod` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;名前リスト。&lt;/li&gt;&lt;li&gt;`_cprodname` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量リスト。&lt;/li&gt;&lt;li&gt;`_cquan` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_sku`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;SKUリスト。&lt;/li&gt;&lt;li&gt;`_csku` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格リスト。&lt;/li&gt;&lt;li&gt;`_cprice` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_discount`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;割引リスト。&lt;/li&gt;&lt;li&gt;`_cpdisc` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_brand`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;ブランドリスト。&lt;/li&gt;&lt;li&gt;`_cbrand` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;カテゴリリスト。&lt;/li&gt;&lt;li&gt;`_ccat` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_category_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;カテゴリIDリスト。&lt;/li&gt;&lt;/ul&gt; |
|`product_coupon`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;クーポンリスト。&lt;/li&gt;&lt;/ul&gt; |
|`product_is_clearance`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;クリアランスステータスリスト。&lt;/li&gt;&lt;/ul&gt; |
|`product_is_sale`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;セールスステータスリスト。&lt;/li&gt;&lt;/ul&gt; |
|`product_margin`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;マージンリスト。&lt;/li&gt;&lt;/ul&gt; |

#### アフィリエイト

|変数| 説明|
|---| ---|
|`allowCommission`|  &lt;ul&gt;&lt;li&gt;コミッション許可&lt;/li&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.ranMID`|  &lt;ul&gt;&lt;li&gt;ranMID&lt;/li&gt;&lt;/ul&gt; |
| `affiliateConfig.taxRate` |  &lt;ul&gt;&lt;li&gt;税率&lt;/li&gt;&lt;/ul&gt; |
| `affiliateConfig.discountType` |  &lt;ul&gt;&lt;li&gt;割引タイプ&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.tagType`|  &lt;ul&gt;&lt;li&gt;タグタイプ&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.includeStatus`|  &lt;ul&gt;&lt;li&gt;ステータスを含む&lt;/li&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.removeOrderTax`|  &lt;ul&gt;&lt;li&gt;注文税を除去&lt;/li&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.removeTaxFromProducts`|  &lt;ul&gt;&lt;li&gt;製品から税を除去&lt;/li&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.removeTaxFromDiscount`|  &lt;ul&gt;&lt;li&gt;割引から税を除去。&lt;/li&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.centValues`|  &lt;ul&gt;&lt;li&gt;セント値。&lt;/li&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
|`affiliateConfig.nonCentCurrencies`|  &lt;ul&gt;&lt;li&gt;非セント通貨。&lt;/li&gt;&lt;li&gt;通貨の配列またはカンマ区切りの通貨リストを含む文字列を受け入れることができます。&lt;/li&gt;&lt;/ul&gt; |

#### ディスプレイ

|変数| 説明|
|---| ---|
|`displayConfig.rdMID`|  &lt;ul&gt;&lt;li&gt;rdMID&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.domain`|  &lt;ul&gt;&lt;li&gt;ドメイン&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.tagType`|  &lt;ul&gt;&lt;li&gt;タグタイプ&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.includeStatus`|  &lt;ul&gt;&lt;li&gt;ステータスを含む&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.allowCommission`|  &lt;ul&gt;&lt;li&gt;コミッション許可&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.removeTaxFromProducts`|  &lt;ul&gt;&lt;li&gt;製品から税を除去&lt;/li&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.removeTaxFromDiscount`|  &lt;ul&gt;&lt;li&gt;割引から税を除去&lt;/li&gt;&lt;li&gt;値は `true` または `false`。&lt;/li&gt;&lt;/ul&gt; |
|`displayConfig.taxRate`|  &lt;ul&gt;&lt;li&gt;税率&lt;/li&gt;&lt;/ul&gt; |

#### 検索

|変数| 説明|
|---| ---|
|`searchConfig.rsMID`|  &lt;ul&gt;&lt;li&gt;rsMID&lt;/li&gt;&lt;/ul&gt; |
|`searchConfig.conversionType`|  &lt;ul&gt;&lt;li&gt;コンバージョンタイプ&lt;/li&gt;&lt;/ul&gt; |
|`searchConfig.accountID`|  &lt;ul&gt;&lt;li&gt;アカウントID&lt;/li&gt;&lt;/ul&gt; |
|`searchConfig.clickID`|  &lt;ul&gt;&lt;li&gt;クリックID&lt;/li&gt;&lt;/ul&gt; |
