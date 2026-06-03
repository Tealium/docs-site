---
title: 小売データレイヤー仕様
description: この記事では小売のためのデータレイヤー定義を提供します。
url: https://docs.tealium.com/ja/platforms/getting-started-web/data-layer/definitions/retail/
---## データレイヤー属性

|変数| 説明| 例| タイプ|
|---| ---| ---| ---|
|`brand_name`| ブランド固有のページのブランド名| `Ralph Lauren`| 文字列|
|`browse_refine_type`| 絞り込みタイプの配列| `[&#34;Size&#34;, &#34;Color&#34;]`| 配列|
|`browse_refine_value`| 絞り込み値の配列| `[&#34;XL&#34;, &#34;Red&#34;]`| 配列|
|`cart_product_id`| `cart_add` イベント時、カート内の全商品IDの配列| `[&#34;PROD123&#34;, &#34;PROD456&#34;]` | 配列|
|`cart_product_price`| `cart_add` イベント時、カート内の全商品価格の配列| `[&#34;12.99&#34;, &#34;25.99&#34;]`| 配列|
|`cart_product_quantity`| `cart_add` イベント時、カート内の全商品数量の配列| `[&#34;2&#34;, &#34;2&#34;]`| 配列|
|`cart_product_sku`| `cart_add` イベント時、カート内の全商品SKUの配列| `[&#34;PR-RED-1234&#34;, &#34;PR-BLK-6789&#34;]` | 配列|
|`cart_total_items`| カート内の商品総数| `4`| 文字列|
|`cart_total_value`| カート内の商品総価値（数字と小数点のみの文字列）| `77.96`| 文字列|
|`category_id`| 閲覧中のカテゴリーの一意のID| `243`| 文字列|
|`category_name`| 閲覧中のカテゴリーのユーザーフレンドリーな名前| `Shoes: Boots`| 文字列|
|`country_code`| 国コード| `us`| 文字列|
|`customer_city`| 顧客の居住都市| `San Diego`| 文字列|
|`customer_country`| 顧客の居住国| `United States`| 文字列|
|`customer_email`| 顧客のメールアドレス| `user@example.com`| 文字列|
|`customer_first_name`| 顧客の名| `John`| 文字列|
|`customer_id`| 顧客の一意のID| `8237572`| 文字列|
|`customer_last_name`| 顧客の姓| `Smith`| 文字列|
|`customer_postal_code`| 顧客の郵便番号| `92101`| 文字列|
|`customer_state`| 顧客の居住州| `CA`| 文字列|
|`event_name`| ユニークなイベントを識別するTealium変数| `cart_add`| 文字列|
|`language_code`| 言語コード| `en`| 文字列|
|`link_category`| クリック追跡イベント時、クリックされた要素のカテゴリー| `Header`| 文字列|
|`link_name`| クリック追跡イベント時、クリックされた要素の名前| `Login`| 文字列|
|`order_currency_code`| サイトの通貨コード| `USD`| 文字列|
|`order_discount_amount`| 注文レベルの割引額| `10.00`| 文字列|
|`order_id`| 注文の一意のID、注文確認ページでのみ入力| `ORD123456`| 文字列|
|`order_merchandise_total`| 商品や注文レベルの割引、税金、送料を除く全商品の価格（数字と小数点のみの文字列）| `55.98`| 文字列|
|`order_payment_type`| 支払いタイプ| `Paypal`| 文字列|
|`order_promo_code`| プロモーションコードのカンマ区切りの文字列リスト| `PROMO10`| 文字列|
|`order_shipping_amount`| 配送料の総額（数字と小数点のみの文字列）| `6.99`| 文字列|
|`order_shipping_type`| 配送タイプ| `UPS`| 文字列|
|`order_store`| ストアタイプの識別子| `mobile web`| 文字列|
|`order_subtotal`| 商品や注文レベルの割引を含む全商品の価格、ただし税金と送料は除く（数字と小数点のみの文字列）| `45.98`| 文字列|
|`order_tax_amount`| この注文の総税額（数字と小数点のみの文字列）| `2.50`| 文字列|
|`order_total`| 全割引を除いた税金と送料を含む注文総額（数字と小数点のみの文字列）| `54.47`| 文字列|
|`order_type`| 発生したばかりの変換のタイプまたはサイト上のユーザーのタイプ| `email`| 文字列|
|`page_name`| ページ名を識別するTealium変数| `Homepage`| 文字列|
|`page_type`| ページのタイプ| `product`| 文字列|
|`product_brand`| 商品ブランドの配列| `[&#34;Ralph Lauren&#34;, &#34;Lucky&#34;]`| 配列|
|`product_category`| 商品カテゴリの配列| `[&#34;Shirts&#34;, &#34;Pants&#34;]`| 配列|
|`product_discount_amount`| 商品レベルのクーポンによる割引額の配列（数字と小数点のみの文字列）| `[&#34;2.98&#34;, &#34;0.00&#34;]`| 配列|
|`product_id`| 商品IDの配列| `[&#34;PROD123&#34;, &#34;PROD456&#34;]`| 配列|
|`product_image_url`| 主要商品画像のURLの配列| `[&#34;//domain.com/123.gif&#34;, &#34;//domain.com/456.gif&#34;]` | 配列|
|`product_name`| 商品名の配列| `[&#34;Product One&#34;, &#34;Expensive Product Two&#34;]` | 配列|
|`product_on_page`| ページ上に表示される他の商品の商品IDの配列| `[&#34;PROD123&#34;, &#34;PROD456&#34;]`| 配列|
|`product_original_price`| 元の提案小売商品価格の配列、カンマと記号を省略| `[&#34;29.99&#34;, &#34;1015.00&#34;]`| 配列|
|`product_price`| 商品販売価格の配列、カンマと記号を省略| `[&#34;12.99&#34;, &#34;1010.98&#34;]`| 配列|
|`product_promo_code`| 特定の商品に適用されたプロモーション/クーポンコードの配列| `[&#34;SHIRT10OFF&#34;,&#34;PROMO10&#34;]`| 配列|
|`product_quantity`| 各商品の数量の配列| `[&#34;2&#34;,&#34;2&#34;]`| 配列|
|`product_sku`| 商品SKUの配列| `[&#34;PR-RED-1234&#34;, &#34;PR-BLK-6789&#34;]` | 配列|
|`product_subcategory`| 商品サブカテゴリの配列| `[&#34;T-Shirts&#34;, &#34;Dress Pants&#34;]`| 配列|
|`product_url`| 個々の商品ページへのURLの配列| `[&#34;//domain.com/123.html&#34;, &#34;//domain.com/456/html&#34;]` | 配列|
|`search_keyword`| ユーザーが入力した検索テキストの値| `cargo`| 文字列|
|`search_results`| 検索によって返された結果の数| `42`| 文字列|
|`site_section`| サイトの高レベルセクション| `Clothing`| 文字列|

