---
title: Branch Mobile Remote Commandタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでBranch Mobile Remote Commandタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/branch-mobile-remote-command-tag/
---
Branchは、異なるデバイス、プラットフォーム、チャネル間でユーザーエクスペリエンスと測定を統一するソリューションを提供する、業界をリードするモバイルリンクプラットフォームを提供しています。

## タグのヒント

* マッピングを使用して：
  * 標準的な構成値を上書きし、カスタムパラメータを構成する
  * 標準的なイベントとカスタムイベントをトリガーする

* 以下のE-Commerce拡張値をサポートしています：
  * 通貨 (`_ccurrency`)
  * 顧客ID (`_ccustid`)
  * プロモコード (`_cpromo`)
  * ブランドのリスト (`_cbrand`)
  * カテゴリのリスト (`_ccat`)
  * SKUのリスト (`_csku`)
  * 名前のリスト (`_cprodname`)
  * カテゴリ2のリスト (`_ccat2`)
  * 価格のリスト (`_cprice`)
  * 数量のリスト (`_cquan`)
  * 税額 (`_ctax`)

* これは、ネイティブモバイルアプリSDKのMobile Remote Commandコンパニオンタグです。

## タグ構成

まず、タグマーケットプレイスに移動し、Branch Mobile Remote Commandタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **Branch Key:**

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### リンク

| 変数                                       | 説明 |
|:-----------------------------------------------|:------------|
| チャネル (`link.channel`)                       | [文字列]    |
| 機能 (`link.feature`)                       | [文字列]    |
| キャンペーン (`link.campaign`)                     | [文字列]    |
| ステージ (`link.stage`)                           | [文字列]    |
| 期間 (`link.duration`)                     | [文字列]    |
| 制御パラメータ (`link.control_parameters`) | [文字列]    |

### 構成

| 変数                                         | 説明 |
|:-------------------------------------------------|:------------|
| Branch Key (`dev_key`)                           | [文字列]    |
| ロギングを有効にする (`settings.enable_logging`)       | [ブール値]   |
| デバイスIDを収集する (`settings.collect_device_id`) | [ブール値]   |

### イベント

| 変数                                                  | 説明 |
|:----------------------------------------------------------|:------------|
| Tealiumイベント (`event.description`)                       | [文字列]    |
| 顧客ID (`event.user_id`) (Overrides `_ccustid`)      | [文字列]    |
| 商品数量 (`event.quantity`) (Overrides `_cquan`)  | [文字列]    |
| 通貨タイプ (`event.currency`) (Overrides `_ccurrency`) | [文字列]    |
| 注文税 (`event.tax`) (Overrides `_ctax`)               | [数値]    |
| 収益 (`event.revenue`)                                 | [数値]    |
| 検索クエリ (`event.search_query`)                       | [文字列]    |

### Buo

| 変数                                | 説明 |
|:----------------------------------------|:------------|
| タイトル (`buo.title`)                       | [文字列]    |
| 説明 (`buo.description`)           | [文字列]    |
| アイテムID (`buo.canonical_identifier`)      | [文字列]    |
| アイテムURL (`buo.canonical_url`)            | [文字列]    |
| 画像URL (`buo.image_url`)               | [文字列]    |
| コンテンツメタデータ (`buo.content_metadata`) | [文字列]    |

### メタデータ

| 変数                                                       | 説明 |
|:---------------------------------------------------------------|:------------|
| 緯度 (`metadata.latitude`)                                   | [数値]    |
| 経度 (`metadata.longitude`)                                 | [数値]    |
| 通貨コード (`metadata.currency_type`) (Overrides `_ccurrency`)  | [文字列]    |
| クーポン (`metadata.coupon`) (Overrides `_cpromo`)                   | [文字列]    |
| 商品ブランド (`metadata.product_brand`) (Overrides `_cbrand`)     | [文字列]    |
| 商品カテゴリ (`metadata.product_category`) (Overrides `_ccat`) | [文字列]    |
| 商品ID (`metadata.sku`) (Overrides `_csku`)                    | [文字列]    |
| 商品名 (`metadata.product_name`) (Overrides `_cprodname`)    | [文字列]    |
| 商品バリアント (`metadata.product_variant`) (Overrides `_cprice`) | [文字列]    |
| 商品単価 (`metadata.price`) (Overrides `_ccustid`)      | [数値]    |

