---
title: Magellan AI S2Sコネクタ構成ガイド
description: この記事では、Magellan AI S2Sコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/magellan-ai-s2s-connector/
---
## API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：Magellan AI S2S API
* APIエンドポイント：`https://mgln.ai`

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **Magellan Pixel Token**：Magellan AIのピクセルトークンです。すべてのイベントをMagellanアカウントに関連付けます。この値はMagellan AIダッシュボードで確認できます。

コネクタを構成したら、**Done**をクリックします。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| ----------- | :------------: | :---------: |
| Send Event | ✓ | ✓ |

### Send Event

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| Event Type | （必須）Magellanイベントタイプを選択します。エンドポイントのパスを決定し、そのイベントに関連するフィールドを制御します。<br>Page View<br>Lead<br>Product<br>Add to Cart<br>Checkout<br>Purchase<br>Identify<br>Code |
| Category | （任意）リードの送信に使用したアクションのタイプ（例：`formFill`または`ButtonClick`）。 |
| Code | （Codeイベントでは必須）追跡対象のクーポンコードまたは紹介コード。紹介者を伴うアカウント作成でよく使用されます。この場合、紹介コードをコードとして渡し、`type`を`referrer`に構成します。購入イベントでDiscount Codeを使用する場合は不要です。 |
| Currency | （リード、商品、カートへの追加、チェックアウト、および購入イベントでは必須）イベントの通貨。リード、商品、カートへの追加、チェックアウト、および購入イベントでは、`_ccurrency`に自動マッピングされます。 |
| Discount Code | （任意）チェックアウトおよび購入イベントの割引コードまたはプロモーションコード。チェックアウトおよび購入イベントでは、`_cpromo`に自動マッピングされます。 |
| ID | イベントごとに異なる用途で使用される一意のID：<ul><li><code>identify</code> — ユーザーID（必須）。</li><li><code>view</code> — ユーザーID（任意）。</li><li><code>lead</code> — ユーザーID（任意）。</li><li><code>checkout</code> — 注文ID（任意）。</li><li><code>purchase</code> — 注文ID（必須）。</li></ul>チェックアウトおよび購入イベントでは、<code>_corder</code>に自動マッピングされます。 |
| IP Address | （必須）クライアントのIPアドレス。Client IP属性に自動マッピングされます。 |
| Is New Customer | （任意）顧客がリピーターでない場合は`true`に構成します。文字列値はブール値に変換されます。 |
| Items Product ID | （任意）商品IDの並列配列。チェックアウトおよび購入イベントでは、`_cprod`に自動マッピングされます。 |
| Items Product Name | （任意）商品名の並列配列。チェックアウトおよび購入イベントでは、`_cprodname`に自動マッピングされます。 |
| Items Product Type | （任意）商品タイプ／カテゴリーの並列配列。チェックアウトおよび購入イベントでは、`_ccat`に自動マッピングされます。 |
| Items Product Vendor | （任意）商品のベンダーの並列配列。チェックアウトおよび購入イベントでは、`_cbrand`に自動マッピングされます。 |
| Items Quantity | （任意）商品の数量の並列配列。チェックアウトおよび購入イベントでは、`_cquan`に自動マッピングされます。 |
| Items Variant ID | （任意）バリエーションIDの並列配列。チェックアウトおよび購入イベントでは、`_csku`に自動マッピングされます。 |
| Items Variant Name | （任意）バリエーション名の並列配列。 |
| Product ID | （任意）商品のID。リード、商品、およびカートへの追加イベントでは、`_cprod`に自動マッピングされます（文字列に変換されます）。 |
| Product Name | （任意）商品の名前。 |
| Product Type | （任意）商品のタイプ（例：`Women's Shoes`）。 |
| Product Vendor | （任意）商品のベンダー。 |
| Quantity | （任意）イベントの数量。リード、カートへの追加、チェックアウト、および購入イベントでは、`_cquan`に自動マッピングされます（数値に変換されます）。 |
| Referrer URL | （任意）参照元URLアドレス。ページビューイベントでは、`dom.referrer`から自動マッピングされます。 |
| Type | （任意）イベントのカテゴリーラベル。リードイベントでは、リードアクションのタイプを指定するために使用します（例：`Sales Demo`、`Account Creation`、`Newsletter signup`）。Codeイベントでは、コードのタイプを指定するために使用します（例：`referrer`）。 |
| URL | （ページビューイベントでは必須）イベントのURL。ビューイベントでは、Current URL属性に自動マッピングされます。 |
| Value | （リード、商品、カートへの追加、チェックアウト、および購入イベントでは必須）イベントごとに異なる用途で使用される値：<ul><li><code>lead</code> — リードに割り当てられた合計値。Leadイベントでは、デフォルト値は<code>0</code>です。</li><li><code>product</code> — 商品ごとの値。</li><li><code>add_to_cart</code> — カートに追加された合計金額。</li><li><code>checkout</code> — カートの合計金額。</li><li><code>purchase</code> — 注文の合計金額。</li></ul>チェックアウトおよび購入イベントでは<code>_ctotal</code>に、カートへの追加および商品イベントでは<code>_cprice</code>の合計に自動マッピングされます。 |
| Variant ID | （任意）商品のバリエーションID。 |
| Variant Name | （任意）商品のバリエーション名。 |
| Pixel Token Override | （任意）このアクションについて、コネクタレベルのMagellan Pixel Tokenを上書きします。異なるイベントが異なるMagellanピクセルに属する場合に使用します。 |
| Disable E-Commerce Automapping | E-Commerceの自動マッピングを無効にすると、標準のコマース属性（**Currency**、**Order ID**、**Value**、**Quantity**、**Product ID**、**Discount Code**、**Line Items**）は、Tealium UDO属性から自動マッピングされません。Event DataセクションとLine Itemsセクションで、これらのフィールドを手動でマッピングしてください。 |
| Disable Identifiers Automapping | Identifiersの自動マッピングを無効にすると、**IP Address**はClient IP属性から自動マッピングされません。Event DataセクションでIP Addressフィールドを手動でマッピングしてください。 |