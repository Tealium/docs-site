---
title: Adition (Track) タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAdition (Track)タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/adition-track-tag/
---
## タグのヒント

* これはAditionのトラックバージョンです。
* Aditionとの契約に従ってドメインを構成します。

  * デフォルト値: `adfarm1.adition.com`
  * AdfarmID: `ad&lt;id&gt;.adfarm1.adition.com`
  * カスタム: `&lt;subdomain&gt;.&lt;domain&gt;.&lt;tld&gt;`

* デフォルトの戻りタイプは `img` です。
* 次のE-コマース変数を使用します

  * `_cprod`
  * `_cquan`
  * `_cprice`
  * `_corder`

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Adition (Track)タグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加したら、次の構成を行います：

* **ドメイン**
  * Aditionから提供されるドメイン。
  * デフォルトのドメインは `adfarm1.adition.com` です。

* **TID**
  * 必須。
  * Aditionの広告配信システム内のランディングページを表します。

* **SID**
  * 必須。
  * Aditionの広告配信システム内のトラッキングスポットを表します。

* **タグタイプ**:

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|タグタイプ|  &lt;ul&gt;&lt;li&gt;タグタイプ&lt;/li&gt;&lt;/ul&gt; |
|ドメイン|  &lt;ul&gt;&lt;li&gt;ドメイン&lt;/li&gt;&lt;/ul&gt; |
| `tid` |  &lt;ul&gt;&lt;li&gt;ランディングページID&lt;/li&gt;&lt;/ul&gt; |
| `sid` |  &lt;ul&gt;&lt;li&gt;トラッキングスポットID&lt;/li&gt;&lt;/ul&gt; |
|`orderid`|  &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;`_corder` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`descr`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;アイテムの説明。&lt;/li&gt;&lt;li&gt;`_cprod` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `quantity` |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;アイテムの数量。&lt;/li&gt;&lt;li&gt;`_cquan` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;アイテムの価格。&lt;/li&gt;&lt;li&gt;`_cprice` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`total`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;合計価格。&lt;/li&gt;&lt;/ul&gt; |
|`param`|  &lt;ul&gt;&lt;li&gt;パラメータ&lt;/li&gt;&lt;li&gt;値は1 - 20です。&lt;/li&gt;&lt;/ul&gt; |

