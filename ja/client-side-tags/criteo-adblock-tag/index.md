---
title: Criteo Adblockタグ構成ガイド
description: この記事では、Criteo Adblockタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/criteo-adblock-tag/
---
## 前提条件

* Criteoアカウントでの構成を完了していること：PassbackとCPMが構成されていることを確認してください。
* Criteo Zone ID

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を行います。

1. Criteo Zone ID：Criteoから提供される一意のID。
1. Container ID：コンテナのHTML要素ID。
1. CPM：自動最適化するか、Criteoアカウントで構成されているCPMに従うかを選択します。
1. Enable Passback：Criteo Passbackを有効にするかどうかを選択します。この構成は、Criteoで行った選択と一致している必要があります。

## ロードルール

[ロードルール](https://docs.tealium.com/about-load-rules/)では、サイト上でこのタグのインスタンスをいつ、どこに読み込むかを指定します。

推奨されるロードルール：**すべてのページで読み込む**。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

Criteo Adblockタグの宛先変数は、［データマッピング］タブに組み込まれています。使用可能なカテゴリーは次のとおりです。

### 標準

| **宛先名**      | **説明**                                                                                  |
|:----------------|:------------------------------------------------------------------------------------------|
| Zone ID         | 一意のID                                                                                  |
| Container ID    | コンテナのHTML要素ID                                                                      |
| CPM             | Criteoアカウントで構成されているCPM構成。指定可能な文字列値は`auto`または`abide`です。     |
| Enable Passback | Criteoアカウントで構成されているPassbackフラグ。指定可能な文字列値は`yes`または`no`です。 |

## ベンダーのドキュメント

* [Criteoパブリッシャーサポート](https://support.criteo.com/hc/en-us/categories/200849245)