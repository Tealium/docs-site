---
title: Nextag ROI Trackerタグ構成ガイド
description: この記事では、タグ管理アカウントでNextag ROI Trackerタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/nextag-roi-tracker-tag/
---
## タグの仕様と要件

### 仕様

* **名前**: Nextag ROI Tracker
* **ベンダー**: Nextag
* **タイプ**: [比較ショッピングサービス](http://en.wikipedia.org/wiki/Price_comparison_service)向けコンバージョントラッキング

### 必須要件

**サービス**: Nextagアカウント

**構成**:

* マーチャントID

## タグの構成

### タグの追加

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

### タグの構成

1. **タイトル**:（必須）タグインスタンスを識別するための分かりやすいタイトルを入力します。
1. **アカウントID**:（任意）Nextagから提供された数値のマーチャントIDを入力します。また、`id`を宛先変数としてマッピングすることで、このフィールドを動的に構成することもできます（[マッピングの構成](#mappings)を参照）。例: `12345`。

### 読み込みルールの適用

[読み込みルール](https://docs.tealium.com/about-load-rules/)では、このタグのインスタンスをいつ、どこで読み込むかを決定します。デフォルトの読み込みルールは、**すべてのページで読み込む**ルールです。このタグを特定のページで読み込むには、該当する条件を指定して新しい読み込みルールを作成します。

**ベストプラクティス**: サイトの注文確認ページ（サンクューページまたは領収書ページ）でこのタグを読み込むように、読み込みルールの条件を構成します。

### マッピングの構成

[マッピング](https://docs.tealium.com/about-data-mappings/)とは、データレイヤー内のデータソースから、ベンダータグの対応する宛先変数へデータを送信するためのシンプルなプロセスです。このタグのマッピングツールボックスには、事前定義された宛先変数はありません。ただし、マッピングを使用してアカウントIDを動的に構成できます。これを行うには、ドロップダウンリストから適切なデータソースを選択し、隣接するテキストフィールドに`id`と入力します（以下のスクリーンショット例を参照）。


<blockquote>
このタグを構成する前に、[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)がセットアップおよび構成されていることを確認してください。このタグで使用するEコマース変数は、`_cprod`、`_corder`、`_ccat`、`_cquan`、`_ctotal`です。
</blockquote>


## ベンダーのドキュメント

* [Nextagマーチャントヘルプセンター](http://blog.nextag.com/merchants/)
* [Nextag ROI Optimizerクイックガイド](http://blog.nextag.com/merchants/wp-content/uploads/2012/03/ROI_Optimizer.pdf)