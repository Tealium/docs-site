---
title: Selligent Webtrackerタグ構成ガイド
description: この記事では、Selligent Webtrackerタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/selligent-webtracker-tag/
---
Selligentのクロスチャネルキャンペーン管理により、マーケターは単一のソリューションからインタラクションを管理できます。

## タグに関するヒント

マッピングを使用して`taxtags`をオーバーライドし、タクソノミータグを渡します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の項目を構成します。

* **アカウントID**：Selligentから提供されたアカウントID。
* **DLLドメイン**：`.dll`のドメイン。例：`https://example.domain.com/optiext/webtracker.dll`の`example.domain.com`。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `accountid` | アカウントID |
| `dll_domain` | DLLドメイン |
| `taxtags` | タクソノミータグ |
| `nb_segments` | セグメント数 |
| `from_airport` | 出発空港 |
| `to_airport` | 到着空港 |

### Eコマース

| 変数 | 説明 |
|:---------|:------------|
| `order_id` | 注文`ID`（`_corder`をオーバーライド） |
| `order_total` | 注文合計（`_ctotal`をオーバーライド） |

## タグのデバッグ

タグをテストするには、リダイレクトURLに`m_i`クエリ文字列パラメータを追加するキャンペーンを使用します。`m_i`クエリ文字列によってトラッキングコールがトリガーされ、ブラウザーに`m_trk`ファーストパーティCookieが作成されて値が割り当てられます。