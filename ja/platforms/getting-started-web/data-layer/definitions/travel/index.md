---
title: 旅行データレイヤー仕様
description: この記事では、旅行のためのデータレイヤー定義を提供します。
url: https://docs.tealium.com/ja/platforms/getting-started-web/data-layer/definitions/travel/
---## データレイヤーの属性

|変数| 説明| 例| タイプ|
|---| ---| ---| ---|
|`aircraft_capacity`| 航空機の座席数| `148`| 文字列|
|`aircraft_type`| 航空機のタイプ| `A320`| 文字列|
|`avg_room_rate`| 各部屋の平均料金の配列| `["100.00"]`| 配列|
|`cancellation_id`| 予約キャンセル時に与えられるID| `987654654`| 文字列|
|`checkout_step`| チェックアウトプロセス中のステップ番号を指定| `3`| 文字列|
|`country_code`| 国コード| `us`| 文字列|
|`currency`| 通貨タイプ| `USD`| 文字列|
|`customer_city`| 顧客の居住都市を含む| `San Diego`| 文字列|
|`customer_country`| 顧客の居住国を含む| `United States`| 文字列|
|`customer_email`| 顧客のメールアドレスを含む| `johnsmith@example.com`| 文字列|
|`customer_first_name`| 主要連絡先の名| `John`| 文字列|
|`customer_id`| ユニークなユーザーIDを含む（現在のページ上で）| `8237572`| 文字列|
|`customer_last_name`| 主要連絡先の姓| `Smith`| 文字列|
|`customer_middle_name`| 主要連絡先のミドルネーム| `Alberto`| 文字列|
|`customer_nationality`| 主要顧客の国籍を指定| `Mexican`| 文字列|
|`customer_phone`| 主要連絡先の電話番号| `123-564-7894`| 文字列|
|`customer_postal_code`| 顧客の郵便番号を含む| `92101`| 文字列|
|`customer_state`| 顧客の居住州を含む| `CA`| 文字列|
|`customer_type`| 顧客のタイプを指定| `Web member`| 文字列|
|`days_to_trip_start`| 今日から旅行開始日までの日数| `20`| 文字列|
|`displayed_properties`| ホテル選択ページでリストされた各プロパティのIDの配列| `["234234","234256"]`| 配列|
|`displayed_rate_amount`| 部屋選択ページで表示される料金額| `100.00`| 文字列|
|`displayed_rate_codes`| ホテル選択ページでリストされた各プロパティの料金コードの配列| `["AAA","Corporate"]`| 配列|
|`displayed_room_rates`| 部屋タイプ別にグループ化された表示料金の配列| `["100.00","75.00"]`| 配列|
|`displayed_room_types`| 部屋選択ページで表示される部屋タイプの配列| `["2QueenBeds","studio"]`| 配列|
|`ecommerce_action`| eコマースイベントのアクションを指定| `detail`| 文字列|
|`error_message`| ユーザーに表示されるエラーテキスト| `Destination City doesn't match Departure on return`| 文字列|
|`fare_class`| 運賃クラスを指定| `Class L`| 文字列|
|`favorite_property_id`| 「お気に入り」としてキャプチャされたプロパティID| `79865`| 文字列|
|`filter_amenities`| 適用された選択の配列| `["pool","microwave"]`| 配列|
|`filter_distance`| イベントからのフィルター距離| `20`| 文字列|
|`filter_hotel_type`| ユーザーによってフィルターされたホテルタイプの配列| `["economy","luxury","brand"]`| 配列|
|`filter_max_rate`| 適用された料金をキャプチャ| `150`| 文字列|
|`filter_rating`| ユーザー、サイト、トリップアドバイザーなどによってフィルターされた評価の配列| `["3","4","5"]`| 配列|
|`flight_route`| ルート| `SAN-CUN,CUN-SAN`| 文字列|
|`flight_sku`| 製品SKUの配列| `["Y123","Z456"]`| 配列|
|`flight_type`| 往復、片道| `Round`| 文字列|
|`language_code`| 言語コード| `en`| 文字列|
|`link_action`| クリック追跡イベント中、クリックされた要素のアクション| `View Image`| 文字列|
|`link_category`| クリック追跡イベント中、クリックされた要素のカテゴリ| `Header`| 文字列|
|`link_name`| クリック追跡イベント中、クリックされた要素の名前| `Login`| 文字列|
|`link_value`| クリック追跡イベント中、クリックされた要素の値| `10`| 文字列|
|`login_status`| ユーザーがログインしているかログアウトしているか| `logged in`| 文字列|
|`loyalty_id`| ロイヤルティIDまたは会員番号| `46794561`| 文字列|
|`loyalty_point_balance`| ユーザーのロイヤルティアカウントの現在のポイント残高| `10,000`| 文字列|
|`loyalty_tier`| 会員ステータスレベル| `Silver`| 文字列|
|`num_adult_occupants`| 大人の総数| `3`| 文字列|
|`num_adult_passengers`| 予約に含まれる大人の乗客数| `1`| 文字列|
|`num_child_occupants`| 子供の総数| `3`| 文字列|
|`num_child_passengers`| 予約に含まれる子供の乗客数| `1`| 文字列|
|`num_of_nights`| 宿泊数の合計| `4`| 文字列|
|`num_of_rooms`| 部屋数の合計| `2`| 文字列|
|`occupancy_detail`| 検索された各部屋の総占有率の配列| `["3","3"]`| 配列|
|`order_cancellation_policy`| 注文の各部屋のキャンセルポリシーの配列| `["24 Hours","No Cancellation"]`| 配列|
|`order_corp_id`| 注文に添付された企業ID（ある場合）| `32132465475`| 文字列|
|`order_discount_amount`| 注文レベルの割引額を含む| `10.00`| 文字列|
|`order_grand_total`| 税金と送料を含むがすべての割引を除いた注文の総額を数字と小数点のみの文字列で| `54.47`| 文字列|
|`order_iata`| 注文に添付された国際航空運送協会番号（例：旅行代理店番号）| `654654`| 文字列|
|`order_id`| 注文確認ページで生成される注文のユニークID| `132133`| 文字列|
|`order_payment_type`| 支払いタイプを含む| `Paypal`| 文字列|
|`order_points_used`| 注文の各部屋の総ポイント量の配列| `2000`| 文字列|
|`order_promo_code`| コンマ区切りのプロモーションコードの文字列リスト| `MEX30`| 文字列|
|`order_rate_code`| 注文の各部屋で予約された料金コードの配列| `["AAA"]`| 配列|
|`order_special_requests`| 「特別リクエスト」フィールドに入力されたフリーテキスト（部屋ごと）| `No Feathers`| 文字列|
|`order_store`| ストアタイプのID| `mobile web`| 文字列|
|`order_subtotal`| すべての商品の価格を含むが、税金と送料を除く数字と小数点のみの文字列| `45.98`| 文字列|
|`order_tax_amount`| この注文の総税額を数字と小数点のみの文字列で| `2.50`| 文字列|
|`order_total_occupancy`| 予約時の注文の総占有率| `6`| 文字列|
|`origin_flight_route`| 出発フライト| `["SAN-CUN"]`| 配列|
|`page_name`| ページ名を識別するTealium変数| `Homepage`| 文字列|
|`page_type`| ページのタイプ| `home`| 文字列|
|`passenger_name`| 乗客名の配列| `["Steve","Jack"]`| 配列|
|`passenger_price`| 予約に含まれる各乗客の価格| `["100.00","120.00"]`| 配列|
|`product_impression_category`| インプレッション内の製品のカテゴリを指定（付帯サービスまたはフライト）| `["Flight"]`| 配列|
|`product_impression_id`| インプレッション内の製品のIDを指定| `["Y1234"]`| 配列|
|`product_impression_name`| インプレッション内の製品の名前を指定| `["CUN-MEX"]`| 配列|
|`product_impression_position`| インプレッション内の製品の位置を指定| `["1"]`| 配列|
|`product_impression_price`| インプレッション内の製品の価格を指定| `["12.99"]`| 配列|
|`product_impression_variant`| インプレッション内の製品のバリアントを指定| `["1A"]`| 配列|
|`product_name`| 製品名| `["Seat","Room","Car"]`| 配列|
|`product_price`| 製品価格| `["123.00","250.00","59.30"]`| 配列|
|`promo_registration_page`| プロモーション登録が行われたページ| `Promo`| 文字列|
|`promotion_creative`| プロモーションのクリエイティブ名を指定| `Fall Sale`| 文字列|
|`promotion_name`| プロモーション内の製品の名前を指定| `Promo One`| 文字列|
|`property_brand`| プロパティのブランド名| `["Rest Eazy","Best Motels"]`| 配列|
|`property_city`| プロパティが位置する都市| `["San Francisco","Monterey Bay"]`| 配列|
|`property_country`| プロパティが位置する国| `["San Francisco","Monterey"]`| 配列|
|`property_id`| プロパティ番号の配列| `["HI456767","BW123"]`| 配列|
|`property_name`| プロパティ名の配列| `["Holiday Inn SF","Mont. Best Motels"]`| 配列|
|`property_postal_code`| プロパティの郵便番号の配列| `["99999","11111"]`| 配列|
|`property_room_occupancy`| 注文の各部屋の総占有率の配列| `["3","3"]`| 配列|
|`property_room_type`| 各部屋の予約された部屋の配列 | `["economy"]`| 配列|
|`property_state`| 物件が位置する州の配列 | `["CA","CA"]`| 配列|
|`proximity`| 市中心部と物件の位置の距離（マイル）の配列 | `["20","30"]`| 配列|
|`quantity`| 各製品の数量の配列 | `["2","2"]`| 配列|
|`returning_flight_route`| 帰りのフライト | `["CUN-SAN"]`| 配列|
|`search_city`| 検索された目的地の都市 | `Cancun`| 文字列|
|`search_country`| 検索された目的地の国 | `USA`| 文字列|
|`search_rate`| 予約ウィジェットのレート選択ドロップダウンメニューから選択されたレート | `105`| 文字列|
|`search_rate_value`| 予約ウィジェットのレート選択ドロップダウンメニューから入力されたプロモーションと企業選択の値 | `AAA`| 文字列|
|`search_results`| 検索によって返されたフライトの数 | `42`| 文字列|
|`search_state`| 検索された目的地の州 | `CA`| 文字列|
|`search_type`| Googleによって定義された目的地のタイプ | `airport`| 文字列|
|`select_room_position`| Select HotelページからSelect Roomページで表示されたレートの最高位置 | `5`| 文字列|
|`show_available`| 利用可能なホテルのみを表示する構成; trueまたはfalse | `true`| 文字列|
|`site_section`| サイトの高レベルセクション | `Loyalty`| 文字列|
|`social_channel`| ソーシャルメディアで情報が共有されたときにイベントで使用 | `Facebook`| 文字列|
|`sort_by`| 並び替え選択（距離、低から高、高から低） | `distance`| 文字列|
|`total_passengers`| 予約の総乗客数 | `3`| 文字列|
|`transactionAffiliation`| 支払いに使用された支払いタイプを指定 | `Visa`| 文字列|
|`trip_end_date`| ユーザーのホテルまたは車の出発日、航空会社の到着日 | `03/12/2017`| 文字列|
|`trip_start_date`| ユーザーのホテルまたは車の到着日、航空会社の出発日 | `03/02/2017`| 文字列|
|`variant`| 座席番号またはエクストラ | `["14F","15D","baggage","car"]`| 配列|
|`video_action`| 現在ビデオで行われているアクション | `play`| 文字列|
|`video_content_type`| 視聴されたビデオのタイプ | `hotel promo`| 文字列|
|`video_name`| 視聴されたビデオの名前 | `Stay the Night`| 文字列|
|`video_segments`| ビデオの視聴されたパーセンテージ | `50`| 文字列|

