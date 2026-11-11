---
title: Salecycleタグ構成ガイド
description: この記事では、タグ管理アカウントでSalecycleタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/salecycle-tag/
---
## タグ構成のヒント

* マッピングを使用して、標準構成値またはEコマース拡張機能の値を上書きします。
* このタグを読み込み順序の先頭または先頭付近で読み込みます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の項目を構成します。

* **クライアントID**：SaleCycleから提供された小文字のクライアントID。この値は、スクリプトパス内の`clientID`を置き換えます（例：`https://s.salecycle.com/clientID/bundle.js`）。
* **ピクセルタイプ**：読み込むタグのタイプ。指定できる値は`script`と`image`です。どちらを使用すべきか不明な場合は、`script`オプションを使用してください。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。