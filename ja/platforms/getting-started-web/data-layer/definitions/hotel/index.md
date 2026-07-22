---
title: ホテルデータレイヤー仕様
description: この記事では、ホテルのデータレイヤー定義について説明します。
url: https://docs.tealium.com/ja/platforms/getting-started-web/data-layer/definitions/hotel/
---## データレイヤー属性

|変数| 説明| 例| タイプ|
|---| ---| ---| ---|
|`avg_room_rate`| 各部屋の平均料金の配列| `["100.25"]`| 配列|
|`cancellation_id`| 予約がキャンセルされた際のID| `12254875`| 文字列|
|`check_in`| 利用者の到着日| `02/18/2017`| 文字列|
|`check_out`| 利用者の出発日| `02/24/2017`| 文字列|
|`check_reservation`| ゲストが予約を確認する方法（確認または情報）| `information`| 文字列|
|`currency`| 料金の通貨| `USD`| 文字列|
|`customer_city`| 予約者の居住都市| `San Diego`| 文字列|
|`customer_country`| 予約者の居住国| `USA`| 文字列|
|`customer_email`| 予約者のメールアドレス| `example@example.com`| 文字列|
|`customer_first_name`| 予約者の名前| `Tealium`| 文字列|
|`customer_id_type`| ロイヤルティサイトへのログインに使用されるIDのタイプ（メールまたはロイヤルティID）| `loyalty id`| 文字列|
|`customer_last_name`| 予約者の姓| `Tealium`| 文字列|
|`customer_postal_code`| 予約者の郵便番号| `92121`| 文字列|
|`customer_state`| 予約者の州| `CA`| 文字列|
|`days_till_checkin`| 今日からチェックインまでの日数| `45`| 文字列|
|`displayed_properties`| ホテル選択ページに表示される全ての物件のIDの配列| `["345","4567"]`| 配列|
|`displayed_rate_amount`| 部屋選択ページに表示される料金| `150.00`| 文字列|
|`displayed_rate_amounts`| ホテル選択ページに表示される各物件の料金の配列| `["100.25","150.00","340.00"]`| 配列|
|`displayed_rate_codes`| ホテル選択ページに表示される各物件の料金コードの配列| `["economy","economy","luxury"]`| 配列|
|`displayed_room_rates`| 部屋選択ページに表示される部屋タイプごとの料金の配列| `["340.00","500.00","650.00"]`| 配列|
|`displayed_room_types`| 部屋選択ページに表示される部屋タイプの配列| `["2 Queen Beds","Ocean View","Ocean Front"]`| 配列|
|`error_message`| ユーザーに表示されるエラーメッセージ| `Room no longer available`| 文字列|
|`favorite_property_id`| 「お気に入り」として登録された物件ID| `123`| 文字列|
|`filter_amenities`| 適用された選択肢の配列| `["pool","microwave"]`| 配列|
|`filter_distance`| イベントからのフィルター距離| `20`| 文字列|
|`filter_hotel_type`| ユーザーによってフィルターされたホテルタイプの配列| `["economy","luxury"]`| 配列|
|`filter_max_rate`| 適用された料金| `150`| 文字列|
|`filter_rate_change`| フィルター変更| `AAA to 20% Off`| 文字列|
|`filter_ta_rating`| ユーザーによってフィルターされたトラベルアドバイザーの評価の配列| `["3","4","5"]`| 配列|
|`language_code`| 言語コード| `us`| 文字列|
|`link_category`| クリック追跡イベント中、クリックされた要素のカテゴリ| `Navigation`| 文字列|
|`link_name`| クリック追跡イベント中、クリックされた要素の名前| `properties`| 文字列|
|`login_status`| ユーザーのログイン状態| `logged in`| 文字列|
|`loyalty_id`| ロイヤルティ会員番号| `99568784521`| 文字列|
|`loyalty_point_balance`| ユーザーのロイヤルティアカウントの現在のポイント残高| `1000`| 文字列|
|`loyalty_tier`| 会員ステータスレベル| `Silver`| 文字列|
|`modify_stay`| 宿泊が変更されるたびに構成されるイベント追跡| `true`| 文字列|
|`num_of_adults`| 大人の総数| `2`| 文字列|
|`num_of_children`| 子供の総数| `3`| 文字列|
|`num_of_nights`| 宿泊数| `5`| 文字列|
|`num_of_rooms`| 部屋数| `1`| 文字列|
|`occupancy_detail`| 検索された各部屋の総宿泊人数の配列| `["4","2"]`| 配列|
|`order_cancellation_policy`| 注文ごとの各部屋のキャンセルポリシーの配列| `["24hours","5days"]`| 配列|
|`order_corp_id`| 注文に添付された企業ID（ある場合）| `987646`| 文字列|
|`order_discount_amount`| 注文レベルの割引額| `100.00`| 文字列|
|`order_iata`| 注文に添付された国際航空運送協会番号（旅行代理店番号）| `646879`| 文字列|
|`order_id`| 注文の一意のID、注文確認ページでのみ入力| `1234`| 文字列|
|`order_payment_method`| 支払い方法| `visa`| 文字列|
|`order_payment_type`| 標準収入またはポイント| `revenue`| 文字列|
|`order_points_used`| 注文の各部屋の総ポイント数の配列| `["1000","5000"]`| 配列|
|`order_postal_code`| 予約された物件の郵便番号| `00267`| 文字列|
|`order_promo_code`| 注文に添付されたプロモーションコード（ある場合）| `SALE`| 文字列|
|`order_rate_code`| 注文の各部屋に予約された料金コードの配列| `["AAA",""]`| 配列|
|`order_room_occupancy`| 注文の各部屋の総宿泊人数の配列| `["5","2"]`| 配列|
|`order_room_type`| 注文の各部屋に予約された部屋タイプの配列| `["double","ocean view"]`| 配列|
|`order_special_requests`| レビュー＆予約ページの「特別リクエスト」欄に入力されたフリーテキスト（部屋ごと）| `No Feathers`| 文字列|
|`order_subtotal`| 商品または注文レベルの割引を含む総小計（税金や手数料を除く）| `1000.00`| 文字列|
|`order_tax_amount`| 総税金と手数料| `75.00`| 文字列|
|`order_total`| 注文の総額| `1175.00`| 文字列|
|`order_total_occupancy`| 予約時の注文の総宿泊人数| `5`| 文字列|
|`page_joined`| ゲストがロイヤルティに参加するページ - ページ名| `homepage`| 文字列|
|`page_name`| ページ名を識別するTealium変数| `homepage`| 文字列|
|`page_type`| ホーム、物件、確認などの高レベルページタイプ| `home`| 文字列|
|`promo_registration_page`| プロモーション登録が行われたページ| `offers`| 文字列|
|`property_brand`| 物件のブランド名| `["economy brand"]`| 配列|
|`property_city`| 物件が位置する都市| `["Chula Vista"]`| 配列|
|`property_country`| 物件が位置する国| `["USA"]`| 配列|
|`property_id`| 物件番号の配列| `["354498765467"]`| 配列|
|`property_name`| 物件名の配列| `["hotel Chula Vista"]`| 配列|
|`property_position`| 選択された物件のインデックスの配列| `["1"]`| 配列|
|`property_postal_code`| 物件の郵便番号の配列| `["92121"]`| 配列|
|`property_state`| 物件が位置する州の配列| `["CA"]`| 配列|
|`proximity`| 市中心部と物件位置の距離（マイル）の配列| `["24"]`| 配列|
|`registration_id`| 特別オファーやプロモの登録にユーザーが入力したID; メールまたはロイヤルティID| `example@example.com`| 文字列|
|`search_city`| 検索された目的地の都市| `Chula Vista`| 文字列|
|`search_country`| 検索された目的地の国| `USA`| 文字列|
|`search_full`| Googleによって提供される目的地の完全な説明| `Chula Vista, California, United States`| 文字列|
|`search_rate`| 予約ウィジェットの料金選択ドロップダウンメニューから選択された料金| `Corporate`| 文字列|
|`search_rate_value`| 予約ウィジェットの料金選択ドロップダウンメニューから選択されたプロモーションと企業の選択の値| `Tealium`| 文字列|
|`search_results`| 検索によって返された結果の数| `22`| 文字列|
|`search_state`| 検索された目的地の州| `WA`| 文字列|
|`search_type`| 目的地のタイプ（空港、地域、国立公園など、Googleによって定義）| `airport`| 文字列|
|`select_room_position`| 部屋選択ページでホテル選択ページから表示された料金の最高位置| `1`| 文字列|
|`selected_rate_price`| 部屋選択ページでユーザーによって選択された部屋の料金の配列| `["100.00","150.00"]`| 配列|
|`selected_rate_type`| 部屋選択ページでユーザーによって選択された部屋の料金タイプの配列| `["Best Rate","loyalty","AAA"]`| 配列|
|`selected_room_type`| 部屋選択ページでユーザーによって選択された部屋タイプの配列| `["2 double beds","Ocean View"]`| 配列|
|`show_available`| 利用可能なホテルのみを表示する構成| `true`| 文字列|
|`site`| ユーザーが使用しているサイト| `economy site`| 文字列|
|`site_section`| サイトの高レベルセクション| `offers`| 文字列|
|`social_channel`| ソーシャルメディアで情報が共有されたときに使用されるイベント | `facebook`| 文字列|
|`sort_by`| 並び替え選択（距離、低から高、高から低）| `distance`| 文字列|
|`sort_order`| 部屋のタイプ、料金コード、料金額、通貨が選択された部屋のページに表示される配列 | `["room type","distance"]`| 配列|
|`video_action`| 現在ビデオで行われているアクション、再生、再生中、一時停止、停止、完了 | `play`| 文字列|
|`video_content_type`| 視聴されたビデオのタイプ | `Property Video`| 文字列|
|`video_name`| 視聴されたビデオの名前 | `Video Name`| 文字列|
|`video_segments`| ビデオの視聴率 | `75`| 文字列|

