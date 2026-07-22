---
title: Qualarooタグ
description: この記事では、Qualarooタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/qualaroo-tag/
---
## タグのヒント

* マッピングを使用して、標準の構成値を動的に上書きします。
* ログインしている顧客のメールアドレス（または他の識別子）を送信するには、その値をマッピングを通じて`identify`に割り当てます。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **JavaScriptファイルパス**：Qualaroo JavaScriptライブラリファイルへのパス。例えば、`s3.amazonaws.com/ki.js/12345/example.js`

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `jspath`| 文字列 | Qualaroo JavaScriptライブラリファイルへのパス。例えば、`s3.amazonaws.com/ki.js/12345/example.js`  |
|`identify`| 文字列 | メールアドレスまたは他の識別子パラメータ。  | 

