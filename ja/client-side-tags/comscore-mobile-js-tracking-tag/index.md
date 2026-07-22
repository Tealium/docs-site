---
title: comScore Mobile JS トラッキングタグ構成ガイド
description: この記事では、comScore Mobile JS トラッキングタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/comscore-mobile-js-tracking-tag/
---
## タグのヒント

* このタグはネイティブモバイルアプリ内での使用を目的としています。モバイルウェブサイトの実装で使用することは意図されていません。
* 追加のパラメータを構成したり、標準の構成値を上書きするためにマッピングを使用します。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **クライアントID**
* **パブリッシャーシークレットキー**
* **自動更新を有効にする**
* **キープアライブイベント**

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `clientID` | クライアントID  |
| `pub_key` | パブリッシャーキー  |
| `appName` | アプリ名  |
| `appVersion` | アプリバージョン |
| `keepAliveEnabled` | キープアライブ有効、真/偽、デフォルトは真。 |
| `enableAutoUpdate` | 自動更新を有効にする、真/偽、デフォルトは偽。 |
| `update_interval` | 更新間隔 |
| `update_foregroundOnly` | フォアグラウンドのみ更新 |
| `view_name` | ページビュー名 |

### ラベル

| 変数 | 説明 |
|:---------|:------------|
| `labels.ns_site` | comscore_site |
| `labels.####` | カスタムラベル |
| `autoStartLabels.####` | 自動開始ラベル |

### イベント
イベントをマップするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `active` | アクティブ |
| `aggregate` | 集計 |
| `close` | 閉じる |
| `inactive` | 非アクティブ |
| `hidden` | 隠す |
| `launch` | 起動 |
| `sleep` | スリープ |
| `view` | ビュー |
| `wake` | 起きる |

### プラットフォーム

| 変数 | 説明 |
|:---------|:------------|
| `plat.appName` | アプリ名 |
| `plat.appVersion` | アプリバージョン |
| `plat.visitorId` | 訪問ID、`_ccustid`を上書き |
| `plat.deviceName` | デバイス名 |
| `plat.version` | プラットフォームバージョン |
| `plat.name` | プラットフォーム名 |
| `plat.runtime` | ランタイムバージョン |
| `plat.os_version` | OSバージョン  |
| `plat.dev_resolution` | デバイス解像度 |
| `plat.dev_language` | デバイス言語 |
| `plat.app_rdns` | パッケージ名 |
| `plat.connection_type` | 接続タイプ |
| `plat.visitorIDSuffix` | 訪問IDサフィックス |

