---
title: YellowHammer タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで YellowHammer を構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/yellowhammer-tag/
---YellowHammer Media Group は、ダイレクトレスポンス全体にわたる高インパクトなオンラインディスプレイパフォーマンスソリューションに焦点を当てた広告配信サービスプロバイダーです。

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法については、[タグ概要](https://docs.tealium.com/about-tags/)の記事を参照してください。

タグを追加する際には、以下の構成を構成します：

* パス (tr): 画像ピクセルの jump.omnitarget.com の直後の部分です。例えば、<http://jump.omnitarget.com/tr123456>? の `tr123456`。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

YellowHammer (Omnitarget) タグの宛先変数は、その**データマッピング**タブに組み込まれています。利用可能なカテゴリーは以下の通りです：

### 標準

|**宛先名**| **説明**|
|---| ---|
|パス (tr)| 構成値を上書きするために使用します。|
|SSPデータ (sspdata)| ランディングページで構成した値のクッキーをマッピングします。|

### Eコマース

YellowHammer (Omnitarget) タグはEコマースをサポートしているため、デフォルトのEコマース拡張マッピングを自動的に使用します。以下の場合を除き、このカテゴリでの手動マッピングは通常必要ありません：

* 拡張マッピングを上書きしたい場合。
* 拡張機能で提供されていないEコマース変数が必要な場合。

|**宛先名**| **説明**|
|---| ---|
|注文ID (order\_id)| デフォルトのEコマース値 `_corder` を上書きするために使用します。|
|小計/販売額 (order\_subtotal)| デフォルトのEコマース値 `_csubtotal` を上書きするために使用します。|
|顧客ID (customer\_id)| デフォルトのEコマース値 `_ccustid` を上書きするために使用します。|
