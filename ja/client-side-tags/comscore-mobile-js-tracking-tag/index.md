---
title: comScore Mobile JSトラッキングタグ構成ガイド
description: この記事では、comScore Mobile JSトラッキングタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/comscore-mobile-js-tracking-tag/
---
## タグに関するヒント

* このタグは、ネイティブモバイルアプリ内で使用するためのものです。モバイルWebサイトへの実装を目的としたものではありません。
* マッピングを使用して追加のパラメータを構成し、標準の構成値を上書きします。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の項目を構成します。

* **クライアントID**
* **パブリッシャー秘密鍵**
* **自動更新を有効化**
* **キープアライブイベント**

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `clientID` | clientID |
| `pub_key` | pub_key |
| `appName` | appName |
| `appVersion` | appVersion |
| `keepAliveEnabled` | keepAliveEnabled。true/false。デフォルトはtrueです。 |
| `enableAutoUpdate` | enableAutoUpdate。true/false。デフォルトはfalseです。 |
| `update_interval` | update_interval |
| `update_foregroundOnly` | update_foregroundOnly |
| `view_name` | ページビュー名 |

### ラベル

| 変数 | 説明 |
|:---------|:------------|
| `labels.ns_site` | comscore_site |
| `labels.####` | カスタムラベル |
| `autoStartLabels.####` | 自動開始ラベル |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `active` | アクティブ |
| `aggregate` | 集約 |
| `close` | 終了 |
| `inactive` | 非アクティブ |
| `hidden` | 非表示 |
| `launch` | 起動 |
| `sleep` | スリープ |
| `view` | ビュー |
| `wake` | ウェイク |

### プラットフォーム

| 変数 | 説明 |
|:---------|:------------|
| `plat.appName` | アプリ名 |
| `plat.appVersion` | アプリのバージョン |
| `plat.visitorId` | 訪問ID。`_ccustid`を上書きします |
| `plat.deviceName` | デバイス名 |
| `plat.version` | プラットフォームのバージョン |
| `plat.name` | プラットフォーム名 |
| `plat.runtime` | ランタイムのバージョン |
| `plat.os_version` | OSのバージョン |
| `plat.dev_resolution` | デバイスの解像度 |
| `plat.dev_language` | デバイスの言語 |
| `plat.app_rdns` | パッケージ名 |
| `plat.connection_type` | 接続タイプ |
| `plat.visitorIDSuffix` | 訪問IDのサフィックス |