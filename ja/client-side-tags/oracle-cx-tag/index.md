---
title: Oracle CXタグ構成ガイド
description: この記事では、タグ管理アカウントでOracle CX Tagタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/oracle-cx-tag/
---
## タグに関するヒント

* 次のEコマース拡張パラメータをサポートしています。
  * 注文ID（`_corder`）
  * 商品IDのリスト（`_cprod`）
  * 商品SKUのリスト（`_csku`）
  * 商品数量のリスト（`_cquan`）
  * 注文合計（`_ctotal`）
  * 小計（`_csubtotal`）
  * 配送料（`_cship`）
  * 税額（`_ctax`）
  * 通貨（`_ccurrency`）
  * プロモーションコード（`_cpromo`）
  * 商品名のリスト（`_cprodname`）
  * ブランドのリスト（`_cbrand`）
  * カテゴリのリスト（`_ccat`）
  * カテゴリ2のリスト（`_ccat2`）
  * 価格のリスト（`_cprice`）
  * 割引のリスト（`_cpdisc`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を行います。

* **アカウントID**
  * Oracle InfinityのアカウントID。

* **タグID**
  * Oracle InfinityのタグID。

* **コンテキスト**
  * 任意
  * Oracle Infinityタグのコンテキスト。
  * 例：`analytics:dev`

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`account_guid`|アカウントID|
|`tag_id`|タグID|
|`context`|コンテキスト|

### クリックトラッキング構成

|変数|説明|
|---|---|
|`successCallback`|成功時のコールバック関数|
|`failCallback`|失敗時のコールバック関数|
|`mutation`|変更関数|
|`wt.dl`|イベントID|

### コマース

|変数|説明|
|---|---|
|`wt.tx_i`|請求書番号|
|`wt.tx_id`|請求書の日付|
|`wt.tx_it`|請求書の時刻|
|`wt.mc_id`|キャンペーンID|
|`wt.mc_ev`|キャンペーンイベント|
|`wt.conv`|コンバージョン名|
|`wt.pn_sku`|商品SKU|
|`wt.pn_id`|商品識別子|
|`wt.pn_fa`|商品ファミリー|
|`wt.pn_gr`|商品グループ|
|`wt.pn_sc`|商品サブグループ|
|`wt.pn_ma`|商品メーカー|
|`wt.pn_su`|商品サプライヤー|
|`wt.product_coupon`|クーポンコード|
|`wt.product_name`|商品名|
|`wt.pn_gr`|商品グループ|
|`wt.pn_sc`|商品サブグループ|
|`wt.product_price`|商品価格|
|`wt.product_discount`|商品単価の割引額|
|`wt.cart_total`|カート合計|
|`wt.cart_subtotal`|カート小計|
|`wt.cart_shipping`|カートの配送料|
|`wt.cart_tax`|カートの税額|
|`wt.currency`|通貨|
|`wt.si_cs`|コンバージョンステップ|
|`wt.si_n`|シナリオ名|
|`wt.si_p`|シナリオステップ名|
|`wt.si_x`|シナリオステップ番号|
|`wt.tx_cartid`| <ul><li>カートID</li><li>`_corder`を上書きします。</li></ul> |
|`wt.tx_s`|取引小計|
|`wt.tx_u`|単位数|
|`wt.tx_e`|取引イベントタイプ|

### 取引イベントタイプ

|変数|説明|
|---|---|
|`a`|カートへの追加|
|`p`|購入|
|`r`|カートからの削除|
|`v`|商品の表示|
|カスタム|カスタム|

### コンテンツ

|変数|説明|
|---|---|
|`wt.cg_n`|コンテンツグループ名|
|`wt.cg_s`|コンテンツサブグループ名|
|`wt.ti`|ページタイトル|
|`page-uri`|ページURI|
|`wt.es`|ページURL|
|`domain`|ドメイン|
|`wt.oss`|サイト内検索語句|
|`wt.oss_r`|サイト内検索の成功|

### モバイルWebとアプリ

|変数|説明|
|---|---|
|`wt.a_ac`|アプリ広告のクリック|
|`wt.a_ai`|アプリ広告のインプレッション|
|`wt.a_an`|アプリ広告名|
|`wt.a_pub`|アプリのパブリッシャー|
|`wt.ct`|接続タイプ|
|`wt.g_co`|送信元の国|
|`wt.dm`|デバイスモデル|
|`wt.ets`|イベントのタイムスタンプ|
|`wt.gc`|位置情報の座標|
|`wt.sys`|モバイルアプリのイベントタイプ|
|`wt.a_nm`|モバイルアプリ名|
|`wt.av`|モバイルアプリのバージョン|
|`wt.a_dc`|モバイル通信事業者|
|`wt.sdk_v`|モバイルSDKビルド|

### トラフィックソース

|変数|説明|
|---|---|
|`referrer`|リファラー|
|`referrer-domain`|参照元ドメイン|
|`referrer-path`|参照元URI|