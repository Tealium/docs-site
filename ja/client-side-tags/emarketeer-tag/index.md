---
title: Emarketeerタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでEmarketeerタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/emarketeer-tag/
---
## タグ構成

まず、タグマーケットに移動し、Emarketeerタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **ユーザーシークレット**
  * あなたのEmarketeerユーザーシークレット

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
|`EMUserSecret`|  <ul><li>文字列</li><li>Emarketeerユーザーシークレット</li></ul> |
