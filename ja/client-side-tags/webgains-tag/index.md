---
title: Webgains タグ構成ガイド
description: この記事では、Webgains タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/webgains-tag/
---
## タグのヒント

* E-Commerce 拡張機能を使用して、`_corder`、`_csubtotal`、`_ccustid`、`_cpromo` の値を構成します。
* 製品レベルのバウチャーを構成するために、配列値を `wgvouchercode` にマッピングします。
* `_cprice` には価格のリストが必要です。
* `wgitems` は、E-Commerce 拡張機能の値（`_cprice`、`_cprodname`、`_cprod`）を使用して自動的に構成されます。これらの E-Commerce 拡張機能の値をオーバーライドするには、この変数に文字列をマッピングします。
* 注文レベルの割引を構成するために、割引値を `wgDISCOUNT` にマッピングします。タグはこの値をマイナス額に変換し、製品リストに割引行項目を追加します。
* タグは、すべてのページでランディングページスクリプトを、注文確認ページでコンバージョンスクリプトを発火します。コンバージョンスクリプトは、データレイヤー変数と `_cprice`、`_cprodname`、`_cprod`、`_cquan` から自動的に構築された `items[]` 配列から `cvr` オブジェクトを送信します。ページロードごとに一意の注文参照に対して一度だけコンバージョンが発火します。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグの追加方法については、[タグの管理](https://docs.tealium.com/manage-tags/)を参照してください。

タグを追加する際には、以下の構成を構成します：

* **プログラム ID**: あなたの Webgains プログラム ID。タグはこの値を使用してアナリティクスエンドポイント URL を構築します：`https://analytics.webgains.io/{programid}/main.min.js`。詳細については、[Webgains デフォルトトラッキングガイド](https://knowledgehub.webgains.com/home/webgains-default-tracking-guide)を参照してください。
* **イベント ID**: 必須の値。Webgains はイベント ID を使用してコミッション率を決定します。あなたのイベント/コミッショングループ ID については、[Webgains デフォルトトラッキングガイド](https://knowledgehub.webgains.com/home/webgains-default-tracking-guide)を参照してください。
* **レガシートランザクションピクセルを有効にする**: 有効にすると、タグは新しい `analytics.webgains.io` のコンバージョントラッキングと古い `track.webgains.com/transaction.html` ピクセルの両方を発火します。デフォルトトラッキングへの移行を完了した後、このオプションを無効にします。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | データタイプ | 説明 |
|:---------|:------------|:------------|
| `wgsubdomain` | 文字列 |トラッキングされているサーバーのサブドメイン。 |
| `wglang` |  文字列 |トラッキングされているコンテンツのISO 639-1 2文字言語コード。 |
| `wgslang` | 文字列 |トラッキングされているコンテンツのISO 639-1 2文字サブ言語コード。  |
| `wgprogramid` |  文字列 |Webgains プログラム ID。|
| `wgeventid` | 文字列 |ユニークなイベント ID。  |
| `wgvalue` |  文字列 |イベントの金銭的価値。|
| `wgorderreference` |  文字列 |イベント内のトランザクションのユニークな参照 ID。|
| `wgcomment` | 文字列 |イベントに関するコメント。 |
| `wgmultiple` |  ブール |このイベントが複数回トラッキングまたは個別にカウントされるかどうか。`1`はすべてのイベントが個別にトラッキングされることを示し、`0`は最初のイベントのみがトラッキングされることを示します。 |
| `wgitems` | 文字列 |このトランザクションのアイテムまたは製品の詳細。 |
| `wgcustomerid` |  文字列 |顧客 ID。 |
| `wgproductid` | 文字列 |製品 ID。 |
| `wgvouchercode` | 文字列 |イベントのバウチャーまたは割引コード。 |
| `wgchecksum` | 文字列 |イベントのチェックサム。  |
| `wgDISCOUNT`  | 文字列 |この値で割引製品を追加します。 | 
| `wgcurrency`  | 文字列 |トランザクション通貨、例：`USD`。 |   
| `wglanguage`  | 文字列 |注文の言語、例：`en_EN`。 |   
| `wgcustomertype`  | 文字列 |顧客タイプ：`new`、`existing`、または `trial` や `subscription` などのカスタム値。 |   
| `wglocation`  | 文字列 |注文確認ページのURL、例：`https://example.com/checkout`。 |   