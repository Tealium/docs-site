---
title: MyBuysタグの構成ガイド
description: この記事では、iQ Tag Management（TiQ）アカウントでMyBuysタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/mybuys-tag/
---
## タグの構成

まず、タグマーケットプレイスにアクセスし、MyBuysタグをプロファイルに追加します。詳細については、[タグの管理]()を参照してください。

タグを追加した後、以下の構成を構成します：

* **クライアントID：** MyBuysのクライアントID。
* **Div ID：** 推奨が表示されるページのDOM要素のID属性。
* **MySite Recommendation Zone：** 数値のゾーン番号。
* **Global CSS Path：** デフォルトのグローバルMyBuys CSSのURL（使用する場合）。
* **Client CSS Path：** クライアント固有のCSSのURL（使用する場合）。

## ロードルール

[ロードルール]()は、サイト上でこのタグのインスタンスをいつ、どこにロードするかを決定します。

推奨されるロードルール：すべてのページ。

## データマッピング

マッピングは、[データレイヤ変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法についての手順については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

以下のテーブルは、MyBuysがトラッキングするさまざまなページタイプとイベント、およびTealium iQ内での対応するデータのマッピング方法を説明しています。Universal Data Objectにはすでに`page_type`と`event_name`変数が含まれているはずです。

### ページタイプ

| MyBuysページタイプ       | Tealiumページタイプ（`page_type`） | 必須/オプション |
|:-------------------------|:----------------------------------|:----------------|
| ホーム                   | `home`                            | 必須            |
| 上位カテゴリ             | `section`                         | 必須            |
| 下位カテゴリ             | `category`                        | 必須            |
| 製品詳細                 | `product`                         | 必須            |
| 検索結果                 | `search`                          | 必須            |
| カートに追加             | `cart_add` (`event_name`)         | 必須            |
| ショッピングカートとチェックアウト | `cart`, `checkout`        | 必須            |
| 注文確認                 | `receipt`                         | 必須            |
| セール                   | `sale`                            | オプション        |
| 新着商品                 | `new_arrivals`                    | オプション        |
| ブランドホーム             | `brand_home`                      | オプション        |
| ブランド                 | `brand`                           | オプション        |
| ランディングページ         | `landing`                         | オプション        |
| マイページ               | `account`                         | オプション        |
| 製品評価                 | `product_ratings`                 | オプション        |
| メールニュースレターサインアップ | `email_signup` (`event_name`) | オプション        |

`page_type`変数の名前は、実装によって異なる場合があります。マッピングツールボックスを使用すると、TealiumのページタイプをMyBuysのページタイプに簡単に接続できます。`page_type`変数をマップするときは、「ページタイプ」タブをクリックし、Tealium UDOに表示される値を入力し、ドロップダウンメニューから対応するMyBuysページを選択します。

同じタイプのマッピングは、`event_name`変数を使用してイベントをトラッキングするためにも使用できます。

### Eコマース

Eコマース固有のデータレイヤ変数を送信するために、次の宛先にマップします。通常、この目的のためにTealiumの[Eコマース拡張機能]()を使用することをお勧めします。なぜなら、適切に構成されている場合、拡張機能はプロファイル内のすべてのEコマース対応タグの適切な宛先に変数を自動的にマップします。そのため、すべてのタグに対して変数を繰り返しマップする必要はありません。ただし、拡張機能の変数をオーバーライドするか、または拡張機能で変数が利用できない場合は、ツールボックスを使用してデータソースを宛先に手動でマップする必要があります。

## ページタイプ別の変数

これらのMyBuysページタイプには、次の変数が関連付けられています。これらの変数が[Eコマース拡張機能]()でマップされている場合、その値は自動的にMyBuysタグに渡されます。それ以外の場合は、タグの構成で明示的にマップする必要があります。なお、Tealiumの変数名は異なる場合があります。

### 上位カテゴリ

| MyBuys変数      | Tealium変数          | マッピング |
|:-----------------|:----------------------|:------------|
| categoryId       | `category_id`           | マップ      |
| addItemPresentOnPage | `product_on_page`（配列） | マップ      |

### 下位カテゴリ

| MyBuys変数      | Tealium変数          | マッピング |
|:-----------------|:----------------------|:------------|
| categoryId       | `category_id`           | マップ      |
| addItemPresentOnPage | `product_on_page`（配列） | マップ      |

### ブランドページ（オプション）

| MyBuys変数      | Tealium変数          | マッピング |
|:-----------------|:----------------------|:------------|
| brandname        | `brand_name`            | マップ      |
| addItemPresentOnPage | `product_on_page`（配列） | マップ      |

### 製品詳細ページ

| MyBuys変数      | Tealium変数          | マッピング    |
|:-----------------|:----------------------|:---------------|
| addItemPresentOnPage | `product_on_page`（配列） | マップ     |
| productId        | `product_id`（配列）     | Eコマース |

### 製品評価ページ

| MyBuys変数 | Tealium変数     | マッピング    |
|:------------|:-----------------|:---------------|
| productId   | `product_id`（配列） | Eコマース |

### 検索結果ページ

| MyBuys変数      | Tealium変数          | マッピング |
|:-----------------|:----------------------|:------------|
| addItemPresentOnPage | `product_on_page`（配列） | マップ      |

### カートに追加ページ/イベント

| MyBuys変数        | Tealium変数                                                          | マッピング             |
|:-------------------|:----------------------------------------------------------------------|:------------------------|
| email              | `customer_email`（デフォルトは`customer_id`）                              | マップ（Eコマース） |
| amount             | `cart_total_value`                                                        | マップ                  |
| optin              | `customer_optin`                                                          | マップ                  |
| addCartItemQtySubtotal | `cart_product_id`、`cart_product_quantity`、`cart_product_price`（配列） | マップ                  |

### ショッピングカートページ

| MyBuys変数        | Tealium変数                                           | マッピング             |
|:-------------------|:-------------------------------------------------------|:------------------------|
| email              | `customer_email`（デフォルトは`customer_id`）               | マップ（Eコマース） |
| amount             | `cart_total_value`                                         | マップ                  |
| optin              | `customer_optin`                                           | マップ                  |
| addCartItemQtySubtotal | `product_id`、`product_quantity`、`product_price`（配列） | Eコマース          |

### 注文確認ページ

| MyBuys変数        | Tealium変数                                           | マッピング             |
|:-------------------|:-------------------------------------------------------|:------------------------|
| email              | `customer_email`（デフォルトは`customer_id`）               | マップ（Eコマース） |
| orderId            | `order_id`                                                 | Eコマース          |
| amount             | `order_subtotal`                                           | Eコマース          |
| optin              | `customer_optin`                                           | マップ                  |
| addCartItemQtySubtotal | `product_id`、`product_quantity`、`product_price`（配列） | Eコマース          |

### メールサインアップページ/イベント

| MyBuys変数 | Tealium変数                             | マッピング             |
|:------------|:-----------------------------------------|:------------------------|
| email       | `customer_email`（デフォルトは`customer_id`） | マップ（Eコマース） |
| gender      | `customer_gender`                        | マップ                  |
| zipcode     | `customer_postal_code`                   | Eコマース          |

Tealium iQでのサンプルのMyBuys変数マッピング：

![](/images/client-side-tags/tealium-mybuys-mapped-sources.jpg)

### MySite推奨ゾーン

MySite推奨ゾーンは、DIV IDとゾーン番号を指定して構成できます。DIV IDは、推奨が表示されるページのHTMLタグの`id`属性を参照する必要があります。ゾーン番号は、MyBuysの推奨に作成された数値のゾーンと一致する必要があります。適切な配置を確保するために、これらのHTML要素をページにハードコードすることをお勧めします。

例：

```html
&lt;body&gt;
...
&lt;div id=&#34;mybuys1&#34;&gt;&lt;/div&gt;
...
&lt;/body&gt;
```

ページごとに複数のゾーンを構成するには、`divs`と`zones`変数の追加のマッピングが必要です。これらの変数の値は、DIV IDのリストとそれに対応するゾーン番号のリストを含む配列である必要があります。

この例では、`mb_divs`と`mb_zones`を新しい変数として定義し、それぞれの値を配列として構成しています。配列は**JSコード**の割り当てオプションを使用してポピュレートできます。ゾーンは、ページごとに構成することができます。条件ごとに複数の拡張機能を作成することで、ゾーンを構成できます。

製品詳細ページで複数のゾーンを構成する例：

![](/images/client-side-tags/tealium-mybuys-multiple-zones.jpg)

結果：

```
// 製品ページ（page_typeが &#34;product&#34; の場合）
b.mb_divs = [&#34;mybuys1&#34;, &#34;mybuys2&#34;, &#34;mybuys3&#34;]
b.mb_zones = [&#34;1&#34;, &#34;2&#34;, &#34;3&#34;]
```

## タグの検証

MyBuysタグは、Tealium内部と外部で同じように動作するはずです。MyBuysタグが正常に動作しているかどうかを確認する最も簡単な方法は、ページの読み込み時にネットワークトラフィックを検査することです。TealiumがMyBuysタグをロードして発火する際に、CSSファイル、JavaScriptコードファイル、および最終的なピクセルコールを取得するためにMyBuysサーバーに対していくつかのリクエストが行われます。

