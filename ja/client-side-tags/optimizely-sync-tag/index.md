---
title: Optimizely同期タグ構成ガイド（非推奨）
description: 重要  このタグは現在非推奨です。[Optimizelyの同期実装用utag.sync.js](/ja/client-side-tags/optimizely-synchronous-implementation/)を使用してください。既存のタグインスタンスについては、引き続きサポートします。
url: https://docs.tealium.com/ja/client-side-tags/optimizely-sync-tag/
---
Tealiumのタグマーケットプレイスでは、Optimizelyタグに、ページ上で非同期に読み込むバージョンと、同期的に読み込むバージョンの2種類が用意されています。では、どちらを使用すべきでしょうか？

* **非同期**：タグを非同期に読み込むことで、タグの読み込み失敗によりサイトが動作しなくなるリスクを回避できます。
* **同期**：このバージョンは、コンテンツのちらつきを防ぐことが最優先の場合に適しています。何かを同期的に読み込むと、何らかの理由でブラウザーがその要素を取得できない場合に、サイトが動作しなくなるリスクが生じることに注意してください。必要に応じて、カスタムソリューションについて担当のアカウントマネージャーにご相談ください。

### 前提条件

* Optimizelyアカウント
* プロジェクトID

### タグの追加

タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

### タグの構成

![](https://docs.tealium.com/images/client-side-tags/sync-tag-config.png)

1. **タイトル**：（必須）タグインスタンスを識別するための、わかりやすいタイトルを入力します。
1. **プロジェクトID**：（必須）Optimizelyから提供された数値のプロジェクト識別子を入力します。

### ロードルールの適用

[ロードルール](https://docs.tealium.com/about-load-rules/)によって、このタグのインスタンスをいつ、どこで読み込むかが決まります。デフォルトのロードルールは「すべてのページで読み込む」です。特定のページでこのタグを読み込むには、該当する条件を指定した新しいロードルールを作成します。

**ベストプラクティス**：このタグをすべてのページで読み込むことを推奨します。そのため、「すべてのページで読み込む」ロードルールを選択したままにしてください。また、「タグ」タブのタグリストの先頭にOptimizelyタグを配置してください。

### マッピングの構成

[マッピング](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)とは、データレイヤー内のデータソースから、ベンダータグの対応する宛先変数へデータを送信するための簡単なプロセスです。

注：Optimizelyタグを使用してEコマースデータをトラッキングする場合は、[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)を使用して、そのデータを自動的にマッピングすることを推奨します。

タグの宛先にマッピングする方法については、[データソースのマッピング](https://docs.tealium.com/about-data-sources/)を参照してください。

**![](https://docs.tealium.com/images/client-side-tags/sync-tag-mapping.png)**

* **trackEventのイベント名（EVENT\_NAME）**
イベントを識別するデータソースをマッピングします。

* **trackEventのイベント値（EVENT\_VALUE）**
イベントの値を識別するデータソースをマッピングします。

----

### ベンダーのドキュメント

* [Optimizelyのドキュメント](http://developers.optimizely.com/)
* [タグ管理を使用したOptimizelyの実装](https://help.optimizely.com/hc/en-us/articles/206420397-Implementing-Optimizely-with-Tealium-iQ-or-Ensighten)