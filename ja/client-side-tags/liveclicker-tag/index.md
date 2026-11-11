---
title: Liveclickerタグ構成ガイド
description: この記事では、Liveclickerタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/liveclicker-tag/
---
Liveclickerは、マーケティングチャネル向けの動画コマースソリューションです。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **アカウントID**：Liveclickerから提供されるLiveclickerアカウントの識別子です。トラッキングリクエストをアカウントに関連付けるために使用されます。
* **ベースURL**：Liveclickerのトラッキングエンドポイントのホスト名とパスです（例：`sc.liveclicker.net/service/track`）。プロトコルは含めないでください。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `value` | コンバージョンまたは注文に割り当てる金額。 |
| `order_id` | コンバージョンに関連付けられた注文または取引の一意の識別子。 |