## 追跡されるページ

### ホームページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `page_view`| ホームページ。|`http://www.example.com/`|

サンプル:  
```javascript
{
    &#34;cart_total_items&#34; : &#34;4&#34;,
    &#34;cart_total_value&#34; : &#34;77.96&#34;,
    &#34;country_code&#34;     : &#34;us&#34;,
    &#34;language_code&#34;    : &#34;en&#34;,
    &#34;page_name&#34;        : &#34;Homepage&#34;,
    &#34;page_type&#34;        : &#34;home&#34;,
    &#34;site_section&#34;     : &#34;Clothing&#34;,
    &#34;tealium_event&#34;    : &#34;page_view&#34;
}
```

### セクションページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `page_view`| 親カテゴリまたはトップレベルセクションページ。| `http://www.example.com/top-level/`|

サンプル:  
```javascript
{
    &#34;brand_name&#34;        : &#34;Ralph Lauren&#34;,
    &#34;cart_total_items&#34;  : &#34;4&#34;,
    &#34;cart_total_value&#34;  : &#34;77.96&#34;,
    &#34;category_id&#34;       : &#34;243&#34;,
    &#34;category_name&#34;     : &#34;Shoes: Boots&#34;,
    &#34;country_code&#34;      : &#34;us&#34;,
    &#34;language_code&#34;     : &#34;en&#34;,
    &#34;page_name&#34;         : &#34;Homepage&#34;,
    &#34;page_type&#34;         : &#34;section&#34;,
    &#34;product_on_page&#34;   : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;site_section&#34;      : &#34;Clothing&#34;,
    &#34;tealium_event&#34;     : &#34;page_view&#34;
}
```

### カテゴリーページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `category_view`| 通常、商品リストを表示するカテゴリーページ。| `http://www.example.com/top-level/sub-level/`|

サンプル:  
```javascript
{
    &#34;brand_name&#34;           : &#34;Ralph Lauren&#34;,
    &#34;browse_refine_type&#34;   : [&#34;Size&#34;, &#34;Color&#34;],
    &#34;browse_refine_value&#34;  : [&#34;XL&#34;, &#34;Red&#34;],
    &#34;cart_total_items&#34;     : &#34;4&#34;,
    &#34;cart_total_value&#34;     : &#34;77.96&#34;,
    &#34;category_id&#34;          : &#34;243&#34;,
    &#34;category_name&#34;        : &#34;Shoes: Boots&#34;,
    &#34;country_code&#34;         : &#34;us&#34;,
    &#34;language_code&#34;        : &#34;en&#34;,
    &#34;page_name&#34;            : &#34;Homepage&#34;,
    &#34;page_type&#34;            : &#34;category&#34;,
    &#34;product_on_page&#34;      : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;site_section&#34;         : &#34;Clothing&#34;,
    &#34;tealium_event&#34;        : &#34;category_view&#34;
}
```
### 商品ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `product_view`| 商品詳細ページです。| `http://www.example.com/top-level/sub-level/product.html`|

サンプル:  
```javascript
{
    &#34;cart_total_items&#34;        : &#34;4&#34;,
    &#34;cart_total_value&#34;        : &#34;77.96&#34;,
    &#34;category_id&#34;             : &#34;243&#34;,
    &#34;category_name&#34;           : &#34;靴: ブーツ&#34;,
    &#34;country_code&#34;            : &#34;us&#34;,
    &#34;language_code&#34;           : &#34;en&#34;,
    &#34;page_name&#34;               : &#34;ホームページ&#34;,
    &#34;page_type&#34;               : &#34;product&#34;,
    &#34;product_brand&#34;           : [&#34;Ralph Lauren&#34;, &#34;Lucky&#34;],
    &#34;product_category&#34;        : [&#34;シャツ&#34;, &#34;パンツ&#34;],
    &#34;product_id&#34;              : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;product_image_url&#34;       : [&#34;//domain.com/path/image.gif&#34;],
    &#34;product_name&#34;            : [&#34;商品一&#34;, &#34;高級商品二&#34;],
    &#34;product_on_page&#34;         : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;product_original_price&#34;  : [&#34;29.99&#34;, &#34;1015.00&#34;],
    &#34;product_price&#34;           : [&#34;12.99&#34;, &#34;1010.98&#34;],
    &#34;product_sku&#34;             : [&#34;PR-RED-1234&#34;, &#34;PR-BLK-6789&#34;],
    &#34;product_subcategory&#34;     : [&#34;Tシャツ&#34;, &#34;ドレスパンツ&#34;],
    &#34;product_url&#34;             : [&#34;//domain.com/cat/prod/prod123.html&#34;],
    &#34;site_section&#34;            : &#34;衣類&#34;,
    &#34;tealium_event&#34;           : &#34;product_view&#34;
}
```

### 検索ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `search`| 検索結果ページです。| `http://www.example.com/search?query=term`|

サンプル:  
```javascript
{
    &#34;browse_refine_type&#34;   : [&#34;サイズ&#34;, &#34;色&#34;],
    &#34;browse_refine_value&#34;  : [&#34;XL&#34;, &#34;赤&#34;],
    &#34;cart_total_items&#34;     : &#34;4&#34;,
    &#34;cart_total_value&#34;     : &#34;77.96&#34;,
    &#34;country_code&#34;         : &#34;us&#34;,
    &#34;language_code&#34;        : &#34;en&#34;,
    &#34;page_name&#34;            : &#34;ホームページ&#34;,
    &#34;page_type&#34;            : &#34;search&#34;,
    &#34;product_on_page&#34;      : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;search_keyword&#34;       : &#34;カーゴ&#34;,
    &#34;search_results&#34;       : &#34;42&#34;,
    &#34;site_section&#34;         : &#34;衣類&#34;,
    &#34;tealium_event&#34;        : &#34;search&#34;
}
```

### カートページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `cart_view`| ショッピングカートページで、カートの商品内容が表示されます。| `http://www.example.com/cart`|

サンプル:  
```javascript
{
    &#34;cart_total_items&#34;         : &#34;2&#34;,
    &#34;cart_total_value&#34;         : &#34;2524.00&#34;,
    &#34;country_code&#34;             : &#34;us&#34;,
    &#34;language_code&#34;            : &#34;en&#34;,
    &#34;page_name&#34;                : &#34;ショッピングバッグ&#34;,
    &#34;page_type&#34;                : &#34;cart&#34;,
    &#34;product_brand&#34;            : [&#34;Ralph Lauren&#34;, &#34;Lucky&#34;],
    &#34;product_category&#34;         : [&#34;シャツ&#34;, &#34;パンツ&#34;],
    &#34;product_discount_amount&#34;  : [&#34;2.98&#34;, &#34;0.00&#34;],
    &#34;product_id&#34;               : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;product_image_url&#34;        : [&#34;//domain.com/path/image123.gif&#34;,
                                  &#34;//domain.com/path/image456.gif&#34;],
    &#34;product_name&#34;             : [&#34;商品一&#34;, &#34;高級商品二&#34;],
    &#34;product_price&#34;            : [&#34;12.00&#34;, &#34;1250.00&#34;],
    &#34;product_promo_code&#34;       : [&#34;SHIRT10OFF&#34;,&#34;&#34;],
    &#34;product_quantity&#34;         : [&#34;2&#34;,&#34;2&#34;],
    &#34;product_sku&#34;              : [&#34;PR-RED-1234&#34;, &#34;PR-BLK-6789&#34;],
    &#34;product_subcategory&#34;      : [&#34;Tシャツ&#34;, &#34;ドレスパンツ&#34;],
    &#34;product_url&#34;              : [&#34;//domain.com/cat/prod/prod123.html&#34;,
                                  &#34;//domain.com/cat/prod/prod456.html&#34;],
    &#34;tealium_event&#34;            : &#34;cart_view&#34;
}
```

### チェックアウトページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `checkout`| 通常は配送、支払い、請求情報ページのチェックアウトページです。| `http://www.example.com/checkout/billing/shipping`|

サンプル:  
```javascript
{
    &#34;cart_total_items&#34;  : &#34;2&#34;,
    &#34;cart_total_value&#34;  : &#34;2524.00&#34;,
    &#34;country_code&#34;      : &#34;us&#34;,
    &#34;language_code&#34;     : &#34;en&#34;,
    &#34;page_name&#34;         : &#34;チェックアウト：支払い&#34;,
    &#34;page_type&#34;         : &#34;checkout&#34;,
    &#34;tealium_event&#34;     : &#34;checkout&#34;
}
```

### 注文ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `purchase`| 注文確認（「ありがとうございます」）ページです。| `http://www.example.com/checkout/success/order.html`|

