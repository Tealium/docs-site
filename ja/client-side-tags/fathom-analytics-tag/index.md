---
title: Fathom Analyticsタグ構成ガイド
description: この記事では、タグ管理アカウントでFathom Analyticsタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/fathom-analytics-tag/
---
このタグは、Fathom Analyticsスクリプトをサイトに追加します。このスクリプトは、Cookieを使用したり個人データを収集したりすることなく、ページビュー、セッション、直帰率などの指標を追跡します。サイトIDの変更、正規URLの無視、Do Not Trackリクエストの尊重など、さまざまなオプションでスクリプトをカスタマイズできます。

## タグに関するヒント

* マッピングを使用すると、標準の構成値を動的に上書きできます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を行います。

* **サイトID**：新しいサイトの作成時に生成されるサイトIDです。data-site属性に表示されます。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 構成

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `site_id`  | 文字列 | サイトID |

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `url`  | 文字列 | URL |
|  `referrer`  | 文字列 | リファラー |
|  `event_id`  | 文字列 | イベントID |
|  `event_value`  | 数値 | イベント値 |

### HTML属性

詳細情報

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `load_option`  | 文字列 | 読み込みオプション。<ul><li>`defer`：サイトの読み込みが完了するまで、スクリプトの読み込みを遅延します。</li><li>`async`：スクリプトを非同期で読み込みます。</li></ul> |
|  `data_auto`  | 文字列 | 自動トラッキングを無効にします。使用可能な値は`true`と`false`です。 |
|  `data_canonical`  | 文字列 | 正規URLを無視します。使用可能な値は`true`と`false`です。 |
|  `data_excluded_domains`  | 文字列 | データ収集から除外するドメインのカンマ区切りリストです。 |
|  `data_spa`  | 文字列 | シングルページアプリケーションモードを構成します。<ul><li>`auto`：HTML5 History APIが利用可能かどうかを自動的に確認し、利用できない場合はハッシュベースのルーティングを使用します。</li><li>`history`：HTML5 History APIを使用します。</li><li>`hash`：ハッシュベースのルーティングを使用します。</li></ul> |

### イベント

イベントのマッピングについて詳しくは、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
|  `trackPageview` | ページビューを追跡 |
|  `trackGoal` | ゴールを追跡 |

### イベント固有のパラメーター

イベントのマッピングについて詳しくは、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
|  `trackPageview` | ページビューを追跡 |
|  `trackGoal` | ゴールを追跡 |