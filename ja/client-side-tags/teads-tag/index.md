---
title: Teadsタグ構成ガイド
description: この記事では、Teadsタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/teads-tag/
---
## タグのヒント

* マッピングを使用して、標準の構成値を上書きし、追加のオプションを構成します。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Teadsタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **pid**
  * Teadsから提供されたPID

* **lang**
  * 言語。
  * デフォルト値は英語（ `en`）。

* **Slot**
  * 広告を配置するためのセレクタ。
  * 例：`.article .article_body &amp;gt; p`

* **Format**
* **minSlot**
* **Mobile**
* **css**

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

| 変数       | 説明                     |
|:-----------|:--------------------------|
| Pid        |                           |
| Lang       |                           |
| Slot       |                           |
| Format     |                           |
| minSlot    |                           |
| mobile     | &lt;ul&gt;&lt;li&gt;ブーリアン&lt;/li&gt;&lt;/ul&gt; |
| Skip delay |                           |
| Mute delay |                           |
| CSS        |                           |
| BTF        | &lt;ul&gt;&lt;li&gt;ブーリアン&lt;/li&gt;&lt;/ul&gt; |
| Mutable    | &lt;ul&gt;&lt;li&gt;ブーリアン&lt;/li&gt;&lt;/ul&gt; |
| AdBreaks   |                           |
| avoidSlot  |                           |