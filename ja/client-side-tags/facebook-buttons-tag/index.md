---
title: Facebook Buttonsタグ構成ガイド
description: この記事では、Facebook Buttonsタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/facebook-buttons-tag/
---
## タグに関するヒント

* 一部の構成パラメータ（枠線の色や高さなど）は、**Like**ボックスにのみ適用されます。
* ページに新しい`DIV`がまだない場合は、**Content Modification**拡張機能を使用して挿入します。
* マッピングで上書きしない限り、`HREF`のデフォルト値はページのURLです。
* 言語は`ll_cc`形式で指定する必要があります。
  * `ll`は2文字の言語コードです。
  * `cc`は2文字の国コードです。
  * サポートされているすべてのコードについては、[Facebook Locales](https://www.facebook.com/translations/FacebookLocales.xml)を参照してください。

* 子供向け
  * Webサイト、オンラインサービス、またはサービスの一部が13歳未満の子供を対象としている場合は、trueに構成する必要があります。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **アクション**
* **Div ID**
  * ボタンを表示する`DIV ID`。

* **HREF**
  * ページのURL。
  * データレイヤー内の`dom.url`がデフォルト値です。

* **言語**
  * デフォルトは`en_US`です。
  * 基本形式は`ll_CC`です。`ll`は2文字の言語コード、`CC`は2文字の国コードです。
  * サポートされているすべてのコードについては、[Facebook Locales](https://www.facebook.com/translations/FacebookLocales.xml)を参照してください。

* **カラースキーム**
* **レイアウト**
  * **Like**ボタンおよび**Share**ボタンで使用します。

* **子供向け**
  * Webサイト、オンラインサービス、またはサービスの一部が13歳未満の子供を対象としている場合は、`true`に構成する必要があります。

* **サイズ**
* **幅**

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`action`|  <ul><li>アクション</li></ul> |
|`language`|  <ul><li>言語</li></ul> |
|`href`|  <ul><li>Hrefリンク</li></ul> |
|`config.colorscheme`|  <ul><li>カラースキーム</li><li>値は`light`または`dark`です</li></ul> |
|`appId`|  <ul><li>アプリID</li></ul> |
|`config.size`|  <ul><li>サイズ</li></ul> |
|`config.width`|  <ul><li>幅</li></ul> |

### Like

|変数| 説明|
|---| ---|
|`like.layout`|  <ul><li>レイアウト</li></ul> |
|`like.show_faces`|  <ul><li>顔を表示</li><li>値は`true`または`false`です。</li></ul> |
|`like.kid_directed`|  <ul><li>子供向けサイト</li><li>値は`true`または`false`です。</li></ul> |
|`like.color_scheme`|  <ul><li>カラースキーム</li><li>値は`light`または`dark`です。</li></ul> |
|`like.###`|  <ul><li>カスタムLike値</li></ul> |

### Recommend

|変数| 説明|
|---| ---|
|`rec.layout`|  <ul><li>レイアウト</li></ul> |
|`rec.show_faces`|  <ul><li>顔を表示</li><li>値は`true`または`false`です。</li></ul> |
|`rec.kid_directed`|  <ul><li>子供向けサイト</li><li>値は`true`または`false`です。</li></ul> |
|`rec.color_scheme`|  <ul><li>カラースキーム</li><li>値は`light`または`dark`です。</li></ul> |
| `rec.###` |  <ul><li>カスタムRecommend値</li></ul> |

### Share

|変数| 説明|
|---| ---|
|`share.layout`|  <ul><li>レイアウト</li></ul> |
|`share.kid_directed`|  <ul><li>子供向けサイト</li><li>値は`true`または`false`です。</li></ul> |
| `share.###` |  <ul><li>カスタムShare値</li></ul> |

### Send

|変数| 説明|
|---| ---|
|`send.kid_directed`|  <ul><li>値は`true`または`false`です。</li></ul> |
|`send.color_scheme`|  <ul><li>値は`light`または`dark`です。</li></ul> |
|`send.###`|  <ul><li>カスタムSend値</li></ul> |