## ページ追跡

### ホームページ

|イベント名|説明|
|---|---|
| `page_view`| ホームページ。|

サンプル:  
```javascript
{
    "currency"       : "USD",
    "customer_email" : "johnsmith@example.com",
    "customer_id"    : "8237572",
    "login_status"   : "logged in",
    "page_name"      : "Homepage",
    "page_type"      : "home",
    "site_section"   : "Loyalty",
    "tealium_event"  : "page_view"
}
```

### フライトページ

|イベント名|説明|
|---|---|
| `page_view`| フライト選択ページ。|

サンプル:  
```javascript
{
    "currency"                    : "USD",
    "customer_email"              : "johnsmith@example.com",
    "customer_id"                 : "8237572",
    "days_to_trip_start"          : "20",
    "fare_class"                  : "Class L",
    "flight_route"                : "SAN-CUN,CUN-SAN",
    "flight_type"                 : "Round",
    "login_status"               : "logged in",
    "num_adult_passengers"        : "1",
    "num_child_passengers"        : "1",
    "page_name"                   : "Homepage",
    "page_type"                   : "flight",
    "product_impression_category" : ["Flight"],
    "product_impression_id"       : ["Y1234"],
    "product_impression_name"     : ["CUN-MEX"],
    "product_impression_position" : ["1"],
    "product_impression_price"    : ["12.99"],
    "product_impression_variant"  : ["1A"],
    "product_name"                : ["Seat","Room","Car"],
    "product_price"               : ["123.00","250.00","59.30"],
    "site_section"                : "Loyalty",
    "tealium_event"               : "page_view",
    "trip_end_date"               : "03/12/2017",
    "trip_start_date"             : "03/02/2017"
}
```

