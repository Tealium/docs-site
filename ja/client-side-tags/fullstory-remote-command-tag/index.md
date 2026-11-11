---
title: FullStoryリモートコマンドタグ構成ガイド
description: この記事では、タグ管理アカウントでFullStoryリモートコマンドタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/fullstory-remote-command-tag/
---
FullStoryは、すべての顧客体験データを、強力で使いやすい1つのプラットフォームに収集します。FullStoryの軽量なスクリプトにより、ピクセル単位で正確なセッション再生、自動インサイト、ファネル分析、強力な検索およびセグメンテーションが利用可能になり、組織の全員が顧客にとって最良のオンライン体験を構築できるようになります。

## タグに関するヒント

* マッピングを使用してイベントをトリガーします。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `uid`  | 文字列 | UID |
|  `user_variables.email_str`  | 文字列 | メールアドレス |
|  `user_variables.phone_str`  | 文字列 | 電話番号 |
|  `tealium_event`  | 文字列 | Tealiumイベント |

### Eコマース

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `event.cart_id_str`  | 文字列 | カートID |
| `event.product_id_str`  | 文字列 | 製品ID |
|  `event.price_real`  | 数値 | 実価格 |
|  `event.name_str`  | 文字列 | 名前 |
|  `event.categoryProperties`  | 文字列 | カテゴリープロパティ |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
|  `identify` | 識別 |
| `setuservariables` | ユーザー変数の構成 |
| `logevent` | イベントの記録 |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
|  `identify` | 識別 |
|  `setuservariables` | ユーザー変数の構成 |
|  `logevent` | イベントの記録 |