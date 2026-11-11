---
title: ContentSquare モバイルリモートコマンドタグ
description: この記事では、タグ管理アカウントで ContentSquare モバイルリモートコマンドタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/contentsquare-mobile-remote-command-tag/
---
ContentSquare は、デジタルチーム全体が顧客に関するインサイトを得られるようにします。マーケターからプロダクトマネージャー、IT 担当者まで、あらゆるデジタル分野の担当者が活用できる強力な統合プラットフォームです。

## タグに関するヒント

* マッピングは、次の目的で使用します。   
  * 構成データを動的に上書きする   
  * E コマース拡張機能の値を動的に上書きする   
  * 追加のデータ値を送信する   
  * イベント固有のパラメータ   
  * イベントトリガー

* 次の E コマース拡張機能の値をサポートしています。   
  * 注文 ID   
  * 商品価格   
  * 通貨

* これは、ネイティブモバイルアプリ SDK 用のモバイルリモートコマンドコンパニオンタグです。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 構成

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `screen_name` | 文字列 | （必須）画面名 |
| `dynamic_var` |  | （必須）動的変数 |

### E コマース

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `purchase.price`（`_ctotal` を上書き） | 配列 | （必須）価格 |
| `purchase.currency`（`_ccurrency` を上書き） | 文字列 | （必須）通貨 |
| `purchase.transaction_id`（`_corder` を上書き） | 文字列 | トランザクション ID |

### カスタム変数

カスタム変数は、画面表示とともに送信される、ページ、ユーザー、またはセッションに関する追加情報です。

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| インデックス | 数値 | カスタム変数のインデックス位置。`1`～`20` の値を選択します。 |
| 名前 | 文字列 | カスタム変数の名前。 |

### イベント

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `sendscreenview` | 画面表示を送信 |
| `sendtransaction` | トランザクションを送信 |
| `senddynamicvar` | 動的変数を送信 |
| `stoptracking` | トラッキングを停止 |
| `resumeTracking` | トラッキングを再開 |
| `forgetme` | 自分に関するデータを消去 |
| `optin` | オプトイン |
| `optout` | オプトアウト |
| `custom` | カスタム |

### イベントパラメータ

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `sendscreenview` | 画面表示を送信 |
| `sendtransaction` | トランザクションを送信 |
| `senddynamicvar` | 動的変数を送信 |
| `stoptracking` | トラッキングを停止 |
| `resumeTracking` | トラッキングを再開 |
| `forgetme` | 自分に関するデータを消去 |
| `optin` | オプトイン |
| `optout` | オプトアウト |
| `custom` | カスタム |