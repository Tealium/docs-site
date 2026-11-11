---
title: Webgainsタグ構成ガイド
description: この記事では、Webgainsタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/webgains-tag/
---
## タグに関するヒント

* Eコマース拡張機能を使用して、`_corder`、`_csubtotal`、`_ccustid`、`_cpromo`の値を構成します。
* 商品レベルのバウチャーを構成するには、配列値を`wgvouchercode`にマッピングします。
* `_cprice`には価格のリストが必要です。
* `wgitems`は、Eコマース拡張機能の値（`_cprice`、`_cprodname`、`_cprod`）を使用して自動的に構成されます。これらのEコマース拡張機能の値を上書きするには、この変数に文字列をマッピングします。
* 注文レベルの割引を構成するには、割引値を`wgDISCOUNT`にマッピングします。タグはこの値を負の金額に変換し、割引の明細項目を商品リストに追加します。
* タグは、すべてのページでランディングページスクリプトを実行し、注文確認ページでコンバージョンスクリプトを実行します。コンバージョンスクリプトは、データレイヤー変数から作成された`cvr`オブジェクトと、`_cprice`、`_cprodname`、`_cprod`、`_cquan`から自動的に作成された`items[]`配列を送信します。ページが読み込まれるたびに、一意の注文参照ごとに1件のコンバージョンのみが実行されます。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳しくは、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **プログラムID**：WebgainsのプログラムIDです。タグはこの値を使用して、分析エンドポイントURL `https://analytics.webgains.io/{programid}/main.min.js`を作成します。詳しくは、[Webgainsデフォルトトラッキングガイド](https://knowledgehub.webgains.com/home/webgains-default-tracking-guide)を参照してください。
* **イベントID**：必須の値です。WebgainsはイベントIDを使用してコミッション率を決定します。イベント／コミッショングループIDについては、[Webgainsデフォルトトラッキングガイド](https://knowledgehub.webgains.com/home/webgains-default-tracking-guide)を参照してください。
* **従来のトランザクションピクセルを有効化**：有効にすると、タグは新しい`analytics.webgains.io`コンバージョントラッキングと従来の`track.webgains.com/transaction.html`ピクセルの両方を実行します。デフォルトトラッキングへの移行が完了したら、このオプションを無効にしてください。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳しくは、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳しくは、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | データ型 | 説明 |
|:---------|:------------|:------------|
| `wgsubdomain` | 文字列 |トラッキング対象のサーバーのサブドメイン。 |
| `wglang` |  文字列 |トラッキング対象コンテンツの2文字のISO 639-1言語コード。 |
| `wgslang` | 文字列 |トラッキング対象コンテンツの2文字のISO 639-1サブ言語コード。 |
| `wgprogramid` |  文字列 |WebgainsのプログラムID。|
| `wgeventid` | 文字列 |一意のイベントID。 |
| `wgvalue` |  文字列 |イベントの金額。|
| `wgorderreference` |  文字列 |イベント内のトランザクションを識別する一意の参照ID。|
| `wgcomment` | 文字列 |イベントに関するコメント。 |
| `wgmultiple` |  真偽値 | このイベントが複数回発生した場合に、それぞれを個別にトラッキングまたはカウントするかどうか。`1`はすべてのイベントを個別にトラッキングすることを示し、`0`は最初のイベントのみをトラッキングすることを示します。 |
| `wgitems` | 文字列 | このトランザクションに含まれる項目または商品に関する詳細。 |
| `wgcustomerid` |  文字列 | 顧客ID。 |
| `wgproductid` | 文字列 | 商品ID。 |
| `wgvouchercode` | 文字列 | イベントのバウチャーコードまたは割引コード。 |
| `wgchecksum` | 文字列 | イベントのチェックサム。 |
| `wgDISCOUNT`  | 文字列 | この値を使用して割引商品を追加します。 |
| `wgcurrency`  | 文字列 | `USD`などのトランザクション通貨。 |
| `wglanguage`  | 文字列 | `en_EN`などの注文言語。 |
| `wgcustomertype`  | 文字列 | 顧客タイプ：`new`、`existing`、または`trial`や`subscription`などのカスタム値。 |
| `wglocation`  | 文字列 | `https://example.com/checkout`などの注文確認ページのURL。 |