### 宿泊ページ

|イベント名|説明|
|---|---|
| `page_view`| ホテル選択ページ。|

サンプル:  
```javascript
{
    "currency"                    : "USD",
    "customer_email"              : "johnsmith@example.com",
    "customer_id"                 : "8237572",
    "displayed_properties"        : ["234234","234256"],
    "displayed_rate_amount"       : "100.00",
    "displayed_rate_codes"        : ["AAA","Corporate"],
    "displayed_room_rates"        : ["100.00","75.00"],
    "displayed_room_types"        : ["2QueenBeds","studio"],
    "filter_amenities"            : ["pool","microwave"],
    "filter_distance"             : "20",
    "filter_hotel_type"           : ["economy","luxury","brand"],
    "filter_max_rate"             : "150",
    "filter_rating"               : ["3","4","5"],
    "login_status"                : "logged in",
    "num_adult_occupants"         : "3",
    "num_child_occupants"         : "3",
    "num_of_nights"               : "4",
    "page_name"                   : "Homepage",
    "page_type"                   : "lodging",
    "product_impression_category" : ["Flight"],
    "product_impression_id"       : ["Y1234"],
    "product_impression_name"     : ["CUN-MEX"],
    "product_impression_position" : ["1"],
    "product_impression_price"    : ["12.99"],
    "product_impression_variant"  : ["1A"],
    "product_name"                : ["Seat","Room","Car"],
    "product_price"               : ["123.00","250.00","59.30"],
    "property_brand"              : ["Rest Eazy","Best Motels"],
    "property_city"               : ["San Francisco","Monterey Bay"],
    "property_country"            : ["San Francisco","Monterey"],
    "property_id"                 : ["HI456767","BW123"],
    "property_name"               : ["Rest Eazy SF","Best Motels Mont"],
    "property_postal_code"        : ["99999","11111"],
    "property_room_occupancy"     : ["3","3"],
    "property_room_type"          : ["economy"],
    "property_state"              : ["CA","CA"],
    "proximity"                   : ["20","30"],
    "quantity"                    : ["2","2"],
    "site_section"                : "Loyalty",
    "tealium_event"               : "page_view",
    "trip_end_date"               : "03/12/2017",
    "trip_start_date"             : "03/02/2017"
}
```

