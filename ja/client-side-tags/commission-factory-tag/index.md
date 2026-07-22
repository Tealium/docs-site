---
title: Commission Factory タグ構成ガイド
description: この記事では、Commission Factory マーケットプレイスタグの追加と構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/commission-factory-tag/
---
## 要件

* Commission Factory タグは、[E-Commerce extension](https://docs.tealium.com/e-commerce-extension/)が必要です。
* 拡張機能を追加し、`_corder`、`_csubtotal`、`_csku`、`_cprice,` `_cquan` 変数をそれぞれのデータソースにマッピングする必要があります。

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法の一般的な指示については、[Tag Overview](https://docs.tealium.com/about-tags/) 記事を読んでください。

タグを追加する際には、以下の構成を行います：

* **Tag ID**: Commission Factoryから提供される整数値。
* **CF-Object Name**: コマンドを実行するために使用される変数。デフォルトは **cf** です。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[Load Rules](https://docs.tealium.com/about-load-rules/) ドキュメントを参照してください。

## データマッピング

このタグのマッピングは、E-Commerce extensionによって自動的に処理されます。

## パフォーマンス（アドバンス）

* Tealiumのタグテンプレートは、`document.write`の呼び出しとCommission Factoryからの`Track.js`のロードを削除します。
* これにより、訪問に対する可能な限り最速のタグロード時間が確保されます。
* トラッキングiframeを挿入するための`document.write`の呼び出しを削除することで、`document.write`からのエラーなしにページがレンダリングされることが保証されます。