## ページ追跡

### ホームページ

|イベント名|説明|
|---|---|
| `page_view`| ホームページ。|

サンプル:  
```javascript
{
   "currency"         : "USD",     
   "customer_email"   : "example@example.com",     
   "customer_id_type" : "loyalty id",     
   "language_code"    : "us",     
   "loyalty_id"       : "99568784521",     
   "page_name"        : "homepage",     
   "page_type"        : "home",     
   "site"             : "economy site",     
   "site_section"     : "offers",     
   "tealium_event"    : "page_view"
}
```

### ホテル選択ページ

|イベント名|説明|
|---|---|
| `page_view`| ホテル選択/検索結果ページ。|

サンプル:  
```javascript
{
   "check_in"               : "02/18/2017",     
   "check_out"              : "02/24/2017",     
   "currency"               : "USD",     
   "customer_email"         : "example@example.com",     
   "customer_id_type"       : "loyalty id",     
   "days_till_checkin"      : "45",     
   "displayed_properties"   : ["345","4567"],     
   "displayed_rate_amounts" : ["100.25","150.00","340.00"],     
   "displayed_rate_codes"   : ["economy","economy","luxury"],     
   "filter_amenities"       : ["pool","microwave"],     
   "filter_distance"        : "20",     
   "filter_hotel_type"      : ["economy","luxury"],     
   "filter_max_rate"        : "150",     
   "filter_rate_change"     : "AAA to 20% Off",     
   "filter_ta_rating"       : ["3","4","5"],     
   "language_code"          : "us",     
   "loyalty_id"             : "99568784521",     
   "modify_stay"            : "true",     
   "num_of_adults"          : "2",     
   "num_of_children"        : "3",     
   "num_of_nights"          : "5",     
   "num_of_rooms"           : "1",     
   "page_name"              : "Select Hotel",     
   "page_type"              : "select_hotel",     
   "proximity"              : ["24"],     
   "search_city"            : "Chula Vista",     
   "search_country"         : "USA",     
   "search_full"            : "Chula Vista, California, United States",     
   "search_rate"            : "Corporate",     
   "search_rate_value"      : "Tealium",     
   "search_results"         : "22",     
   "search_state"           : "WA",     
   "search_type"            : "airport",     
   "show_available"         : "true",     
   "site"                   : "economy site",     
   "site_section"           : "offers",     
   "sort_by"                : "distance",     
   "sort_order"             : ["roomtype","distance"],     
   "tealium_event"          : "page_view"
}
```

