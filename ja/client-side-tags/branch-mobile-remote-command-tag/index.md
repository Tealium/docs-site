---
title: Branch Mobileリモートコマンドタグ構成ガイド
description: この記事では、タグ管理アカウントでBranch Mobileリモートコマンドタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/branch-mobile-remote-command-tag/
---
Branchは、さまざまなデバイス、プラットフォーム、チャネル間でユーザーエクスペリエンスと測定を統合するソリューションを提供する、業界をリードするモバイルリンクプラットフォームです。

## タグに関するヒント

* マッピングを使用して、次の操作を行います。
  * 標準構成値を上書きし、カスタムパラメータを構成する
  * 標準イベントおよびカスタムイベントをトリガーする

* 次のEコマース拡張機能の値をサポートしています。
  * 通貨（`_ccurrency`）
  * 顧客ID（`_ccustid`）
  * プロモーションコード（`_cpromo`）
  * ブランドのリスト（`_cbrand`）
  * カテゴリのリスト（`_ccat`）
  * SKUのリスト（`_csku`）
  * 名前のリスト（`_cprodname`）
  * カテゴリ2のリスト（`_ccat2`）
  * 価格のリスト（`_cprice`）
  * 数量のリスト（`_cquan`）
  * 税額（`_ctax`）

* これは、ネイティブモバイルアプリSDK用のMobileリモートコマンドコンパニオンタグです。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を構成します。

* **Branchキー：**

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### リンク

| 変数                                           | 説明     |
|:-----------------------------------------------|:---------|
| チャネル（`link.channel`）                     | [文字列] |
| 機能（`link.feature`）                         | [文字列] |
| キャンペーン（`link.campaign`）                | [文字列] |
| ステージ（`link.stage`）                       | [文字列] |
| 期間（`link.duration`）                        | [文字列] |
| 制御パラメータ（`link.control_parameters`）    | [文字列] |

### 構成

| 変数                                               | 説明       |
|:---------------------------------------------------|:-----------|
| Branchキー（`dev_key`）                            | [文字列]   |
| ロギングを有効化（`settings.enable_logging`）      | [ブール値] |
| デバイスIDを収集（`settings.collect_device_id`）   | [ブール値] |

### イベント

| 変数                                                         | 説明     |
|:-------------------------------------------------------------|:---------|
| Tealiumイベント（`event.description`）                       | [文字列] |
| 顧客ID（`event.user_id`）（`_ccustid`を上書き）              | [文字列] |
| 商品数量（`event.quantity`）（`_cquan`を上書き）             | [文字列] |
| 通貨タイプ（`event.currency`）（`_ccurrency`を上書き）       | [文字列] |
| 注文税額（`event.tax`）（`_ctax`を上書き）                   | [数値]   |
| 収益（`event.revenue`）                                      | [数値]   |
| 検索クエリ（`event.search_query`）                            | [文字列] |

### BUO

| 変数                                        | 説明     |
|:--------------------------------------------|:---------|
| タイトル（`buo.title`）                     | [文字列] |
| 説明（`buo.description`）                   | [文字列] |
| アイテムID（`buo.canonical_identifier`）    | [文字列] |
| アイテムURL（`buo.canonical_url`）          | [文字列] |
| 画像URL（`buo.image_url`）                  | [文字列] |
| コンテンツメタデータ（`buo.content_metadata`） | [文字列] |

### メタデータ

| 変数                                                                  | 説明     |
|:----------------------------------------------------------------------|:---------|
| 緯度（`metadata.latitude`）                                           | [数値]   |
| 経度（`metadata.longitude`）                                          | [数値]   |
| 通貨コード（`metadata.currency_type`）（`_ccurrency`を上書き）        | [文字列] |
| クーポン（`metadata.coupon`）（`_cpromo`を上書き）                    | [文字列] |
| 商品ブランド（`metadata.product_brand`）（`_cbrand`を上書き）         | [文字列] |
| 商品カテゴリ（`metadata.product_category`）（`_ccat`を上書き）        | [文字列] |
| 商品ID（`metadata.sku`）（`_csku`を上書き）                           | [文字列] |
| 商品名（`metadata.product_name`）（`_cprodname`を上書き）             | [文字列] |
| 商品バリエーション（`metadata.product_variant`）（`_cprice`を上書き） | [文字列] |
| 商品単価（`metadata.price`）（`_ccustid`を上書き）                    | [数値]   |

