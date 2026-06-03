---
title: チーターデジタルタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでチーターデジタルタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/cheetah-digital-tag/
---
## タグのヒント

* 次のEコマース拡張パラメータをサポートしています：
  * 注文ID
  * 注文小計
  * 製品名のリスト
  * 製品数量のリスト
  * 製品価格のリスト
* マッピングを使用して：
  * 標準の構成値を上書きする
  * Eコマース拡張値を上書きする
  * 追加データを渡す

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグを追加する方法についての詳細は、[タグの管理]()を参照してください。

タグを追加する際に、以下の構成を構成します：

* **タグタイプ**
* **クライアントドメイン**  
クライアントドメインは、クライアントのクリックスルードメインと同じです。例えば `e.clientdomain.com`。クライアントが `clientname.chtah.com` を使用している場合、これは `p.chtah.com` であるべきです。
* **アフィリエイトID**  
メーリングを追跡するために使用されるアフィリエイトID。同じピクセル内の複数のアフィリエイトの場合、アフィリエイトを区切るためにピリオドを使用します。例：`123456789.987654321`。アフィリエイトの数は2から3個が望ましいです。最大は10です。
* **クライアント名**  
（画像タグタイプに必要）アルファベットと数字の名前、10文字以下、通常はクライアント名の略称です。
* **N値**  
（iFrameタグタイプに必要）`n`クエリストリングパラメータの値。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法の指示については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`tagtype`|  &lt;ul&gt;&lt;li&gt;タグタイプ&lt;/li&gt;&lt;li&gt;`img` または `iframe`&lt;/li&gt;&lt;/ul&gt; |
|`cdomain`|  &lt;ul&gt;&lt;li&gt;クライアントドメイン&lt;/li&gt;&lt;/ul&gt; |
|`aid`|  &lt;ul&gt;&lt;li&gt;アフィリエイトID&lt;/li&gt;&lt;/ul&gt; |
|`cname`|  &lt;ul&gt;&lt;li&gt;クライアント名&lt;/li&gt;&lt;/ul&gt; |
|`nval`|  &lt;ul&gt;&lt;li&gt;N値&lt;/li&gt;&lt;/ul&gt; |
|`custom.myvar`|  &lt;ul&gt;&lt;li&gt;カスタム&lt;/li&gt;&lt;/ul&gt; |

### Eコマース

|変数| 説明|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文ID&lt;/li&gt;&lt;li&gt;`_corder`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;小計&lt;/li&gt;&lt;li&gt;`_csubtotal`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;名前のリスト&lt;/li&gt;&lt;li&gt;`_cprodname`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト&lt;/li&gt;&lt;li&gt;`_cquan`を上書き。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト&lt;/li&gt;&lt;li&gt;`_cprice`を上書き。&lt;/li&gt;&lt;/ul&gt; |