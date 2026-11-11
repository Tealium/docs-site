---
title: AppDynamicsタグ構成ガイド
description: この記事では、タグ管理アカウントでAppDynamicsタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/appdynamics-tag/
---
AppDynamicsは、ソフトウェアからインフラストラクチャ、ビジネスジャーニーに至るまで、ビジネスパフォーマンスの把握と最適化を支援するアプリケーションパフォーマンス管理（APM）プラットフォームです。

## タグに関するヒント

* マッピングを使用すると、標準の構成値を動的に上書きできます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **App Key**：AppDynamicsアカウントのEUMアプリキー。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### タグの構成

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| App Key   | 文字列 | AppDynamicsアカウントのEUMアプリキー（タグ構成を上書きします）。 |

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `xhr_url`  | 文字列 | XHR URL |
|  `error_msg`  | 文字列 | エラーメッセージ | 
|  `error_line`  | 数値 | エラーが発生したソースコード内の行番号。 |
|  `error_stack`  | 文字列 | エラー発生時のスタックトレース。 |

### イベント

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `VPageView`  |仮想ページビューの各段階を追跡します。 |
| `Ajax`| Ajaxリクエストを追跡します。 |
| `Error` | エラーを追跡します。 |

### イベント固有のパラメータ

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `xhr_url` | XHR URL。 |
| `error_msg` | エラーメッセージ。 |
| `error_line` | エラーが発生したソースコード内の行番号。 |
| `error_stack` | エラー発生時のスタックトレース。 |  |
| `VPageView` | 仮想ページビューの各段階を追跡します。 |
| `Ajax` | Ajaxリクエストを追跡します。 |
| `Error`| エラーを追跡します。 |