### イベント

| 変数                                     | 説明          |
|:---------------------------------------------|:---------------------|
| 初期化 (`initialize`)                      | initialize           |
| ユーザーIDの構成 (`setuserid`)                      | setuserid            |
| ログアウト (`logout`)                              | logout               |
| ディープリンクの作成 (`createdeeplink`)            | createdeeplink       |
| レベル達成 (`achievelevel`)                 | achievelevel         |
| 支払い情報の追加 (`addpaymentinfo`)            | addpaymentinfo       |
| カートに追加 (`addtocart`)                      | addtocart            |
| ウィッシュリストに追加 (`addtowishlist`)             | addtowishlist        |
| チュートリアル完了 (`completetutorial`)         | completetutorial     |
| 広告クリック (`clickad`)                           | clickad              |
| 登録完了 (`completeregistration`) | completeregistration |
| ストリーム完了 (`completestream`)             | completestream       |
| 購入開始 (`initiatepurchase`)         | initiatepurchase     |
| ストリーム開始 (`initiatestream`)             | initiatestream       |
| 招待 (`invite`)                              | invite               |
| ログイン (`login`)                                | login                |
| 購入 (`purchase`)                          | purchase             |
| 評価 (`rate`)                                  | rate                 |
| 予約 (`reserve`)                            | reserve              |
| 検索 (`search`)                              | search               |
| 共有 (`share`)                                | share                |
| クレジット消費 (`spendcredits`)                 | spendcredits         |
| トライアル開始 (`starttrial`)                     | starttrial           |
| 購読 (`subscribe`)                        | subscribe            |
| 実績解除 (`unlockachievement`)       | unlockachievement    |
| 広告表示 (`viewad`)                             | viewad               |
| カート表示 (`viewcart`)                         | viewcart             |
| アイテム表示 (`viewitem`)                         | viewitem             |
| アイテム表示 (`viewitems`)                       | viewitems            |
| カスタム                                       | custom               |

### イベントパラメータ

| 変数                                     | 説明          |
|:---------------------------------------------|:---------------------|
| 初期化 (`initialize`)                      | initialize           |
| ユーザーIDの構成 (`setuserid`)                      | setuserid            |
| ログアウト (`logout`)                              | logout               |
| ディープリンクの作成 (`createdeeplink`)            | createdeeplink       |
| レベル達成 (`achievelevel`)                 | achievelevel         |
| 支払い情報の追加 (`addpaymentinfo`)            | addpaymentinfo       |
| カートに追加 (`addtocart`)                      | addtocart            |
| ウィッシュリストに追加 (`addtowishlist`)             | addtowishlist        |
| チュートリアル完了 (`completetutorial`)         | completetutorial     |
| 広告クリック (`clickad`)                           | clickad              |
| 登録完了 (`completeregistration`) | completeregistration |
| ストリーム完了 (`completestream`)             | completestream       |
| 購入開始 (`initiatepurchase`)         | initiatepurchase     |
| ストリーム開始 (`initiatestream`)             | initiatestream       |
| 招待 (`invite`)                              | invite               |
| ログイン (`login`)                                | login                |
| 購入 (`purchase`)                          | purchase             |
| 評価 (`rate`)                                  | rate                 |
| 予約 (`reserve`)                            | reserve              |
| 検索 (`search`)                              | search               |
| 共有 (`share`)                                | share                |
| クレジット消費 (`spendcredits`)                 | spendcredits         |
| トライアル開始 (`starttrial`)                     | starttrial           |
| 購読 (`subscribe`)                        | subscribe            |
| 実績解除 (`unlockachievement`)       | unlockachievement    |
| 広告表示 (`viewad`)                             | viewad               |
| カート表示 (`viewcart`)                         | viewcart             |
| アイテム表示 (`viewitem`)                         | viewitem             |
| アイテム表示 (`viewitems`)                       | viewitems            |
| カスタム                                       | custom               |
