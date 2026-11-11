---
title: LiveRampクライアントサイドタグ構成ガイド
description: この記事では、タグ管理アカウントでLiveRampクライアントサイドタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/liveramp-client-side-tag/
---
## タグに関するヒント

* マッピングを使用して、送信する`pdata`の値を構成します。

## タグの構成

タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の項目を構成します。

* **タグID**：ベンダーから提供されたタグID。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数               | 説明                           |
|:-------------------|:-------------------------------|
| `tag_id`           | タグID。                       |
| `pdata.myvar`      | pdata.myvar。                  |
| `timestamp`        | タイムスタンプ。               |
| `repeat_visitor`   | 再訪問。                     |
| `domain`           | ドメイン。                     |
| `device_type`      | デバイスタイプ。               |
| `traffic_source`   | トラフィックソース。           |
| `referral_channel` | 参照チャネル。                 |
| `referral_source`  | 参照元。                       |
| `search_group`     | 検索グループ。                 |
| `key_act_1`        | カスタムデータのキー#1。       |
| `key_act_2`        | カスタムデータのキー#2。       |
| `key_act_3`        | カスタムデータのキー#3。       |
| `key_act_4`        | カスタムデータのキー#4。       |
| `key_act_5`        | カスタムデータのキー#5。       |
| `key_act_6`        | カスタムデータのキー#6。       |
| `key_act_7`        | カスタムデータのキー#7。       |
| `url_path`         | URLパス。                      |