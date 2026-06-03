---
title: Criteo Adblockタグ構成ガイド
description: この記事では、Criteo Adblockタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/criteo-adblock-tag/
---
## 前提条件

* Criteoアカウントでの完全な構成: PassbackとCPMの構成が行われていることを確認してください。
* Criteo ZoneID

## タグ構成

まず、タグマーケットプレイスに移動し、Criteo Adblockタグをプロファイルに追加します([タグの追加方法]())。

タグを追加した後、以下の構成を行います:

1. Criteo Zone ID: Criteoから提供される一意のID。
1. Container ID: コンテナのHTML Element ID。
1. CPM: 自動最適化を選択するか、Criteoアカウントで構成したCPMに従うかを選択します。
1. Enable Passback: Criteo Passbackを有効にするかどうかを選択します。これはCriteoで選択したものと一致していなければなりません。

## ロードルール

[ロードルール]()は、このタグをサイト上のどこで、いつロードするかを決定します。

推奨されるロードルール: **すべてのページでロード**。

## データマッピング

マッピングは、[データレイヤー変数](/ja/iq-tag-management/data-mappings/manage/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

Criteo Adblockタグの宛先変数は、そのデータマッピングタブに組み込まれています。利用可能なカテゴリーは以下の通りです:

### 標準

| **宛先名** | **説明**                                                                           |
|:---------------------|:------------------------------------------------------------------------------------------|
| Zone ID              | ユニークID                                                                                 |
| Container ID         | コンテナのHTML Element ID                                                              |
| CPM                  | Criteoアカウントで構成したCPM。可能な文字列値は`auto`または`abide`です。 |
| Enable Passback      | Criteoアカウントで構成したPassbackフラグ。可能な文字列値は`yes`または`no`です。    |

## ベンダー文書

* [Criteo Publisher Support](https://support.criteo.com/hc/en-us/categories/200849245)