### レンタルページ

|イベント名|説明|
|---|---|
| `page_view`| レンタカー選択ページ。|

サンプル:  
```javascript
{
    "currency"                    : "USD",
    "customer_email"              : "johnsmith@example.com",
    "customer_id"                 : "8237572",
    "login_status"                : "logged in",
    "num_of_nights"               : "4",
    "page_name"                   : "Homepage",
    "page_type"                   : "rental",
    "product_impression_category" : ["Flight"],
    "product_impression_id"       : ["Y1234"],
    "product_impression_name"     : ["CUN-MEX"],
    "product_impression_position" : ["1"],
    "product_impression_price"    : ["12.99"],
    "product_impression_variant"  : ["1A"],
    "product_name"                : ["Seat","Room","Car"],
    "product_price"               : ["123.00","250.00","59.30"],
    "quantity"                    : ["2","2"],
    "site_section"                : "Loyalty",
    "tealium_event"               : "page_view",
    "trip_end_date"               : "03/12/2017",
    "trip_start_date"             : "03/02/2017"
}
```
### 検索ページ

|イベント名|説明|
|---|---|
| `search`| 検索結果ページ。|

サンプル:  
```javascript
{
    "checkout_step"               : "3",
    "currency"                    : "USD",
    "customer_email"              : "johnsmith@example.com",
    "customer_id"                 : "8237572",
    "customer_type"               : "Web member",
    "days_to_trip_start"          : "20",
    "flight_route"                : "SAN-CUN,CUN-SAN",
    "flight_type"                 : "Round",
    "login_status"                : "logged in",
    "num_adult_passengers"        : "1",
    "num_child_passengers"        : "1",
    "origin_flight_route"         : ["SAN-CUN"],
    "page_name"                   : "Homepage",
    "page_type"                   : "search",
    "product_impression_category" : ["Flight"],
    "product_impression_id"       : ["Y1234"],
    "product_impression_name"     : ["CUN-MEX"],
    "product_impression_position" : ["1"],
    "product_impression_price"    : ["12.99"],
    "product_impression_variant"  : ["1A"],
    "product_name"                : ["Seat","Room","Car"],
    "product_price"               : ["123.00","250.00","59.30"],
    "returning_flight_route"      : ["CUN-SAN"],
    "site_section"                : "Loyalty",
    "sort_by"                     : "distance",
    "tealium_event"               : "search",
    "total_passengers"            : "3",
    "trip_end_date"               : "03/12/2017",
    "trip_start_date"             : "03/02/2017"
}
```

