---
title: BlueKaiタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでBlueKaiタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/bluekai-tag/
---
## タグのヒント

マッピングを使用して、標準の構成値を上書きするか、追加のパラメータを渡します。

## タグの構成

タグマーケットプレイスに移動し、BlueKaiタグを追加します。詳細については、[タグの管理]()を参照してください。

タグを追加した後、次の変数を構成します：

* **サイトID**：ピクセルが特定のDMPパートナーに所属していることを識別する一意の番号。
* **制限**：BlueKaiによって発火されるメディアパートナーセグメントピクセルの最大数。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

次の変数はBlueKaiタグで利用可能です：

### 標準

|変数| 説明|
|---| ---|
|サイトID| (siteid)|
|制限| (limit)|
|複数の呼び出しを許可する (`allow_multiple_calls`)| [boolean]|
|show| |
|tod| |
|lv| |
|ss| |
|top| |
|sub1| |
|sub2| |
|sub3| |
|ref| |
|srch| |