### 部屋選択ページ

|イベント名|説明|
|---|---|
| `page_view`| 部屋選択/物件詳細ページ。|

サンプル:  
```javascript
{
   "check_in"              : "02/18/2017",     
   "check_out"             : "02/24/2017",     
   "currency"              : "USD",     
   "customer_email"        : "example@example.com",     
   "customer_id_type"      : "loyalty id",     
   "days_till_checkin"     : "45",     
   "displayed_rate_amount" : "150.00",     
   "displayed_room_rates"  : ["340.00","500.00","650.00"],     
   "displayed_room_types"  : ["2 Queen Beds","Ocean View","Ocean Front"],     
   "language_code"         : "us",     
   "loyalty_id"            : "99568784521",     
   "modify_stay"           : "true",     
   "num_of_adults"         : "2",     
   "num_of_children"        : "3",     
   "num_of_nights"         : "5",     
   "num_of_rooms"          : "1",     
   "page_name"             : "Select a Room",     
   "page_type"             : "select_room",     
   "property_brand"        : ["economy brand"],     
   "property_city"         : ["Chula Vista"],     
   "property_country"      : ["USA"],     
   "property_id"           : ["354498765467"],     
   "property_name"         : ["hotel Chula Vista"],     
   "property_position"     : ["1"],     
   "property_postal_code"  : ["92121"],     
   "property_state"        : ["CA"],     
   "proximity"             : ["24"],     
   "select_room_position"  : "1",     
   "site"                  : "economy site",     
   "site_section"          : "offers",     
   "social_channel"        : "facebook",     
   "tealium_event"         : "page_view"
 }
 ```

