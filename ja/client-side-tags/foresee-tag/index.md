---
title: Foreseeタグ構成ガイド
description: この記事では、タグ管理アカウントでForeseeタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/foresee-tag/
---
## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **タイトル**：デフォルトは「Foresee」です。任意のカスタム名に変更できます。
* **ファイルパス**：Foreseeのファイルや構成がホストされているURL。   
 例：`//gateway.foresee.com/sites/XXX/XXX/gateway.min.js`

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。読み込みルールの詳細については、[読み込みルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

Foreseeタグの宛先変数は、その「データマッピング」タブに組み込まれています。利用可能なカテゴリは次のとおりです。

### 標準

|タグの宛先|説明|
|---|---|
|ファイルパス|ForeseeスニペットがホストされているURL|

## ベンダーのドキュメント

[Foresee開発者ポータル](https://developer.foresee.com/v1.0/)