---
title: Adition（タグ付け）タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAdition（タグ付け）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adition-tagging-tag/
---
## タグのヒント

* これはAditionのタグ付けバージョンです。
* Aditionとの契約に従ってドメインを構成します。

  * デフォルト値：`adfarm1.adition.com`
  * AdfarmID：`ad<id>.adfarm1.adition.com`
  * カスタム：`<subdomain>.<domain>.<tld>`

* デフォルトの戻りタイプは`img`です。
* マッピングでは`tag[key.subkey]`を`tag.key.subkey`としてマップします。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Adition（タグ付け）タグを追加します。（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **ドメイン**
  * Aditionから提供されるドメイン。
  * デフォルトのドメインは：`adfarm1.adition.com`

* **ネットワークID**
  * 必須。
  * 例えば241のような数字の文字列

### データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは次のとおりです：

#### スタンダード

| 変数       | 説明        |
|:-----------|:-------------|
| タグタイプ | タグタイプ   |
| ドメイン   | ドメイン     |
| タグ       | [Key.Subkey] |
| ネットワークID | ネットワークID |