### イベント

| 変数                                             | 説明                 |
|:-------------------------------------------------|:---------------------|
| 初期化（`initialize`）                           | initialize           |
| ユーザーIDを構成（`setuserid`）                  | setuserid            |
| ログアウト（`logout`）                           | logout               |
| ディープリンクを作成（`createdeeplink`）         | createdeeplink       |
| レベル達成（`achievelevel`）                     | achievelevel         |
| 支払い情報を追加（`addpaymentinfo`）             | addpaymentinfo       |
| カートに追加（`addtocart`）                      | addtocart            |
| ウィッシュリストに追加（`addtowishlist`）        | addtowishlist        |
| チュートリアル完了（`completetutorial`）         | completetutorial     |
| 広告をクリック（`clickad`）                      | clickad              |
| 登録完了（`completeregistration`）               | completeregistration |
| ストリーム完了（`completestream`）               | completestream       |
| 購入開始（`initiatepurchase`）                   | initiatepurchase     |
| ストリーム開始（`initiatestream`）               | initiatestream       |
| 招待（`invite`）                                 | invite               |
| ログイン（`login`）                              | login                |
| 購入（`purchase`）                               | purchase             |
| 評価（`rate`）                                   | rate                 |
| 予約（`reserve`）                                | reserve              |
| 検索（`search`）                                 | search               |
| 共有（`share`）                                  | share                |
| クレジットを使用（`spendcredits`）               | spendcredits         |
| トライアル開始（`starttrial`）                   | starttrial           |
| サブスクリプション登録（`subscribe`）            | subscribe            |
| 実績を解除（`unlockachievement`）                | unlockachievement    |
| 広告を表示（`viewad`）                           | viewad               |
| カートを表示（`viewcart`）                       | viewcart             |
| アイテムを表示（`viewitem`）                     | viewitem             |
| 複数のアイテムを表示（`viewitems`）              | viewitems            |
| カスタム                                         | custom               |
### イベントパラメータ

| 変数                                         | 説明                 |
|:---------------------------------------------|:---------------------|
| 初期化 (`initialize`)                         | initialize           |
| ユーザー ID の構成 (`setuserid`)              | setuserid            |
| ログアウト (`logout`)                         | logout               |
| ディープリンクの作成 (`createdeeplink`)       | createdeeplink       |
| レベルの達成 (`achievelevel`)                 | achievelevel         |
| 支払い情報の追加 (`addpaymentinfo`)           | addpaymentinfo       |
| カートへの追加 (`addtocart`)                  | addtocart            |
| ウィッシュリストへの追加 (`addtowishlist`)    | addtowishlist        |
| チュートリアルの完了 (`completetutorial`)     | completetutorial     |
| 広告のクリック (`clickad`)                    | clickad              |
| 登録の完了 (`completeregistration`)           | completeregistration |
| ストリームの完了 (`completestream`)           | completestream       |
| 購入の開始 (`initiatepurchase`)               | initiatepurchase     |
| ストリームの開始 (`initiatestream`)           | initiatestream       |
| 招待 (`invite`)                               | invite               |
| ログイン (`login`)                            | login                |
| 購入 (`purchase`)                             | purchase             |
| 評価 (`rate`)                                 | rate                 |
| 予約 (`reserve`)                              | reserve              |
| 検索 (`search`)                               | search               |
| 共有 (`share`)                                | share                |
| クレジットの使用 (`spendcredits`)             | spendcredits         |
| トライアルの開始 (`starttrial`)               | starttrial           |
| サブスクリプション登録 (`subscribe`)          | subscribe            |
| 実績の解除 (`unlockachievement`)              | unlockachievement    |
| 広告の表示 (`viewad`)                         | viewad               |
| カートの表示 (`viewcart`)                     | viewcart             |
| アイテムの表示 (`viewitem`)                   | viewitem             |
| 複数アイテムの表示 (`viewitems`)              | viewitems            |
| カスタム                                      | custom               |