### 予約フローページ

|イベント名|説明|
|---|---|
| `page_view`| チェックアウトページ。|

サンプル:  
```javascript
{
    "checkout_step"          : "3",
    "currency"               : "USD",
    "customer_email"         : "johnsmith@example.com",
    "customer_id"            : "8237572",
    "customer_type"          : "Web member",
    "fare_class"             : "Class L",
    "flight_route"           : "SAN-CUN,CUN-SAN",
    "flight_sku"             : ["Y123","Z456"],
    "flight_type"            : "Round",
    "login_status"           : "logged in",
    "loyalty_id"             : "46794561",
    "num_adult_passengers"   : "1",
    "num_child_passengers"   : "1",
    "origin_flight_route"    : ["SAN-CUN"],
    "page_name"              : "Homepage",
    "page_type"              : "booking_flow",
    "passenger_name"         : ["Steve","jack"],
    "passenger_price"        : ["100.00","120.00"],
    "product_name"           : ["Seat","Room","Car"],
    "product_price"          : ["123.00","250.00","59.30"],
    "quantity"               : ["2","2"],
    "returning_flight_route" : ["CUN-SAN"],
    "site_section"           : "Loyalty",
    "tealium_event"          : "page_view",
    "total_passengers"       : "3",
    "trip_end_date"          : "03/12/2017",
    "trip_start_date"        : "03/02/2017",
    "variant"                : ["14F","15D","baggage","car"]
}
```

### 注文ページ

|イベント名|説明|
|---|---|
| `purchase`| 注文確認/領収書/サンキューページ。|

サンプル:  
```javascript
{
    "aircraft_capacity"         : "148",
    "aircraft_type"             : "A320",
    "checkout_step"             : "3",
    "currency"                  : "USD",
    "customer_email"            : "johnsmith@example.com",
    "customer_id"               : "8237572",
    "customer_type"             : "Web member",
    "fare_class"                : "Class L",
    "flight_route"              : "SAN-CUN,CUN-SAN",
    "flight_sku"                : ["Y123","Z456"],
    "flight_type"               : "Round",
    "login_status"              : "logged in",
    "loyalty_id"               : "46794561",
    "num_adult_passengers"      : "1",
    "num_child_passengers"      : "1",
    "occupancy_detail"          : ["3","3"],
    "order_cancellation_policy" : ["24 Hours","No Cancellation"],
    "order_grand_total"         : "54.47",
    "order_id"                  : "132133",
    "order_payment_type"        : "paypal",
    "order_promo_code"          : "MEX30",
    "order_store"               : "mobile web",
    "order_subtotal"            : "45.98",
    "order_tax_amount"          : "2.50",
    "origin_flight_route"       : ["SAN-CUN"],
    "page_name"                 : "Homepage",
    "page_type"                 : "order",
    "passenger_name"            : ["Steve","jack"],
    "passenger_price"           : ["100.00","120.00"],
    "quantity"                  : ["2","2"],
    "returning_flight_route"    : ["CUN-SAN"],
    "site_section"              : "Loyalty",
    "tealium_event"             : "purchase",
    "total_passengers"          : "3",
    "transactionAffiliation"    : "Visa",
    "trip_end_date"             : "03/12/2017",
    "trip_start_date"           : "03/02/2017",
    "variant"                   : ["14F","15D","baggage","car"]
}
```

### 予約管理ページ

