---
title: 小売データレイヤー仕様
description: この記事では小売のためのデータレイヤー定義を提供します。
url: https://docs.tealium.com/ja/platforms/getting-started-web/data-layer/definitions/retail/
---## データレイヤー属性

|変数| 説明| 例| タイプ|
|---| ---| ---| ---|
|`brand_name`| ブランド固有のページのブランド名| `Ralph Lauren`| 文字列|
|`browse_refine_type`| 絞り込みタイプの配列| `["Size", "Color"]`| 配列|
|`browse_refine_value`| 絞り込み値の配列| `["XL", "Red"]`| 配列|
|`cart_product_id`| `cart_add` イベント時、カート内の全商品IDの配列| `["PROD123", "PROD456"]` | 配列|
|`cart_product_price`| `cart_add` イベント時、カート内の全商品価格の配列| `["12.99", "25.99"]`| 配列|
|`cart_product_quantity`| `cart_add` イベント時、カート内の全商品数量の配列| `["2", "2"]`| 配列|
|`cart_product_sku`| `cart_add` イベント時、カート内の全商品SKUの配列| `["PR-RED-1234", "PR-BLK-6789"]` | 配列|
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
|`product_brand`| 商品ブランドの配列| `["Ralph Lauren", "Lucky"]`| 配列|
|`product_category`| 商品カテゴリの配列| `["Shirts", "Pants"]`| 配列|
|`product_discount_amount`| 商品レベルのクーポンによる割引額の配列（数字と小数点のみの文字列）| `["2.98", "0.00"]`| 配列|
|`product_id`| 商品IDの配列| `["PROD123", "PROD456"]`| 配列|
|`product_image_url`| 主要商品画像のURLの配列| `["//domain.com/123.gif", "//domain.com/456.gif"]` | 配列|
|`product_name`| 商品名の配列| `["Product One", "Expensive Product Two"]` | 配列|
|`product_on_page`| ページ上に表示される他の商品の商品IDの配列| `["PROD123", "PROD456"]`| 配列|
|`product_original_price`| 元の提案小売商品価格の配列、カンマと記号を省略| `["29.99", "1015.00"]`| 配列|
|`product_price`| 商品販売価格の配列、カンマと記号を省略| `["12.99", "1010.98"]`| 配列|
|`product_promo_code`| 特定の商品に適用されたプロモーション/クーポンコードの配列| `["SHIRT10OFF","PROMO10"]`| 配列|
|`product_quantity`| 各商品の数量の配列| `["2","2"]`| 配列|
|`product_sku`| 商品SKUの配列| `["PR-RED-1234", "PR-BLK-6789"]` | 配列|
|`product_subcategory`| 商品サブカテゴリの配列| `["T-Shirts", "Dress Pants"]`| 配列|
|`product_url`| 個々の商品ページへのURLの配列| `["//domain.com/123.html", "//domain.com/456/html"]` | 配列|
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
    "cart_total_items" : "4",
    "cart_total_value" : "77.96",
    "country_code"     : "us",
    "language_code"    : "en",
    "page_name"        : "Homepage",
    "page_type"        : "home",
    "site_section"     : "Clothing",
    "tealium_event"    : "page_view"
}
```

### セクションページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `page_view`| 親カテゴリまたはトップレベルセクションページ。| `http://www.example.com/top-level/`|

サンプル:  
```javascript
{
    "brand_name"        : "Ralph Lauren",
    "cart_total_items"  : "4",
    "cart_total_value"  : "77.96",
    "category_id"       : "243",
    "category_name"     : "Shoes: Boots",
    "country_code"      : "us",
    "language_code"     : "en",
    "page_name"         : "Homepage",
    "page_type"         : "section",
    "product_on_page"   : ["PROD123", "PROD456"],
    "site_section"      : "Clothing",
    "tealium_event"     : "page_view"
}
```

### カテゴリーページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `category_view`| 通常、商品リストを表示するカテゴリーページ。| `http://www.example.com/top-level/sub-level/`|

サンプル:  
```javascript
{
    "brand_name"           : "Ralph Lauren",
    "browse_refine_type"   : ["Size", "Color"],
    "browse_refine_value"  : ["XL", "Red"],
    "cart_total_items"     : "4",
    "cart_total_value"     : "77.96",
    "category_id"          : "243",
    "category_name"        : "Shoes: Boots",
    "country_code"         : "us",
    "language_code"        : "en",
    "page_name"            : "Homepage",
    "page_type"            : "category",
    "product_on_page"      : ["PROD123", "PROD456"],
    "site_section"         : "Clothing",
    "tealium_event"        : "category_view"
}
```
### 商品ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `product_view`| 商品詳細ページです。| `http://www.example.com/top-level/sub-level/product.html`|

