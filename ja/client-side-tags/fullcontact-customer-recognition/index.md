---
title: FullContact顧客認識タグ構成ガイド
description: この記事では、FullContact顧客認識タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/fullcontact-customer-recognition/
---
FullContactは、人々とブランドの間に信頼を築くプライバシーセーフなID解決会社です。データを統合し、重要な瞬間に洞察を適用することで、カスタマイズされた顧客体験を作り出すための機能を提供します。

## タグのヒント

* マッピングを使用して、標準の構成値を動的に上書きします。

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **FullContactキー**：FullContactタグ認識キー。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `fullContactKey`  | 文字列 | FullContactキー |
|  `base_url`  | 文字列 | ベースURL |
|  `forceCallback`  | ブール値 | 強制コールバック |
|  `fc_cb`  | 関数 | FullContactコールバック |

