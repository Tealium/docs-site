---
title: Cheetah Digitalタグ構成ガイド
description: この記事では、タグ管理アカウントでCheetah Digitalタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/cheetah-digital-tag/
---
## タグに関するヒント

* 次のEコマース拡張機能パラメータをサポートします。
  * 注文ID
  * 注文小計
  * 商品名のリスト
  * 商品数量のリスト
  * 商品価格のリスト
* マッピングを使用して、次のことができます。
  * 標準構成値を上書きする
  * Eコマース拡張機能の値を上書きする
  * 追加データを渡す

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **タグタイプ**
* **クライアントドメイン**  
クライアントドメインは、`e.clientdomain.com`など、クライアントのクリックスルードメインと同じです。クライアントが`clientname.chtah.com`を使用している場合は、`p.chtah.com`を指定します。
* **アフィリエイトID**  
追跡対象のメール配信に使用するアフィリエイトIDです。同じピクセルで複数のアフィリエイトを使用する場合は、ピリオドで区切ります。例：`123456789.987654321`。アフィリエイト数は2～3個程度に抑えてください。最大数は10です。
* **クライアント名**  
（画像タグタイプでは必須）通常はクライアント名の略称で、10文字以内の英数字名です。
* **N値**  
（iFrameタグタイプでは必須）`n`クエリ文字列パラメータの値です。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数| 説明|
|---| ---|
|`tagtype`|  <ul><li>タグタイプ</li><li>`img`または`iframe`</li></ul> |
|`cdomain`|  <ul><li>クライアントドメイン</li></ul> |
|`aid`|  <ul><li>アフィリエイトID</li></ul> |
|`cname`|  <ul><li>クライアント名</li></ul> |
|`nval`|  <ul><li>N値</li></ul> |
|`custom.myvar`|  <ul><li>カスタム</li></ul> |

### Eコマース

|変数| 説明|
|---| ---|
|`order_id`|  <ul><li>注文ID</li><li>`_corder`を上書きします。</li></ul> |
|`order_subtotal`|  <ul><li>小計</li><li>`_csubtotal`を上書きします。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>名前のリスト</li><li>`_cprodname`を上書きします。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト</li><li>`_cprice`を上書きします。</li></ul> |