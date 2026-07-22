---
title: Nextag ROIトラッカータグ構成ガイド
description: この記事では、iQタグ管理（TiQ）アカウントでNextag ROIトラッカータグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/nextag-roi-tracker-tag/
---
## タグの仕様と要件

### 仕様

* **名前**: Nextag ROIトラッカー
* **ベンダー**: Nextag
* **タイプ**: [比較ショッピングサービス](http://en.wikipedia.org/wiki/Price_comparison_service)のコンバージョントラッキング

### 必要なもの

**サービス**: Nextagアカウント

**構成**:

* マーチャントID

## Tealium iQでのタグ構成

### タグの追加

Tealium iQのタグマーケットプレイスは多種多様なタグを提供しています。プロフィールにタグを追加する方法については[こちら](https://docs.tealium.com/manage-tags/)をクリックしてください。

### タグの構成

1. **タイトル** (必須): タグインスタンスを識別するための記述的なタイトルを入力します。
1. **アカウントID** (任意): Nextagから提供された数値のマーチャントIDを入力します。また、`id`を目的変数としてマッピングすることで、このフィールドを動的に構成するオプションもあります（[マッピングの構成](#mappings)を参照）。例えば、`12345`。

### ロードルールの適用

[ロードルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこでロードするかを決定します。**すべてのページでロード**ルールはデフォルトのロードルールです。このタグを特定のページでロードするには、関連する条件を持つ新しいロードルールを作成します。

**ベストプラクティス**: このタグをサイトの注文確認ページ（サンキューやレシート）でロードするようにロードルールの条件を構成します。

### マッピングの構成

[マッピング](https://docs.tealium.com/about-data-mappings/)は、データレイヤーのデータソースからベンダータグの対応する目的変数にデータを送信するシンプルなプロセスです。このタグのマッピングツールボックスは、事前に定義された目的変数を提供していません。しかし、マッピングを通じてアカウントIDを動的に構成することができます。そのためには、ドロップダウンリストから適切なデータソースを選択し、隣接するテキストフィールドに`id`を入力します（下の例のスクリーンショットを参照）。


<blockquote>
このタグを構成する前に、[E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/)が構成され、構成されていることを確認してください。このタグが使用するE-Commerce変数は`_cprod`, `_corder`, `_ccat`, `_cquan`, `_ctotal`です。
</blockquote>


## ベンダーのドキュメンテーション

* [Nextag Merchant Help Center](http://blog.nextag.com/merchants/)
* [NextagのROI Optimizerへのクイックガイド](http://blog.nextag.com/merchants/wp-content/uploads/2012/03/ROI_Optimizer.pdf)