|イベント名|説明|
|---|---|
| `page_view`| 予約管理ページ。|

サンプル:  
```javascript
{
    "currency"       : "USD",
    "customer_email" : "johnsmith@example.com",
    "customer_id"    : "8237572",
    "fare_class"     : "Class L",
    "flight_type"    : "Round",
    "login_status"   : "logged in",
    "page_name"      : "Homepage",
    "page_type"      : "manage_your_booking",
    "site_section"   : "Loyalty",
    "tealium_event"  : "page_view"
}
```

### チェックインページ

|イベント名|説明|
|---|---|
| `page_view`| チェックインフロー。|

サンプル:  
```javascript
{
    "checkout_step"          : "3",
    "currency"               : "USD",
    "customer_email"         : "johnsmith@example.com",
    "customer_id"            : "8237572",
    "fare_class"             : "Class L",
    "flight_route"           : "SAN-CUN,CUN-SAN",
    "flight_sku"             : ["Y123","Z456"],
    "flight_type"            : "Round",
    "login_status"           : "logged in",
    "origin_flight_route"    : ["SAN-CUN"],
    "page_name"              : "Homepage",
    "page_type"              : "check_in",
    "passenger_name"         : ["Steve","jack"],
    "returning_flight_route" : ["CUN-SAN"],
    "site_section"           : "Loyalty",
    "tealium_event"          : "page_view",
    "trip_end_date"          : "03/12/2017",
    "trip_start_date"        : "03/02/2017"
}
```

### アカウントページ

|イベント名|説明|
|---|---|
| `page_view`| ユーザーアカウントログイン。|

サンプル:  
```javascript
{
    "checkout_step"  : "3",
    "currency"       : "USD",
    "customer_email" : "johnsmith@example.com",
    "customer_id"    : "8237572",
    "customer_type"  : "Web member",
    "login_status"   : "logged in",
    "loyalty_id"     : "46794561",
    "page_name"      : "Homepage",
    "page_type"      : "account",
    "site_section"   : "Loyalty",
    "tealium_event"  : "page_view"
}
```

### ランディングページ

|イベント名|説明|
|---|---|
| `page_view`| ランディングページおよびフォームページ（団体旅行）。|

サンプル:  
```javascript
{
    "currency"       : "USD",
    "customer_email" : "johnsmith@example.com",
    "customer_id"    : "8237572",
    "login_status"   : "logged in",
    "page_name"      : "Homepage",
    "page_type"      : "landing",
    "site_section"   : "Loyalty",
    "tealium_event"  : "page_view"
}
```

### 汎用ページ

|イベント名|説明|
|---|---|
| `page_view`| その他のページ。|

サンプル:  
```javascript
{
    "currency"       : "USD",
    "customer_email" : "johnsmith@example.com",
    "customer_id"    : "8237572",
    "login_status"   : "logged in",
    "page_name"      : "Other Page",
    "page_type"      : "content",
    "site_section"   : "Loyalty",
    "tealium_event"  : "page_view"
}
```

## イベントトラッキング
### カート追加

|イベント名|説明|
|---|---|
| `cart_add`| カートに追加するイベント。|

サンプル:  
```javascript
{
    "avg_room_rate"           : ["100.00"],
    "checkout_step"           : "3",
    "customer_type"           : "Web member",
    "days_to_trip_start"      : "20",
    "ecommerce_action"        : "detail",
    "num_adult_occupants"     : "3",
    "num_adult_passengers"    : "1",
    "num_child_occupants"     : "3",
    "num_child_passengers"    : "1",
    "num_of_nights"           : "4",
    "num_of_rooms"            : "2",
    "origin_flight_route"     : ["SAN-CUN"],
    "product_name"            : ["Seat","Room","Car"],
    "product_price"           : ["123.00","250.00","59.30"],
    "property_id"             : ["HI456767","BW123"],
    "property_name"           : ["Rest Eazy","Best Motels"],
    "property_postal_code"    : ["99999","11111"],
    "property_room_occupancy" : ["3","3"],
    "property_room_type"      : ["economy"],
    "property_state"          : ["CA","CA"],
    "proximity"               : ["20","30"],
    "quantity"                : ["2","2"],
    "returning_flight_route"  : ["CUN-SAN"],
    "tealium_event"           : "cart_add",
    "total_passengers"        : "3",
    "trip_end_date"           : "03/12/2017",
    "trip_start_date"         : "03/02/2017",
    "variant"                 : ["14F","15D","baggage","car"]
}
```

