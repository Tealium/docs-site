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

タグマーケットプレイスにアクセスして新しいタグを追加します。タグを追加する方法についての詳細は、[タグの管理](https://docs.tealium.com/manage-tags/)を参照してください。

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

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法の指示については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`tagtype`|  <ul><li>タグタイプ</li><li>`img` または `iframe`</li></ul> |
|`cdomain`|  <ul><li>クライアントドメイン</li></ul> |
|`aid`|  <ul><li>アフィリエイトID</li></ul> |
|`cname`|  <ul><li>クライアント名</li></ul> |
|`nval`|  <ul><li>N値</li></ul> |
|`custom.myvar`|  <ul><li>カスタム</li></ul> |

### Eコマース

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID</li><li>`_corder`を上書き。</li></ul> |
|`order_subtotal`|  <ul><li>小計</li><li>`_csubtotal`を上書き。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>名前のリスト</li><li>`_cprodname`を上書き。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト</li><li>`_cquan`を上書き。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト</li><li>`_cprice`を上書き。</li></ul> |