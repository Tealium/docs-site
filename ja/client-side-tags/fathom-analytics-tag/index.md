---
title: Fathom Analyticsタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでFathom Analyticsタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/fathom-analytics-tag/
---
このタグは、Fathom Analyticsスクリプトをあなたのサイトに追加します。このスクリプトは、クッキーや個人データを収集せずに、ページビュー、セッション、バウンス率、その他のメトリクスを追跡します。スクリプトは、サイトIDの変更、正規URLの無視、トラックしないリクエストの尊重など、さまざまなオプションでカスタマイズできます。

## タグのヒント

* マッピングを使用して、標準の構成値を動的に上書きします。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **サイトID**：新しいサイトを作成する際に生成されるサイトID。data-site属性に表示されます。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 構成

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `site_id`  | String | サイトID |

### 標準

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `url`  | String | URL |
|  `referrer`  | String | リファラー |
|  `event_id`  | String | イベントID |
|  `event_value`  | Number | イベント値 |

### HTML属性

詳細については

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `load_option`  | String | ロードオプション。<ul><li>`defer`: サイトのロードが終了した後にスクリプトのロードを遅延させます。</li><li>`async`: スクリプトを非同期でロードします。</li></ul> | 
|  `data_auto`  | String | 自動トラッキングを無効にします。利用可能な値は`true`と`false`です。 |
|  `data_canonical`  | String | 正規URLを無視します。利用可能な値は`true`と`false`です。 | 
|  `data_excluded_domains`  | String | データ収集から除外するドメインのカンマ区切りリスト。 |
|  `data_spa`  | String | シングルページアプリケーションモードを構成します。<ul><li>`auto`: HTML5 History APIが利用可能か自動的にチェックし、そうでない場合はハッシュベースのルーティングを使用します。</li><li>`history`: HTML5 History APIを使用します。</li><li>`hash`: ハッシュベースのルーティングを使用します。</li></ul> |

### イベント

イベントマッピングの作成についての詳細は、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
|  `trackPageview` | ページビューの追跡 |
|  `trackGoal` | ゴールの追跡 |

### イベント固有のパラメータ
イベントマッピングの作成についての詳細は、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
|  `trackPageview` | ページビューの追跡 |
|  `trackGoal` | ゴールの追跡 |