### 予約確認ページ

|イベント名|説明|
|---|---|
| `page_view`| 予約確認ページ。|

サンプル:  
```javascript
{    
   "check_in"               : "02/18/2017",     
   "check_out"              : "02/24/2017",    
    "currency"              : "USD",     
    "customer_email"        : "example@example.com",     
    "customer_id_type"      : "loyalty id",     
    "days_till_checkin"     : "45",     
    "language_code"         : "us",     
    "loyalty_id"            : "99568784521",     
    "num_of_adults"         : "2",     
    "num_of_children"       : "3",     
    "num_of_nights"         : "5",     
    "num_of_rooms"          : "1",     
    "occupancy_detail"      : ["4","2"],     
    "order_total_occupancy" : "5",     
    "page_name"             : "Review Room",     
    "page_type"             : "review_reserve",     
    "property_brand"        : ["economy brand"],     
    "property_city"         : ["Chula Vista"],     
    "property_country"      : ["USA"],     
    "property_id"           : ["354498765467"],     
    "property_name"         : ["hotel Chula Vista"],     
    "property_postal_code"  : ["92121"],     
    "property_state"        : ["CA"],     
    "proximity"             : ["24"],     
    "selected_rate_price"   : ["100.00","150.00"],     
    "selected_rate_type"    : ["Best Rate","loyalty","AAA"],     
    "selected_room_type"    : ["2 double beds","Ocean View"],     
    "site"                  : "economy site",     
    "site_section"          : "offers",     
    "tealium_event"         : "page_view"
 }
 ```
### 確認ページ

|イベント名|説明|
|---|---|
| `purchase`| 確認ページ。|

サンプル:  
```javascript
{  
   "avg_room_rate"             : ["100.25"],     
   "check_in"                  : "02/18/2017",     
   "check_out"                 : "02/24/2017",     
   "check_reservation"         : "information",     
   "currency"                  : "USD",     
   "customer_city"             : "San Diego",     
   "customer_country"          : "USA",     
   "customer_email"            : "example@example.com",     
   "customer_first_name"       : "Tealium",     
   "customer_id_type"          : "loyalty id",     
   "customer_last_name"        : "Tealium",     
   "customer_postal_code"      : "92121",     
   "customer_state"            : "CA",     
   "days_till_checkin"         : "45",     
   "language_code"             : "us",     
   "loyalty_id"                : "99568784521",     
   "loyalty_point_balance"     : "1000",     
   "loyalty_tier"              : "Silver",     
   "num_of_adults"             : "2",     
   "num_of_children"           : "3",     
   "num_of_nights"             : "5",     
   "num_of_rooms"              : "1",     
   "occupancy_detail"          : ["4","2"],     
   "order_cancellation_policy" : ["24hours","5days"],     
   "order_corp_id"             : "987646",     
   "order_discount_amount"     : "100.00",     
   "order_iata"                : "646879",     
   "order_id"                  : "1234",     
   "order_payment_method"      : "visa",     
   "order_payment_type"        : "revenue",    
   "order_points_used"         : ["1000","5000"],     
   "order_postal_code"         : "00267",     
   "order_promo_code"          : "SALE",     
   "order_rate_code"           : ["AAA",""],     
   "order_room_occupancy"      : ["5","2"],     
   "order_room_type"           : ["double","ocean view"],     
   "order_special_requests"    : "No Feathers",     
   "order_subtotal"            : "1000.00",     
   "order_tax_amount"          : "75.00",     
   "order_total"               : "1175.00",     
   "order_total_occupancy"     : "5",     
   "page_name"                 : "Confirmation",     
   "page_type"                 : "confirmation",     
   "property_brand"            : ["economy brand"],     
   "property_city"             : ["Chula Vista"],     
   "property_country"          : ["USA"],     
   "property_id"               : ["354498765467"],     
   "property_name"             : ["hotel Chula Vista"],     
   "property_postal_code"      : ["92121"],     
   "property_state"            : ["CA"],     
   "proximity"                 : ["24"],     
   "site"                      : "economy site",     
   "site_section"              : "offers",     
   "social_channel"            : "facebook",     
   "tealium_event"             : "purchase"
}
```