サンプル:  
```javascript
{
    "cart_total_items"        : "4",
    "cart_total_value"        : "77.96",
    "category_id"             : "243",
    "category_name"           : "靴: ブーツ",
    "country_code"            : "us",
    "language_code"           : "en",
    "page_name"               : "ホームページ",
    "page_type"               : "product",
    "product_brand"           : ["Ralph Lauren", "Lucky"],
    "product_category"        : ["シャツ", "パンツ"],
    "product_id"              : ["PROD123", "PROD456"],
    "product_image_url"       : ["//domain.com/path/image.gif"],
    "product_name"            : ["商品一", "高級商品二"],
    "product_on_page"         : ["PROD123", "PROD456"],
    "product_original_price"  : ["29.99", "1015.00"],
    "product_price"           : ["12.99", "1010.98"],
    "product_sku"             : ["PR-RED-1234", "PR-BLK-6789"],
    "product_subcategory"     : ["Tシャツ", "ドレスパンツ"],
    "product_url"             : ["//domain.com/cat/prod/prod123.html"],
    "site_section"            : "衣類",
    "tealium_event"           : "product_view"
}
```

### 検索ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `search`| 検索結果ページです。| `http://www.example.com/search?query=term`|

サンプル:  
```javascript
{
    "browse_refine_type"   : ["サイズ", "色"],
    "browse_refine_value"  : ["XL", "赤"],
    "cart_total_items"     : "4",
    "cart_total_value"     : "77.96",
    "country_code"         : "us",
    "language_code"        : "en",
    "page_name"            : "ホームページ",
    "page_type"            : "search",
    "product_on_page"      : ["PROD123", "PROD456"],
    "search_keyword"       : "カーゴ",
    "search_results"       : "42",
    "site_section"         : "衣類",
    "tealium_event"        : "search"
}
```

### カートページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `cart_view`| ショッピングカートページで、カートの商品内容が表示されます。| `http://www.example.com/cart`|

サンプル:  
```javascript
{
    "cart_total_items"         : "2",
    "cart_total_value"         : "2524.00",
    "country_code"             : "us",
    "language_code"            : "en",
    "page_name"                : "ショッピングバッグ",
    "page_type"                : "cart",
    "product_brand"            : ["Ralph Lauren", "Lucky"],
    "product_category"         : ["シャツ", "パンツ"],
    "product_discount_amount"  : ["2.98", "0.00"],
    "product_id"               : ["PROD123", "PROD456"],
    "product_image_url"        : ["//domain.com/path/image123.gif",
                                  "//domain.com/path/image456.gif"],
    "product_name"             : ["商品一", "高級商品二"],
    "product_price"            : ["12.00", "1250.00"],
    "product_promo_code"       : ["SHIRT10OFF",""],
    "product_quantity"         : ["2","2"],
    "product_sku"              : ["PR-RED-1234", "PR-BLK-6789"],
    "product_subcategory"      : ["Tシャツ", "ドレスパンツ"],
    "product_url"              : ["//domain.com/cat/prod/prod123.html",
                                  "//domain.com/cat/prod/prod456.html"],
    "tealium_event"            : "cart_view"
}
```

### チェックアウトページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `checkout`| 通常は配送、支払い、請求情報ページのチェックアウトページです。| `http://www.example.com/checkout/billing/shipping`|

サンプル:  
```javascript
{
    "cart_total_items"  : "2",
    "cart_total_value"  : "2524.00",
    "country_code"      : "us",
    "language_code"     : "en",
    "page_name"         : "チェックアウト：支払い",
    "page_type"         : "checkout",
    "tealium_event"     : "checkout"
}
```

### 注文ページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `purchase`| 注文確認（「ありがとうございます」）ページです。| `http://www.example.com/checkout/success/order.html`|

サンプル:  
```javascript
{
    "cart_total_items"         : "2",
    "cart_total_value"         : "2524.00",
    "country_code"             : "us",
    "customer_city"            : "サンディエゴ",
    "customer_country"         : "アメリカ合衆国",
    "customer_email"           : "john.smith@example.com",
    "customer_first_name"      : "ジョン",
    "customer_id"              : "8237572",
    "customer_last_name"       : "スミス",
    "customer_postal_code"     : "92101",
    "customer_state"           : "CA",
    "language_code"            : "en",
    "order_currency_code"      : "USD",
    "order_discount_amount"    : "10.00",
    "order_id"                 : "ORD123456",
    "order_payment_type"       : "paypal",
    "order_promo_code"         : "SPRFREE,PROMO10",
    "order_shipping_amount"    : "6.99",
    "order_shipping_type"      : "UPS",
    "order_store"              : "モバイルウェブ",
    "order_subtotal"           : "2524.00",
    "order_tax_amount"         : "25.00",
    "order_total"              : "2549.00",
    "page_name"                : "注文確認 - ありがとう",
    "page_type"                : "order",
    "product_brand"            : ["Ralph Lauren", "Lucky"],
    "product_category"         : ["シャツ", "パンツ"],
    "product_discount_amount"  : ["5.00", "0.00"],
    "product_id"               : ["PROD123", "PROD456"],
    "product_image_url"        : ["//domain.com/path/image123.gif",
                                  "//domain.com/path/image456.gif"],
    "product_name"             : ["商品一", "高級商品二"],
    "product_price"            : ["12.00", "1250.00"],
    "product_promo_code"       : ["SHIRT10OFF",""],
    "product_quantity"         : ["2","2"],
    "product_sku"              : ["PR-RED-1234", "PR-BLK-6789"],
    "product_subcategory"      : ["Tシャツ", "ドレスパンツ"],
    "product_url"              : ["//domain.com/cat/prod/prod123.html",
                                  "//domain.com/cat/prod/prod456.html"],
    "tealium_event"            : "purchase"
}
```