### カート削除

|イベント名|説明|
|---|---|
| `cart_remove`| カートから削除するイベント。|

サンプル:  
```javascript
{
    "checkout_step"          : "3",
    "customer_type"          : "Web member",
    "days_to_trip_start"     : "20",
    "ecommerce_action"       : "detail",
    "origin_flight_route"    : ["SAN-CUN"],
    "product_name"           : ["Seat","Room","Car"],
    "product_price"          : ["123.00","250.00","59.30"],
    "quantity"               : ["2","2"],
    "returning_flight_route" : ["CUN-SAN"],
    "tealium_event"          : "cart_remove"
}
```

### ユーザーログイン

|イベント名|説明|
|---|---|
| `user_login`| ユーザーがログインに成功した際のイベント。|

サンプル:  
```javascript
{
    "customer_email" : "johnsmith@example.com",
    "customer_id"    : "8237572",
    "login_status"   : "logged in",
    "tealium_event"  : "user_login"
}
```

### ユーザーログアウト

|イベント名|説明|
|---|---|
| `user_logout`| ユーザーがログアウトに成功した際のイベント。|

サンプル:  
```javascript
{
    "customer_email" : "johnsmith@example.com",
    "customer_id"    : "8237572",
    "login_status"   : "logged in",
    "tealium_event"  : "user_logout"
}
```

### ユーザー登録

|イベント名|説明|
|---|---|
| `user_register`| ユーザーが登録に成功した際のイベント。|

サンプル:  
```javascript
{
    "customer_email" : "johnsmith@example.com",
    "customer_id"    : "8237572",
    "tealium_event"  : "user_register"
}
```

### ユーザー更新

|イベント名|説明|
|---|---|
| `user_update`| ユーザーアカウントの更新に成功した際のイベント。|

サンプル:  
```javascript
{
    "customer_email" : "johnsmith@example.com",
    "customer_id"    : "8237572",
    "tealium_event"  : "user_update"
}
```

### メールサインアップ

|イベント名|説明|
|---|---|
| `email_signup`| メールアップデート/ニュースレターへのサインアップに成功した際のイベント。|

サンプル:  
```javascript
{
    "customer_email" : "johnsmith@example.com",
    "tealium_event"  : "email_signup"
}
```

### カスタムクリック

|イベント名|説明|
|---|---|
| `custom_click`| 特定のページ要素をクリックした際のイベント。|

サンプル:  
```javascript
{
    "link_action"   : "View Image",
    "link_category" : "Header",
    "link_name"     : "Login",
    "link_value"    : "10",
    "tealium_event" : "custom_click"
}
```

### 商品クリック

|イベント名|説明|
|---|---|
| `product_click`| 商品の詳細ページやクイックビューをロードするリンクをクリックした際のイベント。|

サンプル:  
```javascript
{
    "ecommerce_action" : "detail",
    "fare_class"       : "Class L",
    "tealium_event"    : "product_click"
}
```

### プロモクリック

|イベント名|説明|
|---|---|
| `promo_click`| プロモーションをクリックした際のイベント。|

サンプル:  
```javascript
{
    "ecommerce_action"        : "detail",
    "promo_registration_page" : "",
    "promotion_name"          : "Promo One",
    "tealium_event"           : "promo_click"
}
```

### エラーメッセージ

|イベント名|説明|
|---|---|
| `error_message`| エラーを知らせるメッセージをユーザーが閲覧した際のイベント。|

サンプル:  
```javascript
{
    "checkout_step"          : "3",
    "error_mesage"           : "Destination City doesn't match Departure on return",
    "flight_route"           : "SAN-CUN,CUN-SAN",
    "flight_type"            : "Round",
    "origin_flight_route"    : ["SAN-CUN"],
    "page_name"              : "Homepage",
    "returning_flight_route" : ["CUN-SAN"],
    "tealium_event"          : "error_message",
    "total_passengers"       : "3"
}
```

### ビデオ

|イベント名|説明|
|---|---|
| `video`| サイト上のビデオとのインタラクションが発生した際のイベント。|

サンプル:  
```javascript
{
    "tealium_event"      : "video",
    "video_action"       : "play",
    "video_content_type" : "hotel promo",
    "video_name"         : "Stay the Night",
    "video_segments"     : "50"
}
```