### ロイヤリティページ

|イベント名|説明|
|---|---|
|`page_view`| ロイヤリティプログラムのホームページ。|

サンプル:  
```javascript
{
    "currency"              : "USD",
    "customer_email"        : "example@example.com",
    "customer_id_type"      : "loyalty id",
    "language_code"         : "us",
    "loyalty_id"            : "99568784521",
    "loyalty_point_balance" : "1000",
    "loyalty_tier"          : "Silver",
    "page_name"             : "Loyalty Page",
    "page_type"             : "loyalty",
    "site"                  : "economy site",
    "site_section"          : "offers",
    "tealium_event"         : "page_view"
}
```

### オファーページ

|イベント名|説明|
|---|---|
| `page_view`| オファーとプロモーションのページ。|

サンプル:  
```javascript
{
    "currency"         : "USD",
    "customer_email"   : "example@example.com",
    "customer_id_type" : "loyalty id",
    "language_code"    : "us",
    "loyalty_id"       : "99568784521",
    "page_name"        : "Offers",
    "page_type"        : "offers",
    "site"             : "economy site",
    "site_section"     : "offers",
    "tealium_event"    : "page_view"
}
 ```

### ホテルの目的地ページ

|イベント名|説明|
|---|---|
| `page_view`| ホテルの一般情報（予約非対応）。|

サンプル:  
```javascript
{
    "check_in"               : "02/18/2017",
    "check_out"              : "02/24/2017",
    "currency"               : "USD",
    "customer_email"         : "example@example.com",
    "customer_id_type"       : "loyalty id",
    "days_till_checkin"      : "45",
    "displayed_properties"   : ["345","4567"],
    "displayed_rate_amounts" : ["100.25","150.00","340.00"],
    "displayed_rate_codes"   : ["economy","economy","luxury"],
    "filter_amenities"       : ["pool","microwave"],
    "filter_distance"        : "20",
    "filter_hotel_type"      : ["economy","luxury"],
    "filter_max_rate"        : "150",
    "filter_rate_change"     : "AAA to 20% Off",
    "filter_ta_rating"       : ["3","4","5"],
    "language_code"          : "us",
    "loyalty_id"             : "99568784521",
    "modify_stay"            : "true",
    "num_of_adults"          : "2",
    "num_of_children"        : "3",
    "num_of_nights"          : "5",
    "num_of_rooms"           : "1",
    "page_name"              : "Destinations",
    "page_type"              : "hotels_destinations",
    "proximity"              : ["24"],
    "search_city"            : "Chula Vista",
    "search_country"         : "USA",
    "search_full"            : "Chula Vista, California, United States",
    "search_rate"            : "Corporate",
    "search_rate_value"      : "Tealium",
    "search_results"         : "22",
    "search_state"           : "WA",
    "search_type"            : "airport",
    "show_available"         : "true",
    "site"                   : "economy site",
    "site_section"           : "offers",
    "sort_by"                : "distance",
    "sort_order"             : ["roomtype","distance"],
    "tealium_event"          : "page_view"
}
```

### 予約ページ

|イベント名|説明|
|---|---|
| `page_view`| すでに予約された予約を検索する。|