### アカウントページ

|イベント名|説明| サンプルURL|
|---| ---| ---|
| `page_view`| ユーザーアカウントプロファイルページです。| `http://www.example.com/account/profile`|

サンプル:  
```javascript
{
    "cart_total_items"      : "4",
    "cart_total_value"      : "77.96",
    "country_code"          : "us",
    "customer_city"         : "サンディエゴ",
    "customer_country"      : "アメリカ合衆国",
    "customer_email"        : "johnsmith@example.com",
    "customer_first_name"   : "ジョン",
    "customer_id"           : "8237572",
    "customer_last_name"    : "スミス",
    "customer_postal_code"  : "92101",
    "customer_state"        : "CA",
    "language_code"         : "en",
    "page_name"             : "ホームページ",
    "page_type"             : "account",
    "tealium_event"         : "page_view"
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
    "cart_product_id"          : ["PROD123", "PROD456"],
    "cart_product_price"       : ["12.00", "25.99"],
    "cart_product_quantity"    : ["2", "2"],
    "cart_product_sku"         : ["PR-RED-123", "PR-BLK-456"],
    "product_category"         : ["シャツ"],
    "product_id"               : ["PROD678"],
    "product_image_url"        : ["//domain.com/path/image.gif"],
    "product_name"             : ["商品三"],
    "product_price"            : ["18.00"],
    "product_quantity"         : ["2"],
    "product_sku"              : ["PR-BLU-678"],
    "product_subcategory"      : ["Tシャツ"],
    "tealium_event"            : "cart_add"
}
```
### カートから削除

|イベント名|説明|
|---| ---|
| `cart_remove`| カートからの削除アクション。|

サンプル:  
```javascript
{
    "cart_product_id"          : ["PROD123", "PROD456"],
    "cart_product_price"       : ["12.00", "25.99"],
    "cart_product_quantity"    : ["2", "2"],
    "cart_product_sku"         : ["PR-RED-123", "PR-BLK-456"],
    "product_category"         : ["Shirts"],
    "product_id"               : ["PROD456"],
    "product_image_url"        : ["//domain.com/path/image.gif"],
    "product_name"             : ["Product Two"],
    "product_price"            : ["12.00"],
    "product_quantity"         : ["2"],
    "product_sku"              : ["PR-BLK-456"],
    "product_subcategory"      : ["T-Shirts"],
    "tealium_event"            : "cart_remove"
}
```

### ユーザー登録

|イベント名|説明|
|---| ---|
| `user_register`| ユーザー登録が成功した際。|

サンプル:  
```javascript
{
    "customer_city"         : "San Diego",
    "customer_country"      : "United States",
    "customer_email"        : "john.smith@example.com",
    "customer_first_name"   : "John",
    "customer_id"           : "8237572",
    "customer_last_name"    : "Smith",
    "customer_postal_code"  : "92101",
    "customer_state"        : "CA",
    "tealium_event"         : "user_register"
}
```

### ユーザー情報更新

|イベント名|説明|
|---|---|
| `user_update`| ユーザープロファイル情報の更新が成功した際。|

サンプル:  
```javascript
{
    "customer_city"         : "San Diego",
    "customer_country"      : "United States",
    "customer_email"        : "john.smith@example.com",
    "customer_first_name"   : "John",
    "customer_id"           : "8237572",
    "customer_last_name"    : "Smith",
    "customer_postal_code"  : "92101",
    "customer_state"        : "CA",
    "tealium_event"         : "user_update"
}
```

### メールサインアップ

|イベント名|説明|
|---|---|
| `email_signup`| メールニュースレターへのサインアップが成功した際。|

サンプル:  
```javascript
{
    "customer_email"  : "john.smith@example.com",
    "tealium_event"   : "email_signup"
}
```
### カスタムクリック

|イベント名|説明|
|---|---|
| `custom_click`| ページ内の特定のクリックインタラクションを追跡。|

サンプル:  
```javascript
{
    "link_category"  : "Header",
    "link_name"      : "Login",
    "tealium_event"  : "custom_click"
}
```