---
title: Optimizely Syncタグ構成ガイド（廃止）
description: 重要  このタグは現在廃止されています。Optimizely Synchronousの実装には[utag.sync.jsを使用してください](/ja/client-side-tags/optimizely-synchronous-implementation/)。既存のタグのインスタンスについては引き続きサポートします。
url: https://docs.tealium.com/ja/client-side-tags/optimizely-sync-tag/
---
Tealiumのタグマーケットプレイスは、ページ上で非同期にロードされるOptimizelyタグと同期にロードされるOptimizelyタグの2つのバージョンを提供しています。では、どちらを使用すべきでしょうか？

* **非同期**: タグを非同期にロードすると、タグのロード失敗がサイトを壊すリスクがなくなります。
* **同期**: コンテンツのちらつきを避けることが主な関心事であれば、このバージョンが最適です。ただし、何かを同期的にロードするたびに、ブラウザが何らかの理由で要素を取得できない場合にサイトが壊れるリスクを導入することに注意してください。必要に応じてアカウントマネージャーにカスタムソリューションを相談してください。

### 前提条件

* Optimizelyアカウント
* プロジェクトID

### タグの追加

Tealium iQのタグマーケットプレイスは多種多様なタグを提供しています。詳細については、[タグの管理](https://docs.tealium.com/manage-tags/#add-a-tag)を参照してください。

### タグの構成

![](https://docs.tealium.com/images/client-side-tags/sync-tag-config.png)

1. **タイトル** (必須): タグインスタンスを識別するための記述的なタイトルを入力します。
1. **プロジェクトID** (必須): Optimizelyから提供された数値のプロジェクト識別子を入力します。

### ロードルールの適用

[ロードルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこでロードするかを決定します。'すべてのページでロード'ルールはデフォルトのロードルールです。このタグを特定のページでロードするには、関連する条件で新しいロードルールを作成します。

**ベストプラクティス**: このタグをすべてのページでロードすることを推奨しますので、'すべてのページでロード'ルールを選択したままにしてください。また、タグタブのタグリストの上部にOptimizelyタグを配置してください。

### マッピングの構成

[マッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)は、データレイヤーのデータソースからベンダータグの対応する宛先変数にデータを送信するシンプルなプロセスです。

注: OptimizelyタグでE-Commerceデータを追跡する予定の場合、そのデータを自動的にマップするために[E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/)を使用することを推奨します。

タグ宛先にマップする方法の指示については、[データソースのマッピング](https://docs.tealium.com/about-data-sources/)を参照してください。

**![](https://docs.tealium.com/images/client-side-tags/sync-tag-mapping.png)**

* **trackEventのためのイベント名 (EVENT\_NAME)**
イベントを識別するデータソースをマップします。

* **trackEventのためのイベント値 (EVENT\_VALUE)**
イベントの値を識別するデータソースをマップします。

----

### ベンダーのドキュメンテーション

* [Optimizelyのドキュメンテーション](http://developers.optimizely.com/)
* [Tealium iQとのOptimizelyの実装](https://help.optimizely.com/hc/en-us/articles/206420397-Implementing-Optimizely-with-Tealium-iQ-or-Ensighten)