サンプル:  
```javascript
{
    "cancellation_id"   : "12254875",
    "check_reservation" : "information",
    "currency"          : "USD",
    "customer_email"    : "example@example.com",
    "customer_id_type"  : "loyalty id",
    "language_code"     : "us",
    "loyalty_id"        : "99568784521",
    "page_name"         : "Your Reservations",
    "page_type"         : "reservations",
    "site"              : "economy site",
    "site_section"      : "offers",
    "tealium_event"     : "page_view"
}
```

### 一般ページ

|イベント名|説明|
|---|---|
| `page_view`| その他のすべてのページ。|

サンプル:  
```javascript
{
    "currency"         : "USD",
    "customer_email"   : "example@example.com",
    "customer_id_type" : "loyalty id",
    "language_code"    : "us",
    "loyalty_id"       : "99568784521",
    "page_name"        : "Other Page",
    "page_type"        : "content",
    "site"             : "economy site",
    "site_section"     : "offers",
    "tealium_event"    : "page_view"
}
```

## イベントトラッキング

### お気に入り追加

|イベント名|説明|
|---|---|
| `add_favorite`| お気に入りリストにプロパティを追加。|

サンプル:  
```javascript
{
    "favorite_property_id" : "123",
    "tealium_event"        : "add_favorite"
}
```

### ボタン選択

|イベント名|説明|
|---|---|
| `button_selection`| トリップアドバイザーの評価、ブランド。|

サンプル:  
```javascript
{
    "selected_rate_price" : ["100.00","150.00"],
    "selected_rate_type"  : ["Best Rate","loyalty","AAA"],
    "selected_room_type"  : ["2 double beds","Ocean View"],
    "tealium_event"       : "button_selection"
}
```

### キャンセル

|イベント名|説明|
|---|---|
|  `cancellation`| ユーザーが予約をキャンセルしたとき。|

サンプル:  
```javascript
{
    "cancellation_id"           : "12254875",
    "order_cancellation_policy" : ["24hours","5days"],
    "tealium_event"             : "cancellation"
}
```

### 予約確認

|イベント名|説明|
|---|---|
|  `check_reservation`| ユーザーが既存の予約を確認する。|

サンプル:  
```javascript
{
    "check_reservation" : "information",
    "tealium_event"     : "check_reservation"
}
```
### メール登録

|イベント名|説明|
|---|---|
| `email_signup`| メールアップデートまたはニュースレターへの登録が成功した際に発生します。|

サンプル:  
```javascript
{
    "customer_email" : "example@example.com",
    "tealium_event"  : "email_signup"
}
```

### エラーメッセージ

|イベント名|説明|
|---|---|
| `error_message`| ユーザーにエラーメッセージが表示されます。|

サンプル:  
```javascript
{
    "error_message" : "Room no longer available",
    "tealium_event" : "error_message"
}
```

### フォーム送信

|イベント名|説明|
|---|---|
| `form_submit`| ユーザーがフォームを送信します。|

サンプル:  
```javascript
{
    "filter_amenities"   : ["pool","microwave"],
    "filter_distance"    : "20",
    "filter_hotel_type"  : ["economy","luxury"],
    "filter_max_rate"    : "150",
    "filter_rate_change" : "AAA to 20% Off",
    "filter_ta_rating"   : ["3","4","5"],
    "tealium_event"      : "form_submit"
}
```

### カスタムクリック

|イベント名|説明|
|---|---|
| `custom_click`| 特定のページ要素がクリックされた際に発生します。|

サンプル:  
```javascript
{
    "link_category" : "Navigation",
    "link_name"     : "properties",
    "tealium_event" : "custom_click"
}
```

### マップエンゲージメント

|イベント名|説明|
|---|---|
| `map_engagement`| ユーザーがマップと対話します。|

サンプル:  
```javascript
{
    "link_category" : "Navigation",
    "link_name"     : "properties",
    "tealium_event" : "map_engagement"
}
```

### 滞在変更

|イベント名|説明|
|---|---|
| `modify_stay`| ゲストが滞在を変更した際に記録されます。|

サンプル:  
```javascript
{
    "modify_stay"     : "true",
    "num_of_adults"   : "2",
    "num_of_children" : "3",
    "num_of_nights"   : "5",
    "num_of_rooms"    : "1",
    "tealium_event"   : "modify_stay"
}
```