サンプル:  
```javascript
{
    &#34;cart_total_items&#34;         : &#34;2&#34;,
    &#34;cart_total_value&#34;         : &#34;2524.00&#34;,
    &#34;country_code&#34;             : &#34;us&#34;,
    &#34;customer_city&#34;            : &#34;サンディエゴ&#34;,
    &#34;customer_country&#34;         : &#34;アメリカ合衆国&#34;,
    &#34;customer_email&#34;           : &#34;john.smith@example.com&#34;,
    &#34;customer_first_name&#34;      : &#34;ジョン&#34;,
    &#34;customer_id&#34;              : &#34;8237572&#34;,
    &#34;customer_last_name&#34;       : &#34;スミス&#34;,
    &#34;customer_postal_code&#34;     : &#34;92101&#34;,
    &#34;customer_state&#34;           : &#34;CA&#34;,
    &#34;language_code&#34;            : &#34;en&#34;,
    &#34;order_currency_code&#34;      : &#34;USD&#34;,
    &#34;order_discount_amount&#34;    : &#34;10.00&#34;,
    &#34;order_id&#34;                 : &#34;ORD123456&#34;,
    &#34;order_payment_type&#34;       : &#34;paypal&#34;,
    &#34;order_promo_code&#34;         : &#34;SPRFREE,PROMO10&#34;,
    &#34;order_shipping_amount&#34;    : &#34;6.99&#34;,
    &#34;order_shipping_type&#34;      : &#34;UPS&#34;,
    &#34;order_store&#34;              : &#34;モバイルウェブ&#34;,
    &#34;order_subtotal&#34;           : &#34;2524.00&#34;,
    &#34;order_tax_amount&#34;         : &#34;25.00&#34;,
    &#34;order_total&#34;              : &#34;2549.00&#34;,
    &#34;page_name&#34;                : &#34;注文確認 - ありがとう&#34;,
    &#34;page_type&#34;                : &#34;order&#34;,
    &#34;product_brand&#34;            : [&#34;Ralph Lauren&#34;, &#34;Lucky&#34;],
    &#34;product_category&#34;         : [&#34;シャツ&#34;, &#34;パンツ&#34;],
    &#34;product_discount_amount&#34;  : [&#34;5.00&#34;, &#34;0.00&#34;],
    &#34;product_id&#34;               : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;product_image_url&#34;        : [&#34;//domain.com/path/image123.gif&#34;,
                                  &#34;//domain.com/path/image456.gif&#34;],
    &#34;product_name&#34;             : [&#34;商品一&#34;, &#34;高級商品二&#34;],
    &#34;product_price&#34;            : [&#34;12.00&#34;, &#34;1250.00&#34;],
    &#34;product_promo_code&#34;       : [&#34;SHIRT10OFF&#34;,&#34;&#34;],
    &#34;product_quantity&#34;         : [&#34;2&#34;,&#34;2&#34;],
    &#34;product_sku&#34;              : [&#34;PR-RED-1234&#34;, &#34;PR-BLK-6789&#34;],
    &#34;product_subcategory&#34;      : [&#34;Tシャツ&#34;, &#34;ドレスパンツ&#34;],
    &#34;product_url&#34;              : [&#34;//domain.com/cat/prod/prod123.html&#34;,
                                  &#34;//domain.com/cat/prod/prod456.html&#34;],
    &#34;tealium_event&#34;            : &#34;purchase&#34;
}
```

### アカウントページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `page_view`| ユーザーアカウントプロファイルページです。| `http://www.example.com/account/profile`|

サンプル:  
```javascript
{
    &#34;cart_total_items&#34;      : &#34;4&#34;,
    &#34;cart_total_value&#34;      : &#34;77.96&#34;,
    &#34;country_code&#34;          : &#34;us&#34;,
    &#34;customer_city&#34;         : &#34;サンディエゴ&#34;,
    &#34;customer_country&#34;      : &#34;アメリカ合衆国&#34;,
    &#34;customer_email&#34;        : &#34;johnsmith@example.com&#34;,
    &#34;customer_first_name&#34;   : &#34;ジョン&#34;,
    &#34;customer_id&#34;           : &#34;8237572&#34;,
    &#34;customer_last_name&#34;    : &#34;スミス&#34;,
    &#34;customer_postal_code&#34;  : &#34;92101&#34;,
    &#34;customer_state&#34;        : &#34;CA&#34;,
    &#34;language_code&#34;         : &#34;en&#34;,
    &#34;page_name&#34;             : &#34;ホームページ&#34;,
    &#34;page_type&#34;             : &#34;account&#34;,
    &#34;tealium_event&#34;         : &#34;page_view&#34;
}
```

## 追跡イベント

### カートに追加

|イベント名|説明|
|---| ---|
| `cart_add`| カートに追加するアクションです。|

サンプル:  
```javascript
{
    &#34;cart_product_id&#34;          : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;cart_product_price&#34;       : [&#34;12.00&#34;, &#34;25.99&#34;],
    &#34;cart_product_quantity&#34;    : [&#34;2&#34;, &#34;2&#34;],
    &#34;cart_product_sku&#34;         : [&#34;PR-RED-123&#34;, &#34;PR-BLK-456&#34;],
    &#34;product_category&#34;         : [&#34;シャツ&#34;],
    &#34;product_id&#34;               : [&#34;PROD678&#34;],
    &#34;product_image_url&#34;        : [&#34;//domain.com/path/image.gif&#34;],
    &#34;product_name&#34;             : [&#34;商品三&#34;],
    &#34;product_price&#34;            : [&#34;18.00&#34;],
    &#34;product_quantity&#34;         : [&#34;2&#34;],
    &#34;product_sku&#34;              : [&#34;PR-BLU-678&#34;],
    &#34;product_subcategory&#34;      : [&#34;Tシャツ&#34;],
    &#34;tealium_event&#34;            : &#34;cart_add&#34;
}
```
### カートから削除

