---
title: Selligent Webtrackerタグ構成ガイド
description: この記事では、Selligent Webtrackerタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/selligent-webtracker-tag/
---
Selligentのクロスチャネルキャンペーン管理を使用すると、マーケターは一つのソリューションからインタラクションを管理します。

## タグのヒント

分類タグを渡すために、マッピングとオーバーライド`taxtags`を使用します。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **アカウントID**: Selligentから提供されるあなたのアカウントID。
* **DLLドメイン**: あなたの`.dll`ドメイン。例：`https://example.domain.com/optiext/webtracker.dll`の`example.domain.com`。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 変数 | 説明 |
|:---------|:------------|
| `accountid` | アカウントID |
| `dll_domain` | DLLドメイン |
| `taxtags` | 分類タグ |
| `nb_segments` | セグメント数 |
| `from_airport` | 出発空港 |
| `to_airport` | 目的地の空港 |

### E-コマース

| 変数 | 説明 |
|:---------|:------------|
| `order_id` | 注文`ID`（`_corder`を上書き） |
| `order_total` | 注文合計（`_ctotal`を上書き） |

## タグのデバッグ

タグをテストするには、リダイレクションURLに`m_i`クエリストリングパラメータを追加するキャンペーンを使用します。`m_i`クエリストリングはトラッキングコールをトリガーし、それによりブラウザに`m_trk`ファーストパーティクッキーが作成され、それに値が割り当てられます。
