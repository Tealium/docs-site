---
title: Medallia Digitalタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでMedallia Digitalタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/medallia-digital-tag/
---
Medalliaは、美しくブランド化され、高度にターゲット指向の対話を作成するための顧客体験管理ツールを提供します。Web、モバイルWeb、またはアプリ内のインタラクション中にエンゲージするための25以上の具体的な方法があります。

## タグのヒント

* マッピングを使用して、標準の構成値を上書きします。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加するときには、次の構成を行います：

* **Website ID**: サイトIDの数値。例えば、`https://resources.digital-cloud-west.medallia.com/{Path}/{WebSiteID}/onsite/embed.js`。
* **Path**: Medallia Digital URLに見つけることができる文字列。例えば、`https://resources.digital-cloud-west.medallia.com/{Path}/{WebSiteID}/onsite/embed.js`。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

| 変数 | タイプ | 説明 |
|:---------| ---| :------------|
| Website ID | 数値 | サイトIDの数値。 |
| Path | 文字列 | Medallia Digital URLに見つけることができる文字列。 |

