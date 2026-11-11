---
title: LivePerson LiveEngage 2.0タグ構成ガイド
description: この記事では、LivePerson LiveEngage 2.0タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/liveperson-liveengage-tag/
---
チャット、音声、コンテンツ向けのリアルタイムソリューションと、あらゆるオープンAPIを使用して訪問にプロアクティブに働きかけ、顧客ライフサイクル全体を通じてパーソナライズされたユーザーエクスペリエンスを提供します。

## タグに関するヒント

マッピングを使用すると、標準構成値を動的に上書きできます。

* 現在のライブラリバージョン：1.10
* 次のEコマース変数を使用します
  * `_corder`
  * `_ctotal`
  * `_ccustid`
  * `_cprodname`
  * `_ccat`
  * `_csku`
  * `_cquan`
  * `_cprice`

* マーケティングソース - チャネル
  * `0`-直接
  * `1`-検索
  * `2`-ソーシャル
  * `3`-メール
  * `4`-参照
  * `5`-有料検索
  * `6`-ディスプレイ

* サービス - ステータス
  * `0`-完了
  * `1`-進行中
  * `2`-承認済み
  * `3`-キャンセル済み
  * `4`-未承認
  * `5`-レビュー済み
  * `6`-詳細情報不足
  * `7`-クローズ済み
  * `8`-削除済み
  * `9`-割り当て済み

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **サイトID**：サイトの値（例：`23954343`）
* **セクション**：セクション値のカンマ区切りリスト
* **マッピングを許可**：
  * `True` - サイトIDのマッピングを許可し、送信時にライブラリを読み込む  
  * `False` - タグの読み込み時にライブラリを読み込む
* **Eコマースを統合**：
  * `True` - すべてのマッピングの基礎としてEコマース拡張機能を使用する  
  * `False` - データベースとしてEコマース拡張機能を使用しない

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|サイトID| (`site`)|
|イベントタイプ| (`type`)|
|セクション (`section`)| [配列/CSV]|
|タグレット| (`taglets`)|
|ページURL| (`page_url`)（`dom.url`を上書き）|

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

|変数| 説明|
|---| ---|
|カート (`cart`)| `cart`|
|購入 (`purchase`)| `purchase`|
|商品表示 (`prodView`)| `prodView`|
|顧客情報 (`ctmrinfo`)| `ctmrinfo`|
|マーケティングソース (`mrktinfo`)| `mrktinfo`|
|個人情報 (`personal`)| `personal`|
|リード (`lead`)| `lead`|
|サービス (`service`)| `service`|
|検索 (`searchInfo`)| `searchInfo`|
|エラー (`error`)| `error`|

### Eコマース

|変数| 説明|
|---| ---|
|注文ID| (`order_id`)（`_corder`を上書き）|
|注文合計| (`order_total`)（`_ctotal`を上書き）|
|名前のリスト (`product_name`)（`_cprodname`を上書き）| [配列]|
|SKUのリスト (`product_sku`)（`_csku`を上書き）| [配列]|
|カテゴリーのリスト (`product_category`)（`_ccat`を上書き）| [配列]|
|数量のリスト (`product_quantity`)（`_cquan`を上書き）| [配列]|
|価格のリスト (`product_unit_price`)（`_cprice`を上書き）| [配列]|

### カートEコマース

|変数| 説明|
|---| ---|
|注文合計| (`cart.order_total`)（`_ctotal`を上書き）|
|名前のリスト (`cart.product_name`)（`_cprodname`を上書き）| [配列]|
|SKUのリスト (`cart.product_sku`)（`_csku`を上書き）| [配列]|
|カテゴリーのリスト (`cart.product_category`)（`_ccat`を上書き）| [配列]|
|数量のリスト (`cart.product_quantity`)（`_cquan`を上書き）| [配列]|
|価格のリスト (`cart.product_unit_price`)（`_cprice`を上書き）| [配列]|

### 購入Eコマース

|変数| 説明|
|---| ---|
|注文ID| (`purchase.order_id`)（`_corder`を上書き）|
|注文合計| (`purchase.order_total`)（`_ctotal`を上書き）|
|名前のリスト (`purchase.product_name`)（`_cprodname`を上書き）| [配列]|
|SKUのリスト (`purchase.product_sku`)（`_csku`を上書き）| [配列]|
|カテゴリーのリスト (`purchase.product_category`)（`_ccat`を上書き）| [配列]|
|数量のリスト (`purchase.product_quantity`)（`_cquan`を上書き）| [配列]|
|価格のリスト (`purchase.product_unit_price`)（`_cprice`を上書き）| [配列]|

### 商品表示Eコマース

|変数| 説明|
|---| ---|
|名前のリスト (`prodView.product_name`)（`_cprodname`を上書き）| [配列]|
|SKUのリスト (`prodView.product_sku`)（`_csku`を上書き）| [配列]|
|カテゴリーのリスト (`prodView.product_category`)（`_ccat`を上書き）| [配列]|
|価格のリスト (`prodView.product_unit_price`)（`_cprice`を上書き）| [配列]|

### 顧客情報

|変数| 説明|
|---| ---|
|顧客ID| (`customer_id`)（`_ccustid`を上書き）|
|顧客ライフサイクルステータス| (`vi.cstatus`)|
|顧客タイプ| (`vi.ctype`)|
|財務残高 (`vi.balance`)| [浮動小数点数]|
|ソーシャルID| (`vi.socialId`)|
|一意のデバイスまたは電話識別子| (`vi.imei`)|
|ユーザー名| (`vi.userName`)|
|会社規模 (`vi.companySize`)| [整数]|
|会社名| (`vi.accountName`)|
|役割/役職| (`vi.role`)|
|最終支払日 - 日 (`vi.lpd_day`)| [整数]|
|最終支払日 - 月 (`vi.lpd_month`)| [整数]|
|最終支払日 - 年 (`vi.lpd_year`)| [整数]|
|登録日 - 日 (`vi.rd_day`)| [整数]|
|登録日 - 月 (`vi.rd_month`)| [整数]|
|登録日 - 年 (`vi.rd_year`)| [整数]|

### マーケティングソース

|変数| 説明|
|---| ---|
|チャネル| (`ms.channel`)|
|アフィリエイト| (`ms.affiliate`)|
|キャンペーンID| (`ms.campaignId`)|

### 個人情報

|変数| 説明|
|---| ---|
|名| (`per.firstname`)|
|姓| (`per.lastname`)|
|年齢| (`per.age`)|
|出生年| (`per.year`)|
|出生月| (`per.month`)|
|出生日| (`per.day`)|
|メールアドレス| (`per.email`)|
|電話番号| (`per.phone`)|
|性別| (`per.gender`)|
|会社| (`per.company`)|
|言語| (`per.language`)|

### リード

|変数| 説明|
|---| ---|
|トピック| (`lead.topic`)|
|値| (`lead.value`)|
|リードID| (`lead.id`)|

### サービス

|変数| 説明|
|---| ---|
|トピック| (`serv.topic`)|
|ステータス| (`serv.status`)|
|カテゴリー| (`serv.category`)|
|サービスID| (`serv.id`)|

### 検索

|変数| 説明|
|---| ---|
|検索キーワード| (`search.keywords`)|

### エラー

|変数| 説明|
|---| ---|
|メッセージ| (`err.msg`)|
|コード| (`err.code`)|