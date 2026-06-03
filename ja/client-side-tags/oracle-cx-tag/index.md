---
title: Oracle CXタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでOracle CXタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/oracle-cx-tag/
---
## タグのヒント

* 以下のE-Commerce拡張パラメータをサポートしています:
  * 注文ID (`_corder`)
  * 製品IDのリスト (`_cprod`)
  * 製品SKUのリスト (`_csku`)
  * 製品数量のリスト (`_cquan`)
  * 注文合計 (`_ctotal`)
  * 小計 (`_csubtotal`)
  * 送料 (`_cship`)
  * 税金 (`_ctax`)
  * 通貨 (`_ccurrency`)
  * プロモーションコード (`_cpromo`)
  * 名前のリスト (`_cprodname`)
  * ブランドのリスト (`_cbrand`)
  * カテゴリのリスト (`_ccat`)
  * カテゴリ2のリスト (`_ccat2`)
  * 価格のリスト (`_cprice`)
  * 割引のリスト (`_cpdisc`)

## タグの構成

まず、タグマーケットプレイスに移動し、Oracle CXタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います:

* **アカウントID**
  * あなたのOracle InfinityアカウントID。

* **タグID**
  * あなたのOracle InfinityタグID。

* **コンテキスト**
  * 任意
  * あなたのOracle Infinityタグのコンテキスト。
  * 例: `analytics:dev`

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。タグ宛先に変数をマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです:

### スタンダード

|変数| 説明|
|---| ---|
|`account_guid`| アカウントID|
|`tag_id`| タグID|
|`context`| コンテキスト|

### クリックトラッキング構成

|変数| 説明|
|---| ---|
|`successCallback`| 成功時のコールバック関数|
|`failCallback`| 失敗時のコールバック関数|
|`mutation`| 変異関数|
|`wt.dl`| イベントID|

### コマース

|変数| 説明|
|---| ---|
|`wt.tx_i`| 請求書番号|
|`wt.tx_id`| 請求書日付|
|`wt.tx_it`| 請求書時間|
|`wt.mc_id`| キャンペーンID|
|`wt.mc_ev`| キャンペーンイベント|
|`wt.conv`| コンバージョン名|
|`wt.pn_sku`| 製品SKU|
|`wt.pn_id`| 製品識別子|
|`wt.pn_fa`| 製品ファミリー|
|`wt.pn_gr`| 製品グループ|
|`wt.pn_sc`| 製品サブグループ|
|`wt.pn_ma`| 製品製造者|
|`wt.pn_su`| 製品供給者|
|`wt.product_coupon`| クーポンコード|
|`wt.product_name`| 製品名|
|`wt.pn_gr`| 製品グループ|
|`wt.pn_sc`| 製品サブグループ|
|`wt.product_price`| 製品価格|
|`wt.product_discount`| 製品単位の割引|
|`wt.cart_total`| カート合計|
|`wt.cart_subtotal`| カート小計|
|`wt.cart_shipping`| カート送料|
|`wt.cart_tax`| カート税金|
|`wt.currency`| 通貨|
|`wt.si_cs`| コンバージョンステップ|
|`wt.si_n`| シナリオ名|
|`wt.si_p`| シナリオステップ名|
|`wt.si_x`| シナリオステップ番号|
|`wt.tx_cartid`|  &lt;ul&gt;&lt;li&gt;カートID&lt;/li&gt;&lt;li&gt;`_corder`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`wt.tx_s`| トランザクション小計|
|`wt.tx_u`| 単位|
|`wt.tx_e`| トランザクションイベントタイプ|

### トランザクションイベントタイプ

|変数| 説明|
|---| ---|
|`a`| カート追加|
|`p`| 購入|
|`r`| カート削除|
|`v`| 製品表示|
|Custom| カスタム|

### コンテンツ

|変数| 説明|
|---| ---|
|`wt.cg_n`| コンテンツグループ名|
|`wt.cg_s`| コンテンツサブグループ名|
|`wt.ti`| ページタイトル|
|`page-uri`| ページURI|
|`wt.es`| ページURL|
|`domain`| ドメイン|
|`wt.oss`| サイト内検索フレーズ|
|`wt.oss_r`| サイト内検索成功|

### モバイルWebとアプリ

|変数| 説明|
|---| ---|
|`wt.a_ac`| アプリ広告クリック|
|`wt.a_ai`| アプリ広告インプレッション|
|`wt.a_an`| アプリ広告名|
|`wt.a_pub`| アプリ公開社|
|`wt.ct`| 接続タイプ|
|`wt.g_co`| 発信国|
|`wt.dm`| デバイスモデル|
|`wt.ets`| イベントタイムスタンプ|
|`wt.gc`| ジオロケーション座標|
|`wt.sys`| モバイルアプリイベントタイプ|
|`wt.a_nm`| モバイルアプリ名|
|`wt.av`| モバイルアプリバージョン|
|`wt.a_dc`| モバイルキャリア|
|`wt.sdk_v`| モバイルSDKビルド|

### トラフィックソース

|変数| 説明|
|---| ---|
|`referrer`| リファラー|
|`referrer-domain`| リファリングドメイン|
|`referrer-path`| リファリングURI|
