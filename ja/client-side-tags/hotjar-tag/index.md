---
title: Hotjarタグ構成ガイド
description: この記事では、Hotjarタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/hotjar-tag/
---
## タグのヒント

マッピングを使用して、標準の構成値を動的に上書きします。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Hotjarタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **Hotjar ID**
  * あなたのHotjarサイトID。

* **Hotjarスニペットバージョン**
  * Hotjarからのトラッキングコードのバージョン。

### コードからタグを追加（オプション）

以下の手順でコードからHotjarタグを追加します：

1. Hotjarアカウントにログインします。
1. アカウントダッシュボードから、**手動でコードをインストール**をクリックします。
1. **クリップボードにコピー**をクリックします。
1. Tealium iQタグ管理にログインし、**iQタグ管理 &gt; タグ**に移動します。
1. **タグを追加**をクリックします。
1. **コードからタグを検出**をクリックします。
1. ステップ3でコピーしたコードを貼り付けます。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`hjid`|  <ul><li>Hotjar ID</li></ul> |
| `hjsv` |  <ul><li>Hotjarスニペットバージョン</li></ul> |
