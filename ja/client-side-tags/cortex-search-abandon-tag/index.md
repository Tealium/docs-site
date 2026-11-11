---
title: Cortex Search Abandonタグ構成ガイド
description: この記事では、Cortex Search Abandonタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/cortex-search-abandon-tag/
---
## タグの構成

まず、タグマーケットプレイスに移動し、Cortex Search Abandonタグをプロファイルに追加します（[タグを追加する](https://docs.tealium.com/manage-tags/#add-a-tag)を参照）。

タグを追加したら、以下の構成を構成します。

* **サイトID：** Cortexから提供された一意のサイト識別子を入力します。

## 読み込みルール

[読み込みルール](https://docs.tealium.com/about-load-rules/)では、サイト上でこのタグのインスタンスを読み込むタイミングと場所を指定します。

推奨される読み込みルール：検索アクティビティを追跡する特定のページでこのタグを読み込むように、カスタムルールを構成します。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

Cortex Search Abandonタグの送信先変数は、［データマッピング］タブに組み込まれています。使用可能なカテゴリーは次のとおりです。

### 標準

|**送信先名**| **説明**|
|---| ---|
|サイトID| Cortexから提供されたサイト識別子|
|ユーザーのメールアドレス| 訪問のメールアドレス|
|検索語句| 訪問が使用した検索キーワード|

### Eコマース

Cortex Search AbandonタグはEコマースに対応しているため、デフォルトの[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)のマッピングを自動的に使用します。通常、以下の場合を除き、このカテゴリーで手動によるマッピングを行う必要はありません。

* 拡張機能のマッピングを上書きする場合
* 必要なEコマース変数が拡張機能で提供されていない場合

|**送信先名**| **説明**|
|---| ---|
|ユーザーID| 一意の訪問識別子|

## ベンダーのドキュメント

* [Cortexヘルプドキュメント](http://help.retentionscience.com/hc/en-us/articles/115000423328-Search-Abandon)