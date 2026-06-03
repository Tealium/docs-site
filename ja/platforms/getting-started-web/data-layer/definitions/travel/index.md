---
title: 旅行データレイヤー仕様
description: この記事では、旅行のためのデータレイヤー定義を提供します。
url: https://docs.tealium.com/ja/platforms/getting-started-web/data-layer/definitions/travel/
---## データレイヤーの属性

|変数| 説明| 例| タイプ|
|---| ---| ---| ---|
|`aircraft_capacity`| 航空機の座席数| `148`| 文字列|
|`aircraft_type`| 航空機のタイプ| `A320`| 文字列|
|`avg_room_rate`| 各部屋の平均料金の配列| `[&#34;100.00&#34;]`| 配列|
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
|`displayed_properties`| ホテル選択ページでリストされた各プロパティのIDの配列| `[&#34;234234&#34;,&#34;234256&#34;]`| 配列|
|`displayed_rate_amount`| 部屋選択ページで表示される料金額| `100.00`| 文字列|
|`displayed_rate_codes`| ホテル選択ページでリストされた各プロパティの料金コードの配列| `[&#34;AAA&#34;,&#34;Corporate&#34;]`| 配列|
|`displayed_room_rates`| 部屋タイプ別にグループ化された表示料金の配列| `[&#34;100.00&#34;,&#34;75.00&#34;]`| 配列|
|`displayed_room_types`| 部屋選択ページで表示される部屋タイプの配列| `[&#34;2QueenBeds&#34;,&#34;studio&#34;]`| 配列|
|`ecommerce_action`| eコマースイベントのアクションを指定| `detail`| 文字列|
|`error_message`| ユーザーに表示されるエラーテキスト| `Destination City doesn&#39;t match Departure on return`| 文字列|
|`fare_class`| 運賃クラスを指定| `Class L`| 文字列|
|`favorite_property_id`| 「お気に入り」としてキャプチャされたプロパティID| `79865`| 文字列|
|`filter_amenities`| 適用された選択の配列| `[&#34;pool&#34;,&#34;microwave&#34;]`| 配列|
|`filter_distance`| イベントからのフィルター距離| `20`| 文字列|
|`filter_hotel_type`| ユーザーによってフィルターされたホテルタイプの配列| `[&#34;economy&#34;,&#34;luxury&#34;,&#34;brand&#34;]`| 配列|
|`filter_max_rate`| 適用された料金をキャプチャ| `150`| 文字列|
|`filter_rating`| ユーザー、サイト、トリップアドバイザーなどによってフィルターされた評価の配列| `[&#34;3&#34;,&#34;4&#34;,&#34;5&#34;]`| 配列|
|`flight_route`| ルート| `SAN-CUN,CUN-SAN`| 文字列|
|`flight_sku`| 製品SKUの配列| `[&#34;Y123&#34;,&#34;Z456&#34;]`| 配列|
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
|`occupancy_detail`| 検索された各部屋の総占有率の配列| `[&#34;3&#34;,&#34;3&#34;]`| 配列|
|`order_cancellation_policy`| 注文の各部屋のキャンセルポリシーの配列| `[&#34;24 Hours&#34;,&#34;No Cancellation&#34;]`| 配列|
|`order_corp_id`| 注文に添付された企業ID（ある場合）| `32132465475`| 文字列|
|`order_discount_amount`| 注文レベルの割引額を含む| `10.00`| 文字列|
|`order_grand_total`| 税金と送料を含むがすべての割引を除いた注文の総額を数字と小数点のみの文字列で| `54.47`| 文字列|
|`order_iata`| 注文に添付された国際航空運送協会番号（例：旅行代理店番号）| `654654`| 文字列|
|`order_id`| 注文確認ページで生成される注文のユニークID| `132133`| 文字列|
|`order_payment_type`| 支払いタイプを含む| `Paypal`| 文字列|
|`order_points_used`| 注文の各部屋の総ポイント量の配列| `2000`| 文字列|
|`order_promo_code`| コンマ区切りのプロモーションコードの文字列リスト| `MEX30`| 文字列|
|`order_rate_code`| 注文の各部屋で予約された料金コードの配列| `[&#34;AAA&#34;]`| 配列|
|`order_special_requests`| 「特別リクエスト」フィールドに入力されたフリーテキスト（部屋ごと）| `No Feathers`| 文字列|
|`order_store`| ストアタイプのID| `mobile web`| 文字列|
|`order_subtotal`| すべての商品の価格を含むが、税金と送料を除く数字と小数点のみの文字列| `45.98`| 文字列|
|`order_tax_amount`| この注文の総税額を数字と小数点のみの文字列で| `2.50`| 文字列|
|`order_total_occupancy`| 予約時の注文の総占有率| `6`| 文字列|
|`origin_flight_route`| 出発フライト| `[&#34;SAN-CUN&#34;]`| 配列|
|`page_name`| ページ名を識別するTealium変数| `Homepage`| 文字列|
|`page_type`| ページのタイプ| `home`| 文字列|
|`passenger_name`| 乗客名の配列| `[&#34;Steve&#34;,&#34;Jack&#34;]`| 配列|
|`passenger_price`| 予約に含まれる各乗客の価格| `[&#34;100.00&#34;,&#34;120.00&#34;]`| 配列|
|`product_impression_category`| インプレッション内の製品のカテゴリを指定（付帯サービスまたはフライト）| `[&#34;Flight&#34;]`| 配列|
|`product_impression_id`| インプレッション内の製品のIDを指定| `[&#34;Y1234&#34;]`| 配列|
|`product_impression_name`| インプレッション内の製品の名前を指定| `[&#34;CUN-MEX&#34;]`| 配列|
|`product_impression_position`| インプレッション内の製品の位置を指定| `[&#34;1&#34;]`| 配列|
|`product_impression_price`| インプレッション内の製品の価格を指定| `[&#34;12.99&#34;]`| 配列|
|`product_impression_variant`| インプレッション内の製品のバリアントを指定| `[&#34;1A&#34;]`| 配列|
|`product_name`| 製品名| `[&#34;Seat&#34;,&#34;Room&#34;,&#34;Car&#34;]`| 配列|
|`product_price`| 製品価格| `[&#34;123.00&#34;,&#34;250.00&#34;,&#34;59.30&#34;]`| 配列|
|`promo_registration_page`| プロモーション登録が行われたページ| `Promo`| 文字列|
|`promotion_creative`| プロモーションのクリエイティブ名を指定| `Fall Sale`| 文字列|
|`promotion_name`| プロモーション内の製品の名前を指定| `Promo One`| 文字列|
|`property_brand`| プロパティのブランド名| `[&#34;Rest Eazy&#34;,&#34;Best Motels&#34;]`| 配列|
|`property_city`| プロパティが位置する都市| `[&#34;San Francisco&#34;,&#34;Monterey Bay&#34;]`| 配列|
|`property_country`| プロパティが位置する国| `[&#34;San Francisco&#34;,&#34;Monterey&#34;]`| 配列|
|`property_id`| プロパティ番号の配列| `[&#34;HI456767&#34;,&#34;BW123&#34;]`| 配列|
|`property_name`| プロパティ名の配列| `[&#34;Holiday Inn SF&#34;,&#34;Mont. Best Motels&#34;]`| 配列|
|`property_postal_code`| プロパティの郵便番号の配列| `[&#34;99999&#34;,&#34;11111&#34;]`| 配列|
|`property_room_occupancy`| 注文の各部屋の総占有率の配列| `[&#34;3&#34;,&#34;3&#34;]`| 配列|
|`property_room_type`| 各部屋の予約された部屋の配列 | `[&#34;economy&#34;]`| 配列|
|`property_state`| 物件が位置する州の配列 | `[&#34;CA&#34;,&#34;CA&#34;]`| 配列|
|`proximity`| 市中心部と物件の位置の距離（マイル）の配列 | `[&#34;20&#34;,&#34;30&#34;]`| 配列|
|`quantity`| 各製品の数量の配列 | `[&#34;2&#34;,&#34;2&#34;]`| 配列|
|`returning_flight_route`| 帰りのフライト | `[&#34;CUN-SAN&#34;]`| 配列|
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
|`variant`| 座席番号またはエクストラ | `[&#34;14F&#34;,&#34;15D&#34;,&#34;baggage&#34;,&#34;car&#34;]`| 配列|
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
    &#34;currency&#34;       : &#34;USD&#34;,
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;    : &#34;8237572&#34;,
    &#34;login_status&#34;   : &#34;logged in&#34;,
    &#34;page_name&#34;      : &#34;Homepage&#34;,
    &#34;page_type&#34;      : &#34;home&#34;,
    &#34;site_section&#34;   : &#34;Loyalty&#34;,
    &#34;tealium_event&#34;  : &#34;page_view&#34;
}
```

### フライトページ

|イベント名|説明|
|---|---|
| `page_view`| フライト選択ページ。|

サンプル:  
```javascript
{
    &#34;currency&#34;                    : &#34;USD&#34;,
    &#34;customer_email&#34;              : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;                 : &#34;8237572&#34;,
    &#34;days_to_trip_start&#34;          : &#34;20&#34;,
    &#34;fare_class&#34;                  : &#34;Class L&#34;,
    &#34;flight_route&#34;                : &#34;SAN-CUN,CUN-SAN&#34;,
    &#34;flight_type&#34;                 : &#34;Round&#34;,
    &#34;login_status&#34;               : &#34;logged in&#34;,
    &#34;num_adult_passengers&#34;        : &#34;1&#34;,
    &#34;num_child_passengers&#34;        : &#34;1&#34;,
    &#34;page_name&#34;                   : &#34;Homepage&#34;,
    &#34;page_type&#34;                   : &#34;flight&#34;,
    &#34;product_impression_category&#34; : [&#34;Flight&#34;],
    &#34;product_impression_id&#34;       : [&#34;Y1234&#34;],
    &#34;product_impression_name&#34;     : [&#34;CUN-MEX&#34;],
    &#34;product_impression_position&#34; : [&#34;1&#34;],
    &#34;product_impression_price&#34;    : [&#34;12.99&#34;],
    &#34;product_impression_variant&#34;  : [&#34;1A&#34;],
    &#34;product_name&#34;                : [&#34;Seat&#34;,&#34;Room&#34;,&#34;Car&#34;],
    &#34;product_price&#34;               : [&#34;123.00&#34;,&#34;250.00&#34;,&#34;59.30&#34;],
    &#34;site_section&#34;                : &#34;Loyalty&#34;,
    &#34;tealium_event&#34;               : &#34;page_view&#34;,
    &#34;trip_end_date&#34;               : &#34;03/12/2017&#34;,
    &#34;trip_start_date&#34;             : &#34;03/02/2017&#34;
}
```

### 宿泊ページ

|イベント名|説明|
|---|---|
| `page_view`| ホテル選択ページ。|

サンプル:  
```javascript
{
    &#34;currency&#34;                    : &#34;USD&#34;,
    &#34;customer_email&#34;              : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;                 : &#34;8237572&#34;,
    &#34;displayed_properties&#34;        : [&#34;234234&#34;,&#34;234256&#34;],
    &#34;displayed_rate_amount&#34;       : &#34;100.00&#34;,
    &#34;displayed_rate_codes&#34;        : [&#34;AAA&#34;,&#34;Corporate&#34;],
    &#34;displayed_room_rates&#34;        : [&#34;100.00&#34;,&#34;75.00&#34;],
    &#34;displayed_room_types&#34;        : [&#34;2QueenBeds&#34;,&#34;studio&#34;],
    &#34;filter_amenities&#34;            : [&#34;pool&#34;,&#34;microwave&#34;],
    &#34;filter_distance&#34;             : &#34;20&#34;,
    &#34;filter_hotel_type&#34;           : [&#34;economy&#34;,&#34;luxury&#34;,&#34;brand&#34;],
    &#34;filter_max_rate&#34;             : &#34;150&#34;,
    &#34;filter_rating&#34;               : [&#34;3&#34;,&#34;4&#34;,&#34;5&#34;],
    &#34;login_status&#34;                : &#34;logged in&#34;,
    &#34;num_adult_occupants&#34;         : &#34;3&#34;,
    &#34;num_child_occupants&#34;         : &#34;3&#34;,
    &#34;num_of_nights&#34;               : &#34;4&#34;,
    &#34;page_name&#34;                   : &#34;Homepage&#34;,
    &#34;page_type&#34;                   : &#34;lodging&#34;,
    &#34;product_impression_category&#34; : [&#34;Flight&#34;],
    &#34;product_impression_id&#34;       : [&#34;Y1234&#34;],
    &#34;product_impression_name&#34;     : [&#34;CUN-MEX&#34;],
    &#34;product_impression_position&#34; : [&#34;1&#34;],
    &#34;product_impression_price&#34;    : [&#34;12.99&#34;],
    &#34;product_impression_variant&#34;  : [&#34;1A&#34;],
    &#34;product_name&#34;                : [&#34;Seat&#34;,&#34;Room&#34;,&#34;Car&#34;],
    &#34;product_price&#34;               : [&#34;123.00&#34;,&#34;250.00&#34;,&#34;59.30&#34;],
    &#34;property_brand&#34;              : [&#34;Rest Eazy&#34;,&#34;Best Motels&#34;],
    &#34;property_city&#34;               : [&#34;San Francisco&#34;,&#34;Monterey Bay&#34;],
    &#34;property_country&#34;            : [&#34;San Francisco&#34;,&#34;Monterey&#34;],
    &#34;property_id&#34;                 : [&#34;HI456767&#34;,&#34;BW123&#34;],
    &#34;property_name&#34;               : [&#34;Rest Eazy SF&#34;,&#34;Best Motels Mont&#34;],
    &#34;property_postal_code&#34;        : [&#34;99999&#34;,&#34;11111&#34;],
    &#34;property_room_occupancy&#34;     : [&#34;3&#34;,&#34;3&#34;],
    &#34;property_room_type&#34;          : [&#34;economy&#34;],
    &#34;property_state&#34;              : [&#34;CA&#34;,&#34;CA&#34;],
    &#34;proximity&#34;                   : [&#34;20&#34;,&#34;30&#34;],
    &#34;quantity&#34;                    : [&#34;2&#34;,&#34;2&#34;],
    &#34;site_section&#34;                : &#34;Loyalty&#34;,
    &#34;tealium_event&#34;               : &#34;page_view&#34;,
    &#34;trip_end_date&#34;               : &#34;03/12/2017&#34;,
    &#34;trip_start_date&#34;             : &#34;03/02/2017&#34;
}
```

### レンタルページ

|イベント名|説明|
|---|---|
| `page_view`| レンタカー選択ページ。|

サンプル:  
```javascript
{
    &#34;currency&#34;                    : &#34;USD&#34;,
    &#34;customer_email&#34;              : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;                 : &#34;8237572&#34;,
    &#34;login_status&#34;                : &#34;logged in&#34;,
    &#34;num_of_nights&#34;               : &#34;4&#34;,
    &#34;page_name&#34;                   : &#34;Homepage&#34;,
    &#34;page_type&#34;                   : &#34;rental&#34;,
    &#34;product_impression_category&#34; : [&#34;Flight&#34;],
    &#34;product_impression_id&#34;       : [&#34;Y1234&#34;],
    &#34;product_impression_name&#34;     : [&#34;CUN-MEX&#34;],
    &#34;product_impression_position&#34; : [&#34;1&#34;],
    &#34;product_impression_price&#34;    : [&#34;12.99&#34;],
    &#34;product_impression_variant&#34;  : [&#34;1A&#34;],
    &#34;product_name&#34;                : [&#34;Seat&#34;,&#34;Room&#34;,&#34;Car&#34;],
    &#34;product_price&#34;               : [&#34;123.00&#34;,&#34;250.00&#34;,&#34;59.30&#34;],
    &#34;quantity&#34;                    : [&#34;2&#34;,&#34;2&#34;],
    &#34;site_section&#34;                : &#34;Loyalty&#34;,
    &#34;tealium_event&#34;               : &#34;page_view&#34;,
    &#34;trip_end_date&#34;               : &#34;03/12/2017&#34;,
    &#34;trip_start_date&#34;             : &#34;03/02/2017&#34;
}
```
### 検索ページ

|イベント名|説明|
|---|---|
| `search`| 検索結果ページ。|

サンプル:  
```javascript
{
    &#34;checkout_step&#34;               : &#34;3&#34;,
    &#34;currency&#34;                    : &#34;USD&#34;,
    &#34;customer_email&#34;              : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;                 : &#34;8237572&#34;,
    &#34;customer_type&#34;               : &#34;Web member&#34;,
    &#34;days_to_trip_start&#34;          : &#34;20&#34;,
    &#34;flight_route&#34;                : &#34;SAN-CUN,CUN-SAN&#34;,
    &#34;flight_type&#34;                 : &#34;Round&#34;,
    &#34;login_status&#34;                : &#34;logged in&#34;,
    &#34;num_adult_passengers&#34;        : &#34;1&#34;,
    &#34;num_child_passengers&#34;        : &#34;1&#34;,
    &#34;origin_flight_route&#34;         : [&#34;SAN-CUN&#34;],
    &#34;page_name&#34;                   : &#34;Homepage&#34;,
    &#34;page_type&#34;                   : &#34;search&#34;,
    &#34;product_impression_category&#34; : [&#34;Flight&#34;],
    &#34;product_impression_id&#34;       : [&#34;Y1234&#34;],
    &#34;product_impression_name&#34;     : [&#34;CUN-MEX&#34;],
    &#34;product_impression_position&#34; : [&#34;1&#34;],
    &#34;product_impression_price&#34;    : [&#34;12.99&#34;],
    &#34;product_impression_variant&#34;  : [&#34;1A&#34;],
    &#34;product_name&#34;                : [&#34;Seat&#34;,&#34;Room&#34;,&#34;Car&#34;],
    &#34;product_price&#34;               : [&#34;123.00&#34;,&#34;250.00&#34;,&#34;59.30&#34;],
    &#34;returning_flight_route&#34;      : [&#34;CUN-SAN&#34;],
    &#34;site_section&#34;                : &#34;Loyalty&#34;,
    &#34;sort_by&#34;                     : &#34;distance&#34;,
    &#34;tealium_event&#34;               : &#34;search&#34;,
    &#34;total_passengers&#34;            : &#34;3&#34;,
    &#34;trip_end_date&#34;               : &#34;03/12/2017&#34;,
    &#34;trip_start_date&#34;             : &#34;03/02/2017&#34;
}
```

### 予約フローページ

|イベント名|説明|
|---|---|
| `page_view`| チェックアウトページ。|

サンプル:  
```javascript
{
    &#34;checkout_step&#34;          : &#34;3&#34;,
    &#34;currency&#34;               : &#34;USD&#34;,
    &#34;customer_email&#34;         : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;            : &#34;8237572&#34;,
    &#34;customer_type&#34;          : &#34;Web member&#34;,
    &#34;fare_class&#34;             : &#34;Class L&#34;,
    &#34;flight_route&#34;           : &#34;SAN-CUN,CUN-SAN&#34;,
    &#34;flight_sku&#34;             : [&#34;Y123&#34;,&#34;Z456&#34;],
    &#34;flight_type&#34;            : &#34;Round&#34;,
    &#34;login_status&#34;           : &#34;logged in&#34;,
    &#34;loyalty_id&#34;             : &#34;46794561&#34;,
    &#34;num_adult_passengers&#34;   : &#34;1&#34;,
    &#34;num_child_passengers&#34;   : &#34;1&#34;,
    &#34;origin_flight_route&#34;    : [&#34;SAN-CUN&#34;],
    &#34;page_name&#34;              : &#34;Homepage&#34;,
    &#34;page_type&#34;              : &#34;booking_flow&#34;,
    &#34;passenger_name&#34;         : [&#34;Steve&#34;,&#34;jack&#34;],
    &#34;passenger_price&#34;        : [&#34;100.00&#34;,&#34;120.00&#34;],
    &#34;product_name&#34;           : [&#34;Seat&#34;,&#34;Room&#34;,&#34;Car&#34;],
    &#34;product_price&#34;          : [&#34;123.00&#34;,&#34;250.00&#34;,&#34;59.30&#34;],
    &#34;quantity&#34;               : [&#34;2&#34;,&#34;2&#34;],
    &#34;returning_flight_route&#34; : [&#34;CUN-SAN&#34;],
    &#34;site_section&#34;           : &#34;Loyalty&#34;,
    &#34;tealium_event&#34;          : &#34;page_view&#34;,
    &#34;total_passengers&#34;       : &#34;3&#34;,
    &#34;trip_end_date&#34;          : &#34;03/12/2017&#34;,
    &#34;trip_start_date&#34;        : &#34;03/02/2017&#34;,
    &#34;variant&#34;                : [&#34;14F&#34;,&#34;15D&#34;,&#34;baggage&#34;,&#34;car&#34;]
}
```

### 注文ページ

|イベント名|説明|
|---|---|
| `purchase`| 注文確認/領収書/サンキューページ。|

サンプル:  
```javascript
{
    &#34;aircraft_capacity&#34;         : &#34;148&#34;,
    &#34;aircraft_type&#34;             : &#34;A320&#34;,
    &#34;checkout_step&#34;             : &#34;3&#34;,
    &#34;currency&#34;                  : &#34;USD&#34;,
    &#34;customer_email&#34;            : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;               : &#34;8237572&#34;,
    &#34;customer_type&#34;             : &#34;Web member&#34;,
    &#34;fare_class&#34;                : &#34;Class L&#34;,
    &#34;flight_route&#34;              : &#34;SAN-CUN,CUN-SAN&#34;,
    &#34;flight_sku&#34;                : [&#34;Y123&#34;,&#34;Z456&#34;],
    &#34;flight_type&#34;               : &#34;Round&#34;,
    &#34;login_status&#34;              : &#34;logged in&#34;,
    &#34;loyalty_id&#34;               : &#34;46794561&#34;,
    &#34;num_adult_passengers&#34;      : &#34;1&#34;,
    &#34;num_child_passengers&#34;      : &#34;1&#34;,
    &#34;occupancy_detail&#34;          : [&#34;3&#34;,&#34;3&#34;],
    &#34;order_cancellation_policy&#34; : [&#34;24 Hours&#34;,&#34;No Cancellation&#34;],
    &#34;order_grand_total&#34;         : &#34;54.47&#34;,
    &#34;order_id&#34;                  : &#34;132133&#34;,
    &#34;order_payment_type&#34;        : &#34;paypal&#34;,
    &#34;order_promo_code&#34;          : &#34;MEX30&#34;,
    &#34;order_store&#34;               : &#34;mobile web&#34;,
    &#34;order_subtotal&#34;            : &#34;45.98&#34;,
    &#34;order_tax_amount&#34;          : &#34;2.50&#34;,
    &#34;origin_flight_route&#34;       : [&#34;SAN-CUN&#34;],
    &#34;page_name&#34;                 : &#34;Homepage&#34;,
    &#34;page_type&#34;                 : &#34;order&#34;,
    &#34;passenger_name&#34;            : [&#34;Steve&#34;,&#34;jack&#34;],
    &#34;passenger_price&#34;           : [&#34;100.00&#34;,&#34;120.00&#34;],
    &#34;quantity&#34;                  : [&#34;2&#34;,&#34;2&#34;],
    &#34;returning_flight_route&#34;    : [&#34;CUN-SAN&#34;],
    &#34;site_section&#34;              : &#34;Loyalty&#34;,
    &#34;tealium_event&#34;             : &#34;purchase&#34;,
    &#34;total_passengers&#34;          : &#34;3&#34;,
    &#34;transactionAffiliation&#34;    : &#34;Visa&#34;,
    &#34;trip_end_date&#34;             : &#34;03/12/2017&#34;,
    &#34;trip_start_date&#34;           : &#34;03/02/2017&#34;,
    &#34;variant&#34;                   : [&#34;14F&#34;,&#34;15D&#34;,&#34;baggage&#34;,&#34;car&#34;]
}
```

### 予約管理ページ

|イベント名|説明|
|---|---|
| `page_view`| 予約管理ページ。|

サンプル:  
```javascript
{
    &#34;currency&#34;       : &#34;USD&#34;,
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;    : &#34;8237572&#34;,
    &#34;fare_class&#34;     : &#34;Class L&#34;,
    &#34;flight_type&#34;    : &#34;Round&#34;,
    &#34;login_status&#34;   : &#34;logged in&#34;,
    &#34;page_name&#34;      : &#34;Homepage&#34;,
    &#34;page_type&#34;      : &#34;manage_your_booking&#34;,
    &#34;site_section&#34;   : &#34;Loyalty&#34;,
    &#34;tealium_event&#34;  : &#34;page_view&#34;
}
```

### チェックインページ

|イベント名|説明|
|---|---|
| `page_view`| チェックインフロー。|

サンプル:  
```javascript
{
    &#34;checkout_step&#34;          : &#34;3&#34;,
    &#34;currency&#34;               : &#34;USD&#34;,
    &#34;customer_email&#34;         : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;            : &#34;8237572&#34;,
    &#34;fare_class&#34;             : &#34;Class L&#34;,
    &#34;flight_route&#34;           : &#34;SAN-CUN,CUN-SAN&#34;,
    &#34;flight_sku&#34;             : [&#34;Y123&#34;,&#34;Z456&#34;],
    &#34;flight_type&#34;            : &#34;Round&#34;,
    &#34;login_status&#34;           : &#34;logged in&#34;,
    &#34;origin_flight_route&#34;    : [&#34;SAN-CUN&#34;],
    &#34;page_name&#34;              : &#34;Homepage&#34;,
    &#34;page_type&#34;              : &#34;check_in&#34;,
    &#34;passenger_name&#34;         : [&#34;Steve&#34;,&#34;jack&#34;],
    &#34;returning_flight_route&#34; : [&#34;CUN-SAN&#34;],
    &#34;site_section&#34;           : &#34;Loyalty&#34;,
    &#34;tealium_event&#34;          : &#34;page_view&#34;,
    &#34;trip_end_date&#34;          : &#34;03/12/2017&#34;,
    &#34;trip_start_date&#34;        : &#34;03/02/2017&#34;
}
```

### アカウントページ

|イベント名|説明|
|---|---|
| `page_view`| ユーザーアカウントログイン。|

サンプル:  
```javascript
{
    &#34;checkout_step&#34;  : &#34;3&#34;,
    &#34;currency&#34;       : &#34;USD&#34;,
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;    : &#34;8237572&#34;,
    &#34;customer_type&#34;  : &#34;Web member&#34;,
    &#34;login_status&#34;   : &#34;logged in&#34;,
    &#34;loyalty_id&#34;     : &#34;46794561&#34;,
    &#34;page_name&#34;      : &#34;Homepage&#34;,
    &#34;page_type&#34;      : &#34;account&#34;,
    &#34;site_section&#34;   : &#34;Loyalty&#34;,
    &#34;tealium_event&#34;  : &#34;page_view&#34;
}
```

### ランディングページ

|イベント名|説明|
|---|---|
| `page_view`| ランディングページおよびフォームページ（団体旅行）。|

サンプル:  
```javascript
{
    &#34;currency&#34;       : &#34;USD&#34;,
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;    : &#34;8237572&#34;,
    &#34;login_status&#34;   : &#34;logged in&#34;,
    &#34;page_name&#34;      : &#34;Homepage&#34;,
    &#34;page_type&#34;      : &#34;landing&#34;,
    &#34;site_section&#34;   : &#34;Loyalty&#34;,
    &#34;tealium_event&#34;  : &#34;page_view&#34;
}
```

### 汎用ページ

|イベント名|説明|
|---|---|
| `page_view`| その他のページ。|

サンプル:  
```javascript
{
    &#34;currency&#34;       : &#34;USD&#34;,
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;    : &#34;8237572&#34;,
    &#34;login_status&#34;   : &#34;logged in&#34;,
    &#34;page_name&#34;      : &#34;Other Page&#34;,
    &#34;page_type&#34;      : &#34;content&#34;,
    &#34;site_section&#34;   : &#34;Loyalty&#34;,
    &#34;tealium_event&#34;  : &#34;page_view&#34;
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
    &#34;avg_room_rate&#34;           : [&#34;100.00&#34;],
    &#34;checkout_step&#34;           : &#34;3&#34;,
    &#34;customer_type&#34;           : &#34;Web member&#34;,
    &#34;days_to_trip_start&#34;      : &#34;20&#34;,
    &#34;ecommerce_action&#34;        : &#34;detail&#34;,
    &#34;num_adult_occupants&#34;     : &#34;3&#34;,
    &#34;num_adult_passengers&#34;    : &#34;1&#34;,
    &#34;num_child_occupants&#34;     : &#34;3&#34;,
    &#34;num_child_passengers&#34;    : &#34;1&#34;,
    &#34;num_of_nights&#34;           : &#34;4&#34;,
    &#34;num_of_rooms&#34;            : &#34;2&#34;,
    &#34;origin_flight_route&#34;     : [&#34;SAN-CUN&#34;],
    &#34;product_name&#34;            : [&#34;Seat&#34;,&#34;Room&#34;,&#34;Car&#34;],
    &#34;product_price&#34;           : [&#34;123.00&#34;,&#34;250.00&#34;,&#34;59.30&#34;],
    &#34;property_id&#34;             : [&#34;HI456767&#34;,&#34;BW123&#34;],
    &#34;property_name&#34;           : [&#34;Rest Eazy&#34;,&#34;Best Motels&#34;],
    &#34;property_postal_code&#34;    : [&#34;99999&#34;,&#34;11111&#34;],
    &#34;property_room_occupancy&#34; : [&#34;3&#34;,&#34;3&#34;],
    &#34;property_room_type&#34;      : [&#34;economy&#34;],
    &#34;property_state&#34;          : [&#34;CA&#34;,&#34;CA&#34;],
    &#34;proximity&#34;               : [&#34;20&#34;,&#34;30&#34;],
    &#34;quantity&#34;                : [&#34;2&#34;,&#34;2&#34;],
    &#34;returning_flight_route&#34;  : [&#34;CUN-SAN&#34;],
    &#34;tealium_event&#34;           : &#34;cart_add&#34;,
    &#34;total_passengers&#34;        : &#34;3&#34;,
    &#34;trip_end_date&#34;           : &#34;03/12/2017&#34;,
    &#34;trip_start_date&#34;         : &#34;03/02/2017&#34;,
    &#34;variant&#34;                 : [&#34;14F&#34;,&#34;15D&#34;,&#34;baggage&#34;,&#34;car&#34;]
}
```

### カート削除

|イベント名|説明|
|---|---|
| `cart_remove`| カートから削除するイベント。|

サンプル:  
```javascript
{
    &#34;checkout_step&#34;          : &#34;3&#34;,
    &#34;customer_type&#34;          : &#34;Web member&#34;,
    &#34;days_to_trip_start&#34;     : &#34;20&#34;,
    &#34;ecommerce_action&#34;       : &#34;detail&#34;,
    &#34;origin_flight_route&#34;    : [&#34;SAN-CUN&#34;],
    &#34;product_name&#34;           : [&#34;Seat&#34;,&#34;Room&#34;,&#34;Car&#34;],
    &#34;product_price&#34;          : [&#34;123.00&#34;,&#34;250.00&#34;,&#34;59.30&#34;],
    &#34;quantity&#34;               : [&#34;2&#34;,&#34;2&#34;],
    &#34;returning_flight_route&#34; : [&#34;CUN-SAN&#34;],
    &#34;tealium_event&#34;          : &#34;cart_remove&#34;
}
```

### ユーザーログイン

|イベント名|説明|
|---|---|
| `user_login`| ユーザーがログインに成功した際のイベント。|

サンプル:  
```javascript
{
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;    : &#34;8237572&#34;,
    &#34;login_status&#34;   : &#34;logged in&#34;,
    &#34;tealium_event&#34;  : &#34;user_login&#34;
}
```

### ユーザーログアウト

|イベント名|説明|
|---|---|
| `user_logout`| ユーザーがログアウトに成功した際のイベント。|

サンプル:  
```javascript
{
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;    : &#34;8237572&#34;,
    &#34;login_status&#34;   : &#34;logged in&#34;,
    &#34;tealium_event&#34;  : &#34;user_logout&#34;
}
```

### ユーザー登録

|イベント名|説明|
|---|---|
| `user_register`| ユーザーが登録に成功した際のイベント。|

サンプル:  
```javascript
{
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;    : &#34;8237572&#34;,
    &#34;tealium_event&#34;  : &#34;user_register&#34;
}
```

### ユーザー更新

|イベント名|説明|
|---|---|
| `user_update`| ユーザーアカウントの更新に成功した際のイベント。|

サンプル:  
```javascript
{
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;    : &#34;8237572&#34;,
    &#34;tealium_event&#34;  : &#34;user_update&#34;
}
```

### メールサインアップ

|イベント名|説明|
|---|---|
| `email_signup`| メールアップデート/ニュースレターへのサインアップに成功した際のイベント。|

サンプル:  
```javascript
{
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;tealium_event&#34;  : &#34;email_signup&#34;
}
```

### カスタムクリック

|イベント名|説明|
|---|---|
| `custom_click`| 特定のページ要素をクリックした際のイベント。|

サンプル:  
```javascript
{
    &#34;link_action&#34;   : &#34;View Image&#34;,
    &#34;link_category&#34; : &#34;Header&#34;,
    &#34;link_name&#34;     : &#34;Login&#34;,
    &#34;link_value&#34;    : &#34;10&#34;,
    &#34;tealium_event&#34; : &#34;custom_click&#34;
}
```

### 商品クリック

|イベント名|説明|
|---|---|
| `product_click`| 商品の詳細ページやクイックビューをロードするリンクをクリックした際のイベント。|

サンプル:  
```javascript
{
    &#34;ecommerce_action&#34; : &#34;detail&#34;,
    &#34;fare_class&#34;       : &#34;Class L&#34;,
    &#34;tealium_event&#34;    : &#34;product_click&#34;
}
```

### プロモクリック

|イベント名|説明|
|---|---|
| `promo_click`| プロモーションをクリックした際のイベント。|

サンプル:  
```javascript
{
    &#34;ecommerce_action&#34;        : &#34;detail&#34;,
    &#34;promo_registration_page&#34; : &#34;&#34;,
    &#34;promotion_name&#34;          : &#34;Promo One&#34;,
    &#34;tealium_event&#34;           : &#34;promo_click&#34;
}
```

### エラーメッセージ

|イベント名|説明|
|---|---|
| `error_message`| エラーを知らせるメッセージをユーザーが閲覧した際のイベント。|

サンプル:  
```javascript
{
    &#34;checkout_step&#34;          : &#34;3&#34;,
    &#34;error_mesage&#34;           : &#34;Destination City doesn&#39;t match Departure on return&#34;,
    &#34;flight_route&#34;           : &#34;SAN-CUN,CUN-SAN&#34;,
    &#34;flight_type&#34;            : &#34;Round&#34;,
    &#34;origin_flight_route&#34;    : [&#34;SAN-CUN&#34;],
    &#34;page_name&#34;              : &#34;Homepage&#34;,
    &#34;returning_flight_route&#34; : [&#34;CUN-SAN&#34;],
    &#34;tealium_event&#34;          : &#34;error_message&#34;,
    &#34;total_passengers&#34;       : &#34;3&#34;
}
```

### ビデオ

|イベント名|説明|
|---|---|
| `video`| サイト上のビデオとのインタラクションが発生した際のイベント。|

サンプル:  
```javascript
{
    &#34;tealium_event&#34;      : &#34;video&#34;,
    &#34;video_action&#34;       : &#34;play&#34;,
    &#34;video_content_type&#34; : &#34;hotel promo&#34;,
    &#34;video_name&#34;         : &#34;Stay the Night&#34;,
    &#34;video_segments&#34;     : &#34;50&#34;
}
```