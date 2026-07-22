---
title: FullStoryリモートコマンドタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでFullStoryリモートコマンドタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/fullstory-remote-command-tag/
---
FullStoryは、お客様の体験データをすべて1つの強力で使いやすいプラットフォームに収集します。FullStoryの小さなスクリプトは、ピクセル完全なセッション再生、自動インサイト、ファネル分析、そして堅牢な検索とセグメンテーションを解放し、組織内の全員がお客様に最高のオンライン体験を提供するのを支援します。

## タグのヒント

* マッピングを使用してイベントをトリガーします。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは次のとおりです：

### スタンダード

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `uid`  | 文字列 | UID |
|  `user_variables.email_str`  | 文字列 | メール |
|  `user_variables.phone_str`  | 文字列 | 電話 |
|  `tealium_event`  | 文字列 | Tealiumイベント |

### E-コマース

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `event.cart_id_str`  | 文字列 | カートID |
| `event.product_id_str`  | 文字列 | 商品ID  |
|  `event.price_real`  | 数値 |実際の価格|
|  `event.name_str`  | 文字列 | 名前|
|  `event.categoryProperties`  | 文字列 | カテゴリプロパティ |

### イベント

イベントをマップするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
|  `identify` | 識別 |
| `setuservariables` | ユーザー変数の構成 |
| `logevent` | イベントの記録 |

### イベント固有のパラメータ

イベントをマップするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
|  `identify` | 識別 |
|  `setuservariables` | ユーザー変数の構成 |
|  `logevent` | イベントの記録 |