|イベント名|説明|
|---| ---|
| `cart_remove`| カートからの削除アクション。|

サンプル:  
```javascript
{
    &#34;cart_product_id&#34;          : [&#34;PROD123&#34;, &#34;PROD456&#34;],
    &#34;cart_product_price&#34;       : [&#34;12.00&#34;, &#34;25.99&#34;],
    &#34;cart_product_quantity&#34;    : [&#34;2&#34;, &#34;2&#34;],
    &#34;cart_product_sku&#34;         : [&#34;PR-RED-123&#34;, &#34;PR-BLK-456&#34;],
    &#34;product_category&#34;         : [&#34;Shirts&#34;],
    &#34;product_id&#34;               : [&#34;PROD456&#34;],
    &#34;product_image_url&#34;        : [&#34;//domain.com/path/image.gif&#34;],
    &#34;product_name&#34;             : [&#34;Product Two&#34;],
    &#34;product_price&#34;            : [&#34;12.00&#34;],
    &#34;product_quantity&#34;         : [&#34;2&#34;],
    &#34;product_sku&#34;              : [&#34;PR-BLK-456&#34;],
    &#34;product_subcategory&#34;      : [&#34;T-Shirts&#34;],
    &#34;tealium_event&#34;            : &#34;cart_remove&#34;
}
```

### ユーザー登録

|イベント名|説明|
|---| ---|
| `user_register`| ユーザー登録が成功した際。|

サンプル:  
```javascript
{
    &#34;customer_city&#34;         : &#34;San Diego&#34;,
    &#34;customer_country&#34;      : &#34;United States&#34;,
    &#34;customer_email&#34;        : &#34;john.smith@example.com&#34;,
    &#34;customer_first_name&#34;   : &#34;John&#34;,
    &#34;customer_id&#34;           : &#34;8237572&#34;,
    &#34;customer_last_name&#34;    : &#34;Smith&#34;,
    &#34;customer_postal_code&#34;  : &#34;92101&#34;,
    &#34;customer_state&#34;        : &#34;CA&#34;,
    &#34;tealium_event&#34;         : &#34;user_register&#34;
}
```

### ユーザー情報更新

|イベント名|説明|
|---|---|
| `user_update`| ユーザープロファイル情報の更新が成功した際。|

サンプル:  
```javascript
{
    &#34;customer_city&#34;         : &#34;San Diego&#34;,
    &#34;customer_country&#34;      : &#34;United States&#34;,
    &#34;customer_email&#34;        : &#34;john.smith@example.com&#34;,
    &#34;customer_first_name&#34;   : &#34;John&#34;,
    &#34;customer_id&#34;           : &#34;8237572&#34;,
    &#34;customer_last_name&#34;    : &#34;Smith&#34;,
    &#34;customer_postal_code&#34;  : &#34;92101&#34;,
    &#34;customer_state&#34;        : &#34;CA&#34;,
    &#34;tealium_event&#34;         : &#34;user_update&#34;
}
```

### メールサインアップ

|イベント名|説明|
|---|---|
| `email_signup`| メールニュースレターへのサインアップが成功した際。|

サンプル:  
```javascript
{
    &#34;customer_email&#34;  : &#34;john.smith@example.com&#34;,
    &#34;tealium_event&#34;   : &#34;email_signup&#34;
}
```
### カスタムクリック

|イベント名|説明|
|---|---|
| `custom_click`| ページ内の特定のクリックインタラクションを追跡。|

サンプル:  
```javascript
{
    &#34;link_category&#34;  : &#34;Header&#34;,
    &#34;link_name&#34;      : &#34;Login&#34;,
    &#34;tealium_event&#34;  : &#34;custom_click&#34;
}
```