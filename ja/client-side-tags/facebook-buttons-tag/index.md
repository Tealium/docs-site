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

まず、Tealiumのタグマーケットプレイスに移動し、Facebookボタンタグを追加します（[タグの追加方法]()について詳しくはこちらをご覧ください）。

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

マッピングとは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`action`|  &lt;ul&gt;&lt;li&gt;アクション&lt;/li&gt;&lt;/ul&gt; |
|`language`|  &lt;ul&gt;&lt;li&gt;言語&lt;/li&gt;&lt;/ul&gt; |
|`href`|  &lt;ul&gt;&lt;li&gt;Hrefリンク&lt;/li&gt;&lt;/ul&gt; |
|`config.colorscheme`|  &lt;ul&gt;&lt;li&gt;カラースキーム&lt;/li&gt;&lt;li&gt;値は`light`または`dark`&lt;/li&gt;&lt;/ul&gt; |
|`appId`|  &lt;ul&gt;&lt;li&gt;アプリID&lt;/li&gt;&lt;/ul&gt; |
|`config.size`|  &lt;ul&gt;&lt;li&gt;サイズ&lt;/li&gt;&lt;/ul&gt; |
|`config.width`|  &lt;ul&gt;&lt;li&gt;幅&lt;/li&gt;&lt;/ul&gt; |

### Like

|変数| 説明|
|---| ---|
|`like.layout`|  &lt;ul&gt;&lt;li&gt;レイアウト&lt;/li&gt;&lt;/ul&gt; |
|`like.show_faces`|  &lt;ul&gt;&lt;li&gt;顔を表示&lt;/li&gt;&lt;li&gt;値は`true`または`false`。&lt;/li&gt;&lt;/ul&gt; |
|`like.kid_directed`|  &lt;ul&gt;&lt;li&gt;子供向けサイト&lt;/li&gt;&lt;li&gt;値は`true`または`false`。&lt;/li&gt;&lt;/ul&gt; |
|`like.color_scheme`|  &lt;ul&gt;&lt;li&gt;カラースキーム&lt;/li&gt;&lt;li&gt;値は`light`または`dark`。&lt;/li&gt;&lt;/ul&gt; |
|`like.###`|  &lt;ul&gt;&lt;li&gt;カスタムLike値&lt;/li&gt;&lt;/ul&gt; |

### Recommend

|変数| 説明|
|---| ---|
|`rec.layout`|  &lt;ul&gt;&lt;li&gt;レイアウト&lt;/li&gt;&lt;/ul&gt; |
|`rec.show_faces`|  &lt;ul&gt;&lt;li&gt;顔を表示&lt;/li&gt;&lt;li&gt;値は`true`または`false`。&lt;/li&gt;&lt;/ul&gt; |
|`rec.kid_directed`|  &lt;ul&gt;&lt;li&gt;子供向けサイト&lt;/li&gt;&lt;li&gt;値は`true`または`false`。&lt;/li&gt;&lt;/ul&gt; |
|`rec.color_scheme`|  &lt;ul&gt;&lt;li&gt;カラースキーム&lt;/li&gt;&lt;li&gt;値は`light`または`dark`。&lt;/li&gt;&lt;/ul&gt; |
| `rec.###` |  &lt;ul&gt;&lt;li&gt;カスタムRecommend値&lt;/li&gt;&lt;/ul&gt; |

### Share

|変数| 説明|
|---| ---|
|`share.layout`|  &lt;ul&gt;&lt;li&gt;レイアウト&lt;/li&gt;&lt;/ul&gt; |
|`share.kid_directed`|  &lt;ul&gt;&lt;li&gt;子供向けサイト&lt;/li&gt;&lt;li&gt;値は`true`または`false`。&lt;/li&gt;&lt;/ul&gt; |
| `share.###` |  &lt;ul&gt;&lt;li&gt;カスタムShare値&lt;/li&gt;&lt;/ul&gt; |

### Send

|変数| 説明|
|---| ---|
|`send.kid_directed`|  &lt;ul&gt;&lt;li&gt;値は`true`または`false`。&lt;/li&gt;&lt;/ul&gt; |
|`send.color_scheme`|  &lt;ul&gt;&lt;li&gt;値は`light`または`dark`。&lt;/li&gt;&lt;/ul&gt; |
|`send.###`|  &lt;ul&gt;&lt;li&gt;カスタムSend値&lt;/li&gt;&lt;/ul&gt; |
