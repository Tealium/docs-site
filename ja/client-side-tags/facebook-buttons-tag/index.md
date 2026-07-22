---
title: Facebookボタンタグ構成ガイド
description: この記事では、Facebookボタンタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/facebook-buttons-tag/
---
## タグのヒント

* 一部の構成パラメータは**Like**ボックスにのみ適用されます。例えば、ボーダーカラーや高さなどです。
* まだ持っていない場合は、**Content Modification**拡張機能を使用してページに新しい`DIV`を挿入します。
* `HREF`はマッピングによって上書きされない限り、ページURLがデフォルトになります。
* 言語は`ll_cc`の形式である必要があります
  * `ll`は2文字の言語コード
  * `cc`は2文字の国コード
  * すべてのサポートされているコードについては、[Facebook Locales](https://www.facebook.com/translations/FacebookLocales.xml)を参照してください。

* Kid Directed
  * ウェブサイトやオンラインサービス、またはその一部が13歳未満の子供向けになっている場合は、trueに構成する必要があります。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Facebookボタンタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちらをご覧ください）。

タグを追加したら、以下の構成を行います：

* **アクション**
* **Div ID**
  * ボタンが表示される`DIV ID`。

* **HREF**
  * ページのURL。
  * データレイヤーでは`dom.url`がデフォルト

* **言語**
  * デフォルトは`en_US`
  * 基本的な形式は`ll_CC`で、`ll`は2文字の言語コード、`CC`は2文字の国コードです。
  * すべてのサポートされているコードについては、[Facebook Locales](https://www.facebook.com/translations/FacebookLocales.xml)を参照してください。

* **カラースキーム**
* **レイアウト**
  * **Like**および**Share**ボタンで使用します。

* **Kid Directed**
  * ウェブサイトやオンラインサービス、またはその一部が13歳未満の子供向けになっている場合は、`true`に構成する必要があります。

* **サイズ**
* **幅**

## データマッピング

マッピングとは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`action`|  <ul><li>アクション</li></ul> |
|`language`|  <ul><li>言語</li></ul> |
|`href`|  <ul><li>Hrefリンク</li></ul> |
|`config.colorscheme`|  <ul><li>カラースキーム</li><li>値は`light`または`dark`</li></ul> |
|`appId`|  <ul><li>アプリID</li></ul> |
|`config.size`|  <ul><li>サイズ</li></ul> |
|`config.width`|  <ul><li>幅</li></ul> |

### Like

|変数| 説明|
|---| ---|
|`like.layout`|  <ul><li>レイアウト</li></ul> |
|`like.show_faces`|  <ul><li>顔を表示</li><li>値は`true`または`false`。</li></ul> |
|`like.kid_directed`|  <ul><li>子供向けサイト</li><li>値は`true`または`false`。</li></ul> |
|`like.color_scheme`|  <ul><li>カラースキーム</li><li>値は`light`または`dark`。</li></ul> |
|`like.###`|  <ul><li>カスタムLike値</li></ul> |

### Recommend

|変数| 説明|
|---| ---|
|`rec.layout`|  <ul><li>レイアウト</li></ul> |
|`rec.show_faces`|  <ul><li>顔を表示</li><li>値は`true`または`false`。</li></ul> |
|`rec.kid_directed`|  <ul><li>子供向けサイト</li><li>値は`true`または`false`。</li></ul> |
|`rec.color_scheme`|  <ul><li>カラースキーム</li><li>値は`light`または`dark`。</li></ul> |
| `rec.###` |  <ul><li>カスタムRecommend値</li></ul> |

### Share

|変数| 説明|
|---| ---|
|`share.layout`|  <ul><li>レイアウト</li></ul> |
|`share.kid_directed`|  <ul><li>子供向けサイト</li><li>値は`true`または`false`。</li></ul> |
| `share.###` |  <ul><li>カスタムShare値</li></ul> |

### Send

|変数| 説明|
|---| ---|
|`send.kid_directed`|  <ul><li>値は`true`または`false`。</li></ul> |
|`send.color_scheme`|  <ul><li>値は`light`または`dark`。</li></ul> |
|`send.###`|  <ul><li>カスタムSend値</li></ul> |