### オファー登録

|イベント名|説明|
|---|---|
| `register_offer`| ユーザーがオファーやプロモーションに登録する際に記録されます。|

サンプル:  
```javascript
{
    "page_joined"             : "homepage",
    "promo_registration_page" : "offers",
    "registration_id"         : "example@example.com",
    "tealium_event"           : "register_offer"
}
```

### ドロップダウン選択

|イベント名|説明|
|---|---|
| `select_dropdown`| ユーザーがホテル検索結果ページのドロップダウンフィルターを変更します。|

サンプル:  
```javascript
{
    "filter_amenities"    : ["pool","microwave"],
    "filter_distance"     : "20",
    "filter_hotel_type"   : ["economy","luxury"],
    "filter_max_rate"     : "150",
    "filter_rate_change"  : "AAA to 20% Off",
    "filter_ta_rating"    : ["3","4","5"],
    "modify_stay"         : "true",
    "num_of_adults"       : "2",
    "num_of_children"     : "3",
    "num_of_nights"       : "5",
    "num_of_rooms"        : "1",
    "page_name"           : "homepage",
    "search_city"         : "Chula Vista",
    "search_country"      : "USA",
    "search_full"         : "Chula Vista, California, United States",
    "search_rate"         : "Corporate",
    "search_rate_value"   : "Tealium",
    "search_results"      : "22",
    "search_state"        : "WA",
    "selected_rate_price" : ["100.00","150.00"],
    "selected_rate_type"  : ["Best Rate","loyalty","AAA"],
    "selected_room_type"  : ["2 double beds","Ocean View"],
    "tealium_event"       : "select_dropdown"
}
```

### 部屋位置選択

|イベント名|説明|
|---|---|
| `select_room_position`| Select Roomページで、Select Hotelページから表示された料金の最高位置を記録します。|

サンプル:  
```javascript
{  
  "select_room_position" : "1",     
  "tealium_event"        : "select_room_position"
}
```

### ソーシャルクリック

|イベント名|説明|
|---|---|
| `social_click`| コンテンツの共有やいいねをクリックします。|

サンプル:  
```javascript
{
    "social_channel" : "facebook",
    "tealium_event"  : "social_click"
}
```

### ソート順序

|イベント名|説明|
|---|---|
| `sort_order`| ユーザーがホテルの結果ページのソート順を変更します。|

サンプル:  
```javascript
{
    "sort_by"      : "distance",
    "sort_order"   : ["roomtype","distance"],
    "tealium_event": "sort_order"
}
```

### ユーザーログイン

|イベント名|説明|
|---|---|
| `user_login`| ユーザーがログインに成功した際に発生します。|

サンプル:  
```javascript
{
    "customer_email" : "example@example.com",
    "login_status"   : "logged in",
    "tealium_event"  : "user_login"
}
```

### ユーザーログアウト

|イベント名|説明|
|---|---|
| `user_logout`| ユーザーがログアウトに成功した際に発生します。|

サンプル:  
```javascript
{
    "customer_email"       : "example@example.com",
    "customer_first_name"  : "Tealium",
    "customer_id_type"     : "loyalty id",
    "customer_last_name"   : "Tealium",
    "customer_postal_code" : "92121",
    "customer_state"       : "CA",
    "login_status"         : "logged in",
    "tealium_event"        : "user_logout"
}
```

### ユーザー登録

|イベント名|説明|
|---|---|
| `user_register`| ユーザー登録が成功した際に発生します。|

サンプル:  
```javascript
{
    "customer_email" : "example@example.com"
    "page_joined"    : "homepage",
    "tealium_event"  : "user_register"
}
```

### ユーザー更新

|イベント名|説明|
|---|---|
| `user_update`| ユーザーアカウントの更新が成功した際に発生します。|

サンプル:  
```javascript
{
    "customer_email" : "example@example.com",
    "tealium_event"  : "user_update"
}
```

### ビデオ

|イベント名|説明|
|---|---|
| `video`| ユーザーがサイト上のビデオと対話します。|

サンプル:  
```javascript
{
    "tealium_event"      : "video",
    "video_action"       : "play",
    "video_content_type" : "Property Video",
    "video_name"         : "Video Name",
    "video_segments"     : "75"
}
```