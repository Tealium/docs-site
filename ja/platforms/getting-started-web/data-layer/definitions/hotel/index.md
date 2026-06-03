---
title: ホテルデータレイヤー仕様
description: この記事では、ホテルのデータレイヤー定義について説明します。
url: https://docs.tealium.com/ja/platforms/getting-started-web/data-layer/definitions/hotel/
---## データレイヤー属性

|変数| 説明| 例| タイプ|
|---| ---| ---| ---|
|`avg_room_rate`| 各部屋の平均料金の配列| `[&#34;100.25&#34;]`| 配列|
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
|`displayed_properties`| ホテル選択ページに表示される全ての物件のIDの配列| `[&#34;345&#34;,&#34;4567&#34;]`| 配列|
|`displayed_rate_amount`| 部屋選択ページに表示される料金| `150.00`| 文字列|
|`displayed_rate_amounts`| ホテル選択ページに表示される各物件の料金の配列| `[&#34;100.25&#34;,&#34;150.00&#34;,&#34;340.00&#34;]`| 配列|
|`displayed_rate_codes`| ホテル選択ページに表示される各物件の料金コードの配列| `[&#34;economy&#34;,&#34;economy&#34;,&#34;luxury&#34;]`| 配列|
|`displayed_room_rates`| 部屋選択ページに表示される部屋タイプごとの料金の配列| `[&#34;340.00&#34;,&#34;500.00&#34;,&#34;650.00&#34;]`| 配列|
|`displayed_room_types`| 部屋選択ページに表示される部屋タイプの配列| `[&#34;2 Queen Beds&#34;,&#34;Ocean View&#34;,&#34;Ocean Front&#34;]`| 配列|
|`error_message`| ユーザーに表示されるエラーメッセージ| `Room no longer available`| 文字列|
|`favorite_property_id`| 「お気に入り」として登録された物件ID| `123`| 文字列|
|`filter_amenities`| 適用された選択肢の配列| `[&#34;pool&#34;,&#34;microwave&#34;]`| 配列|
|`filter_distance`| イベントからのフィルター距離| `20`| 文字列|
|`filter_hotel_type`| ユーザーによってフィルターされたホテルタイプの配列| `[&#34;economy&#34;,&#34;luxury&#34;]`| 配列|
|`filter_max_rate`| 適用された料金| `150`| 文字列|
|`filter_rate_change`| フィルター変更| `AAA to 20% Off`| 文字列|
|`filter_ta_rating`| ユーザーによってフィルターされたトラベルアドバイザーの評価の配列| `[&#34;3&#34;,&#34;4&#34;,&#34;5&#34;]`| 配列|
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
|`occupancy_detail`| 検索された各部屋の総宿泊人数の配列| `[&#34;4&#34;,&#34;2&#34;]`| 配列|
|`order_cancellation_policy`| 注文ごとの各部屋のキャンセルポリシーの配列| `[&#34;24hours&#34;,&#34;5days&#34;]`| 配列|
|`order_corp_id`| 注文に添付された企業ID（ある場合）| `987646`| 文字列|
|`order_discount_amount`| 注文レベルの割引額| `100.00`| 文字列|
|`order_iata`| 注文に添付された国際航空運送協会番号（旅行代理店番号）| `646879`| 文字列|
|`order_id`| 注文の一意のID、注文確認ページでのみ入力| `1234`| 文字列|
|`order_payment_method`| 支払い方法| `visa`| 文字列|
|`order_payment_type`| 標準収入またはポイント| `revenue`| 文字列|
|`order_points_used`| 注文の各部屋の総ポイント数の配列| `[&#34;1000&#34;,&#34;5000&#34;]`| 配列|
|`order_postal_code`| 予約された物件の郵便番号| `00267`| 文字列|
|`order_promo_code`| 注文に添付されたプロモーションコード（ある場合）| `SALE`| 文字列|
|`order_rate_code`| 注文の各部屋に予約された料金コードの配列| `[&#34;AAA&#34;,&#34;&#34;]`| 配列|
|`order_room_occupancy`| 注文の各部屋の総宿泊人数の配列| `[&#34;5&#34;,&#34;2&#34;]`| 配列|
|`order_room_type`| 注文の各部屋に予約された部屋タイプの配列| `[&#34;double&#34;,&#34;ocean view&#34;]`| 配列|
|`order_special_requests`| レビュー＆予約ページの「特別リクエスト」欄に入力されたフリーテキスト（部屋ごと）| `No Feathers`| 文字列|
|`order_subtotal`| 商品または注文レベルの割引を含む総小計（税金や手数料を除く）| `1000.00`| 文字列|
|`order_tax_amount`| 総税金と手数料| `75.00`| 文字列|
|`order_total`| 注文の総額| `1175.00`| 文字列|
|`order_total_occupancy`| 予約時の注文の総宿泊人数| `5`| 文字列|
|`page_joined`| ゲストがロイヤルティに参加するページ - ページ名| `homepage`| 文字列|
|`page_name`| ページ名を識別するTealium変数| `homepage`| 文字列|
|`page_type`| ホーム、物件、確認などの高レベルページタイプ| `home`| 文字列|
|`promo_registration_page`| プロモーション登録が行われたページ| `offers`| 文字列|
|`property_brand`| 物件のブランド名| `[&#34;economy brand&#34;]`| 配列|
|`property_city`| 物件が位置する都市| `[&#34;Chula Vista&#34;]`| 配列|
|`property_country`| 物件が位置する国| `[&#34;USA&#34;]`| 配列|
|`property_id`| 物件番号の配列| `[&#34;354498765467&#34;]`| 配列|
|`property_name`| 物件名の配列| `[&#34;hotel Chula Vista&#34;]`| 配列|
|`property_position`| 選択された物件のインデックスの配列| `[&#34;1&#34;]`| 配列|
|`property_postal_code`| 物件の郵便番号の配列| `[&#34;92121&#34;]`| 配列|
|`property_state`| 物件が位置する州の配列| `[&#34;CA&#34;]`| 配列|
|`proximity`| 市中心部と物件位置の距離（マイル）の配列| `[&#34;24&#34;]`| 配列|
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
|`selected_rate_price`| 部屋選択ページでユーザーによって選択された部屋の料金の配列| `[&#34;100.00&#34;,&#34;150.00&#34;]`| 配列|
|`selected_rate_type`| 部屋選択ページでユーザーによって選択された部屋の料金タイプの配列| `[&#34;Best Rate&#34;,&#34;loyalty&#34;,&#34;AAA&#34;]`| 配列|
|`selected_room_type`| 部屋選択ページでユーザーによって選択された部屋タイプの配列| `[&#34;2 double beds&#34;,&#34;Ocean View&#34;]`| 配列|
|`show_available`| 利用可能なホテルのみを表示する構成| `true`| 文字列|
|`site`| ユーザーが使用しているサイト| `economy site`| 文字列|
|`site_section`| サイトの高レベルセクション| `offers`| 文字列|
|`social_channel`| ソーシャルメディアで情報が共有されたときに使用されるイベント | `facebook`| 文字列|
|`sort_by`| 並び替え選択（距離、低から高、高から低）| `distance`| 文字列|
|`sort_order`| 部屋のタイプ、料金コード、料金額、通貨が選択された部屋のページに表示される配列 | `[&#34;room type&#34;,&#34;distance&#34;]`| 配列|
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
   &#34;currency&#34;         : &#34;USD&#34;,     
   &#34;customer_email&#34;   : &#34;example@example.com&#34;,     
   &#34;customer_id_type&#34; : &#34;loyalty id&#34;,     
   &#34;language_code&#34;    : &#34;us&#34;,     
   &#34;loyalty_id&#34;       : &#34;99568784521&#34;,     
   &#34;page_name&#34;        : &#34;homepage&#34;,     
   &#34;page_type&#34;        : &#34;home&#34;,     
   &#34;site&#34;             : &#34;economy site&#34;,     
   &#34;site_section&#34;     : &#34;offers&#34;,     
   &#34;tealium_event&#34;    : &#34;page_view&#34;
}
```

### ホテル選択ページ

|イベント名|説明|
|---|---|
| `page_view`| ホテル選択/検索結果ページ。|

サンプル:  
```javascript
{
   &#34;check_in&#34;               : &#34;02/18/2017&#34;,     
   &#34;check_out&#34;              : &#34;02/24/2017&#34;,     
   &#34;currency&#34;               : &#34;USD&#34;,     
   &#34;customer_email&#34;         : &#34;example@example.com&#34;,     
   &#34;customer_id_type&#34;       : &#34;loyalty id&#34;,     
   &#34;days_till_checkin&#34;      : &#34;45&#34;,     
   &#34;displayed_properties&#34;   : [&#34;345&#34;,&#34;4567&#34;],     
   &#34;displayed_rate_amounts&#34; : [&#34;100.25&#34;,&#34;150.00&#34;,&#34;340.00&#34;],     
   &#34;displayed_rate_codes&#34;   : [&#34;economy&#34;,&#34;economy&#34;,&#34;luxury&#34;],     
   &#34;filter_amenities&#34;       : [&#34;pool&#34;,&#34;microwave&#34;],     
   &#34;filter_distance&#34;        : &#34;20&#34;,     
   &#34;filter_hotel_type&#34;      : [&#34;economy&#34;,&#34;luxury&#34;],     
   &#34;filter_max_rate&#34;        : &#34;150&#34;,     
   &#34;filter_rate_change&#34;     : &#34;AAA to 20% Off&#34;,     
   &#34;filter_ta_rating&#34;       : [&#34;3&#34;,&#34;4&#34;,&#34;5&#34;],     
   &#34;language_code&#34;          : &#34;us&#34;,     
   &#34;loyalty_id&#34;             : &#34;99568784521&#34;,     
   &#34;modify_stay&#34;            : &#34;true&#34;,     
   &#34;num_of_adults&#34;          : &#34;2&#34;,     
   &#34;num_of_children&#34;        : &#34;3&#34;,     
   &#34;num_of_nights&#34;          : &#34;5&#34;,     
   &#34;num_of_rooms&#34;           : &#34;1&#34;,     
   &#34;page_name&#34;              : &#34;Select Hotel&#34;,     
   &#34;page_type&#34;              : &#34;select_hotel&#34;,     
   &#34;proximity&#34;              : [&#34;24&#34;],     
   &#34;search_city&#34;            : &#34;Chula Vista&#34;,     
   &#34;search_country&#34;         : &#34;USA&#34;,     
   &#34;search_full&#34;            : &#34;Chula Vista, California, United States&#34;,     
   &#34;search_rate&#34;            : &#34;Corporate&#34;,     
   &#34;search_rate_value&#34;      : &#34;Tealium&#34;,     
   &#34;search_results&#34;         : &#34;22&#34;,     
   &#34;search_state&#34;           : &#34;WA&#34;,     
   &#34;search_type&#34;            : &#34;airport&#34;,     
   &#34;show_available&#34;         : &#34;true&#34;,     
   &#34;site&#34;                   : &#34;economy site&#34;,     
   &#34;site_section&#34;           : &#34;offers&#34;,     
   &#34;sort_by&#34;                : &#34;distance&#34;,     
   &#34;sort_order&#34;             : [&#34;roomtype&#34;,&#34;distance&#34;],     
   &#34;tealium_event&#34;          : &#34;page_view&#34;
}
```

### 部屋選択ページ

|イベント名|説明|
|---|---|
| `page_view`| 部屋選択/物件詳細ページ。|

サンプル:  
```javascript
{
   &#34;check_in&#34;              : &#34;02/18/2017&#34;,     
   &#34;check_out&#34;             : &#34;02/24/2017&#34;,     
   &#34;currency&#34;              : &#34;USD&#34;,     
   &#34;customer_email&#34;        : &#34;example@example.com&#34;,     
   &#34;customer_id_type&#34;      : &#34;loyalty id&#34;,     
   &#34;days_till_checkin&#34;     : &#34;45&#34;,     
   &#34;displayed_rate_amount&#34; : &#34;150.00&#34;,     
   &#34;displayed_room_rates&#34;  : [&#34;340.00&#34;,&#34;500.00&#34;,&#34;650.00&#34;],     
   &#34;displayed_room_types&#34;  : [&#34;2 Queen Beds&#34;,&#34;Ocean View&#34;,&#34;Ocean Front&#34;],     
   &#34;language_code&#34;         : &#34;us&#34;,     
   &#34;loyalty_id&#34;            : &#34;99568784521&#34;,     
   &#34;modify_stay&#34;           : &#34;true&#34;,     
   &#34;num_of_adults&#34;         : &#34;2&#34;,     
   &#34;num_of_children&#34;        : &#34;3&#34;,     
   &#34;num_of_nights&#34;         : &#34;5&#34;,     
   &#34;num_of_rooms&#34;          : &#34;1&#34;,     
   &#34;page_name&#34;             : &#34;Select a Room&#34;,     
   &#34;page_type&#34;             : &#34;select_room&#34;,     
   &#34;property_brand&#34;        : [&#34;economy brand&#34;],     
   &#34;property_city&#34;         : [&#34;Chula Vista&#34;],     
   &#34;property_country&#34;      : [&#34;USA&#34;],     
   &#34;property_id&#34;           : [&#34;354498765467&#34;],     
   &#34;property_name&#34;         : [&#34;hotel Chula Vista&#34;],     
   &#34;property_position&#34;     : [&#34;1&#34;],     
   &#34;property_postal_code&#34;  : [&#34;92121&#34;],     
   &#34;property_state&#34;        : [&#34;CA&#34;],     
   &#34;proximity&#34;             : [&#34;24&#34;],     
   &#34;select_room_position&#34;  : &#34;1&#34;,     
   &#34;site&#34;                  : &#34;economy site&#34;,     
   &#34;site_section&#34;          : &#34;offers&#34;,     
   &#34;social_channel&#34;        : &#34;facebook&#34;,     
   &#34;tealium_event&#34;         : &#34;page_view&#34;
 }
 ```

### 予約確認ページ

|イベント名|説明|
|---|---|
| `page_view`| 予約確認ページ。|

サンプル:  
```javascript
{    
   &#34;check_in&#34;               : &#34;02/18/2017&#34;,     
   &#34;check_out&#34;              : &#34;02/24/2017&#34;,    
    &#34;currency&#34;              : &#34;USD&#34;,     
    &#34;customer_email&#34;        : &#34;example@example.com&#34;,     
    &#34;customer_id_type&#34;      : &#34;loyalty id&#34;,     
    &#34;days_till_checkin&#34;     : &#34;45&#34;,     
    &#34;language_code&#34;         : &#34;us&#34;,     
    &#34;loyalty_id&#34;            : &#34;99568784521&#34;,     
    &#34;num_of_adults&#34;         : &#34;2&#34;,     
    &#34;num_of_children&#34;       : &#34;3&#34;,     
    &#34;num_of_nights&#34;         : &#34;5&#34;,     
    &#34;num_of_rooms&#34;          : &#34;1&#34;,     
    &#34;occupancy_detail&#34;      : [&#34;4&#34;,&#34;2&#34;],     
    &#34;order_total_occupancy&#34; : &#34;5&#34;,     
    &#34;page_name&#34;             : &#34;Review Room&#34;,     
    &#34;page_type&#34;             : &#34;review_reserve&#34;,     
    &#34;property_brand&#34;        : [&#34;economy brand&#34;],     
    &#34;property_city&#34;         : [&#34;Chula Vista&#34;],     
    &#34;property_country&#34;      : [&#34;USA&#34;],     
    &#34;property_id&#34;           : [&#34;354498765467&#34;],     
    &#34;property_name&#34;         : [&#34;hotel Chula Vista&#34;],     
    &#34;property_postal_code&#34;  : [&#34;92121&#34;],     
    &#34;property_state&#34;        : [&#34;CA&#34;],     
    &#34;proximity&#34;             : [&#34;24&#34;],     
    &#34;selected_rate_price&#34;   : [&#34;100.00&#34;,&#34;150.00&#34;],     
    &#34;selected_rate_type&#34;    : [&#34;Best Rate&#34;,&#34;loyalty&#34;,&#34;AAA&#34;],     
    &#34;selected_room_type&#34;    : [&#34;2 double beds&#34;,&#34;Ocean View&#34;],     
    &#34;site&#34;                  : &#34;economy site&#34;,     
    &#34;site_section&#34;          : &#34;offers&#34;,     
    &#34;tealium_event&#34;         : &#34;page_view&#34;
 }
 ```
### 確認ページ

|イベント名|説明|
|---|---|
| `purchase`| 確認ページ。|

サンプル:  
```javascript
{  
   &#34;avg_room_rate&#34;             : [&#34;100.25&#34;],     
   &#34;check_in&#34;                  : &#34;02/18/2017&#34;,     
   &#34;check_out&#34;                 : &#34;02/24/2017&#34;,     
   &#34;check_reservation&#34;         : &#34;information&#34;,     
   &#34;currency&#34;                  : &#34;USD&#34;,     
   &#34;customer_city&#34;             : &#34;San Diego&#34;,     
   &#34;customer_country&#34;          : &#34;USA&#34;,     
   &#34;customer_email&#34;            : &#34;example@example.com&#34;,     
   &#34;customer_first_name&#34;       : &#34;Tealium&#34;,     
   &#34;customer_id_type&#34;          : &#34;loyalty id&#34;,     
   &#34;customer_last_name&#34;        : &#34;Tealium&#34;,     
   &#34;customer_postal_code&#34;      : &#34;92121&#34;,     
   &#34;customer_state&#34;            : &#34;CA&#34;,     
   &#34;days_till_checkin&#34;         : &#34;45&#34;,     
   &#34;language_code&#34;             : &#34;us&#34;,     
   &#34;loyalty_id&#34;                : &#34;99568784521&#34;,     
   &#34;loyalty_point_balance&#34;     : &#34;1000&#34;,     
   &#34;loyalty_tier&#34;              : &#34;Silver&#34;,     
   &#34;num_of_adults&#34;             : &#34;2&#34;,     
   &#34;num_of_children&#34;           : &#34;3&#34;,     
   &#34;num_of_nights&#34;             : &#34;5&#34;,     
   &#34;num_of_rooms&#34;              : &#34;1&#34;,     
   &#34;occupancy_detail&#34;          : [&#34;4&#34;,&#34;2&#34;],     
   &#34;order_cancellation_policy&#34; : [&#34;24hours&#34;,&#34;5days&#34;],     
   &#34;order_corp_id&#34;             : &#34;987646&#34;,     
   &#34;order_discount_amount&#34;     : &#34;100.00&#34;,     
   &#34;order_iata&#34;                : &#34;646879&#34;,     
   &#34;order_id&#34;                  : &#34;1234&#34;,     
   &#34;order_payment_method&#34;      : &#34;visa&#34;,     
   &#34;order_payment_type&#34;        : &#34;revenue&#34;,    
   &#34;order_points_used&#34;         : [&#34;1000&#34;,&#34;5000&#34;],     
   &#34;order_postal_code&#34;         : &#34;00267&#34;,     
   &#34;order_promo_code&#34;          : &#34;SALE&#34;,     
   &#34;order_rate_code&#34;           : [&#34;AAA&#34;,&#34;&#34;],     
   &#34;order_room_occupancy&#34;      : [&#34;5&#34;,&#34;2&#34;],     
   &#34;order_room_type&#34;           : [&#34;double&#34;,&#34;ocean view&#34;],     
   &#34;order_special_requests&#34;    : &#34;No Feathers&#34;,     
   &#34;order_subtotal&#34;            : &#34;1000.00&#34;,     
   &#34;order_tax_amount&#34;          : &#34;75.00&#34;,     
   &#34;order_total&#34;               : &#34;1175.00&#34;,     
   &#34;order_total_occupancy&#34;     : &#34;5&#34;,     
   &#34;page_name&#34;                 : &#34;Confirmation&#34;,     
   &#34;page_type&#34;                 : &#34;confirmation&#34;,     
   &#34;property_brand&#34;            : [&#34;economy brand&#34;],     
   &#34;property_city&#34;             : [&#34;Chula Vista&#34;],     
   &#34;property_country&#34;          : [&#34;USA&#34;],     
   &#34;property_id&#34;               : [&#34;354498765467&#34;],     
   &#34;property_name&#34;             : [&#34;hotel Chula Vista&#34;],     
   &#34;property_postal_code&#34;      : [&#34;92121&#34;],     
   &#34;property_state&#34;            : [&#34;CA&#34;],     
   &#34;proximity&#34;                 : [&#34;24&#34;],     
   &#34;site&#34;                      : &#34;economy site&#34;,     
   &#34;site_section&#34;              : &#34;offers&#34;,     
   &#34;social_channel&#34;            : &#34;facebook&#34;,     
   &#34;tealium_event&#34;             : &#34;purchase&#34;
}
```

### ロイヤリティページ

|イベント名|説明|
|---|---|
|`page_view`| ロイヤリティプログラムのホームページ。|

サンプル:  
```javascript
{
    &#34;currency&#34;              : &#34;USD&#34;,
    &#34;customer_email&#34;        : &#34;example@example.com&#34;,
    &#34;customer_id_type&#34;      : &#34;loyalty id&#34;,
    &#34;language_code&#34;         : &#34;us&#34;,
    &#34;loyalty_id&#34;            : &#34;99568784521&#34;,
    &#34;loyalty_point_balance&#34; : &#34;1000&#34;,
    &#34;loyalty_tier&#34;          : &#34;Silver&#34;,
    &#34;page_name&#34;             : &#34;Loyalty Page&#34;,
    &#34;page_type&#34;             : &#34;loyalty&#34;,
    &#34;site&#34;                  : &#34;economy site&#34;,
    &#34;site_section&#34;          : &#34;offers&#34;,
    &#34;tealium_event&#34;         : &#34;page_view&#34;
}
```

### オファーページ

|イベント名|説明|
|---|---|
| `page_view`| オファーとプロモーションのページ。|

サンプル:  
```javascript
{
    &#34;currency&#34;         : &#34;USD&#34;,
    &#34;customer_email&#34;   : &#34;example@example.com&#34;,
    &#34;customer_id_type&#34; : &#34;loyalty id&#34;,
    &#34;language_code&#34;    : &#34;us&#34;,
    &#34;loyalty_id&#34;       : &#34;99568784521&#34;,
    &#34;page_name&#34;        : &#34;Offers&#34;,
    &#34;page_type&#34;        : &#34;offers&#34;,
    &#34;site&#34;             : &#34;economy site&#34;,
    &#34;site_section&#34;     : &#34;offers&#34;,
    &#34;tealium_event&#34;    : &#34;page_view&#34;
}
 ```

### ホテルの目的地ページ

|イベント名|説明|
|---|---|
| `page_view`| ホテルの一般情報（予約非対応）。|

サンプル:  
```javascript
{
    &#34;check_in&#34;               : &#34;02/18/2017&#34;,
    &#34;check_out&#34;              : &#34;02/24/2017&#34;,
    &#34;currency&#34;               : &#34;USD&#34;,
    &#34;customer_email&#34;         : &#34;example@example.com&#34;,
    &#34;customer_id_type&#34;       : &#34;loyalty id&#34;,
    &#34;days_till_checkin&#34;      : &#34;45&#34;,
    &#34;displayed_properties&#34;   : [&#34;345&#34;,&#34;4567&#34;],
    &#34;displayed_rate_amounts&#34; : [&#34;100.25&#34;,&#34;150.00&#34;,&#34;340.00&#34;],
    &#34;displayed_rate_codes&#34;   : [&#34;economy&#34;,&#34;economy&#34;,&#34;luxury&#34;],
    &#34;filter_amenities&#34;       : [&#34;pool&#34;,&#34;microwave&#34;],
    &#34;filter_distance&#34;        : &#34;20&#34;,
    &#34;filter_hotel_type&#34;      : [&#34;economy&#34;,&#34;luxury&#34;],
    &#34;filter_max_rate&#34;        : &#34;150&#34;,
    &#34;filter_rate_change&#34;     : &#34;AAA to 20% Off&#34;,
    &#34;filter_ta_rating&#34;       : [&#34;3&#34;,&#34;4&#34;,&#34;5&#34;],
    &#34;language_code&#34;          : &#34;us&#34;,
    &#34;loyalty_id&#34;             : &#34;99568784521&#34;,
    &#34;modify_stay&#34;            : &#34;true&#34;,
    &#34;num_of_adults&#34;          : &#34;2&#34;,
    &#34;num_of_children&#34;        : &#34;3&#34;,
    &#34;num_of_nights&#34;          : &#34;5&#34;,
    &#34;num_of_rooms&#34;           : &#34;1&#34;,
    &#34;page_name&#34;              : &#34;Destinations&#34;,
    &#34;page_type&#34;              : &#34;hotels_destinations&#34;,
    &#34;proximity&#34;              : [&#34;24&#34;],
    &#34;search_city&#34;            : &#34;Chula Vista&#34;,
    &#34;search_country&#34;         : &#34;USA&#34;,
    &#34;search_full&#34;            : &#34;Chula Vista, California, United States&#34;,
    &#34;search_rate&#34;            : &#34;Corporate&#34;,
    &#34;search_rate_value&#34;      : &#34;Tealium&#34;,
    &#34;search_results&#34;         : &#34;22&#34;,
    &#34;search_state&#34;           : &#34;WA&#34;,
    &#34;search_type&#34;            : &#34;airport&#34;,
    &#34;show_available&#34;         : &#34;true&#34;,
    &#34;site&#34;                   : &#34;economy site&#34;,
    &#34;site_section&#34;           : &#34;offers&#34;,
    &#34;sort_by&#34;                : &#34;distance&#34;,
    &#34;sort_order&#34;             : [&#34;roomtype&#34;,&#34;distance&#34;],
    &#34;tealium_event&#34;          : &#34;page_view&#34;
}
```

### 予約ページ

|イベント名|説明|
|---|---|
| `page_view`| すでに予約された予約を検索する。|

サンプル:  
```javascript
{
    &#34;cancellation_id&#34;   : &#34;12254875&#34;,
    &#34;check_reservation&#34; : &#34;information&#34;,
    &#34;currency&#34;          : &#34;USD&#34;,
    &#34;customer_email&#34;    : &#34;example@example.com&#34;,
    &#34;customer_id_type&#34;  : &#34;loyalty id&#34;,
    &#34;language_code&#34;     : &#34;us&#34;,
    &#34;loyalty_id&#34;        : &#34;99568784521&#34;,
    &#34;page_name&#34;         : &#34;Your Reservations&#34;,
    &#34;page_type&#34;         : &#34;reservations&#34;,
    &#34;site&#34;              : &#34;economy site&#34;,
    &#34;site_section&#34;      : &#34;offers&#34;,
    &#34;tealium_event&#34;     : &#34;page_view&#34;
}
```

### 一般ページ

|イベント名|説明|
|---|---|
| `page_view`| その他のすべてのページ。|

サンプル:  
```javascript
{
    &#34;currency&#34;         : &#34;USD&#34;,
    &#34;customer_email&#34;   : &#34;example@example.com&#34;,
    &#34;customer_id_type&#34; : &#34;loyalty id&#34;,
    &#34;language_code&#34;    : &#34;us&#34;,
    &#34;loyalty_id&#34;       : &#34;99568784521&#34;,
    &#34;page_name&#34;        : &#34;Other Page&#34;,
    &#34;page_type&#34;        : &#34;content&#34;,
    &#34;site&#34;             : &#34;economy site&#34;,
    &#34;site_section&#34;     : &#34;offers&#34;,
    &#34;tealium_event&#34;    : &#34;page_view&#34;
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
    &#34;favorite_property_id&#34; : &#34;123&#34;,
    &#34;tealium_event&#34;        : &#34;add_favorite&#34;
}
```

### ボタン選択

|イベント名|説明|
|---|---|
| `button_selection`| トリップアドバイザーの評価、ブランド。|

サンプル:  
```javascript
{
    &#34;selected_rate_price&#34; : [&#34;100.00&#34;,&#34;150.00&#34;],
    &#34;selected_rate_type&#34;  : [&#34;Best Rate&#34;,&#34;loyalty&#34;,&#34;AAA&#34;],
    &#34;selected_room_type&#34;  : [&#34;2 double beds&#34;,&#34;Ocean View&#34;],
    &#34;tealium_event&#34;       : &#34;button_selection&#34;
}
```

### キャンセル

|イベント名|説明|
|---|---|
|  `cancellation`| ユーザーが予約をキャンセルしたとき。|

サンプル:  
```javascript
{
    &#34;cancellation_id&#34;           : &#34;12254875&#34;,
    &#34;order_cancellation_policy&#34; : [&#34;24hours&#34;,&#34;5days&#34;],
    &#34;tealium_event&#34;             : &#34;cancellation&#34;
}
```

### 予約確認

|イベント名|説明|
|---|---|
|  `check_reservation`| ユーザーが既存の予約を確認する。|

サンプル:  
```javascript
{
    &#34;check_reservation&#34; : &#34;information&#34;,
    &#34;tealium_event&#34;     : &#34;check_reservation&#34;
}
```
### メール登録

|イベント名|説明|
|---|---|
| `email_signup`| メールアップデートまたはニュースレターへの登録が成功した際に発生します。|

サンプル:  
```javascript
{
    &#34;customer_email&#34; : &#34;example@example.com&#34;,
    &#34;tealium_event&#34;  : &#34;email_signup&#34;
}
```

### エラーメッセージ

|イベント名|説明|
|---|---|
| `error_message`| ユーザーにエラーメッセージが表示されます。|

サンプル:  
```javascript
{
    &#34;error_message&#34; : &#34;Room no longer available&#34;,
    &#34;tealium_event&#34; : &#34;error_message&#34;
}
```

### フォーム送信

|イベント名|説明|
|---|---|
| `form_submit`| ユーザーがフォームを送信します。|

サンプル:  
```javascript
{
    &#34;filter_amenities&#34;   : [&#34;pool&#34;,&#34;microwave&#34;],
    &#34;filter_distance&#34;    : &#34;20&#34;,
    &#34;filter_hotel_type&#34;  : [&#34;economy&#34;,&#34;luxury&#34;],
    &#34;filter_max_rate&#34;    : &#34;150&#34;,
    &#34;filter_rate_change&#34; : &#34;AAA to 20% Off&#34;,
    &#34;filter_ta_rating&#34;   : [&#34;3&#34;,&#34;4&#34;,&#34;5&#34;],
    &#34;tealium_event&#34;      : &#34;form_submit&#34;
}
```

### カスタムクリック

|イベント名|説明|
|---|---|
| `custom_click`| 特定のページ要素がクリックされた際に発生します。|

サンプル:  
```javascript
{
    &#34;link_category&#34; : &#34;Navigation&#34;,
    &#34;link_name&#34;     : &#34;properties&#34;,
    &#34;tealium_event&#34; : &#34;custom_click&#34;
}
```

### マップエンゲージメント

|イベント名|説明|
|---|---|
| `map_engagement`| ユーザーがマップと対話します。|

サンプル:  
```javascript
{
    &#34;link_category&#34; : &#34;Navigation&#34;,
    &#34;link_name&#34;     : &#34;properties&#34;,
    &#34;tealium_event&#34; : &#34;map_engagement&#34;
}
```

### 滞在変更

|イベント名|説明|
|---|---|
| `modify_stay`| ゲストが滞在を変更した際に記録されます。|

サンプル:  
```javascript
{
    &#34;modify_stay&#34;     : &#34;true&#34;,
    &#34;num_of_adults&#34;   : &#34;2&#34;,
    &#34;num_of_children&#34; : &#34;3&#34;,
    &#34;num_of_nights&#34;   : &#34;5&#34;,
    &#34;num_of_rooms&#34;    : &#34;1&#34;,
    &#34;tealium_event&#34;   : &#34;modify_stay&#34;
}
```

### オファー登録

|イベント名|説明|
|---|---|
| `register_offer`| ユーザーがオファーやプロモーションに登録する際に記録されます。|

サンプル:  
```javascript
{
    &#34;page_joined&#34;             : &#34;homepage&#34;,
    &#34;promo_registration_page&#34; : &#34;offers&#34;,
    &#34;registration_id&#34;         : &#34;example@example.com&#34;,
    &#34;tealium_event&#34;           : &#34;register_offer&#34;
}
```

### ドロップダウン選択

|イベント名|説明|
|---|---|
| `select_dropdown`| ユーザーがホテル検索結果ページのドロップダウンフィルターを変更します。|

サンプル:  
```javascript
{
    &#34;filter_amenities&#34;    : [&#34;pool&#34;,&#34;microwave&#34;],
    &#34;filter_distance&#34;     : &#34;20&#34;,
    &#34;filter_hotel_type&#34;   : [&#34;economy&#34;,&#34;luxury&#34;],
    &#34;filter_max_rate&#34;     : &#34;150&#34;,
    &#34;filter_rate_change&#34;  : &#34;AAA to 20% Off&#34;,
    &#34;filter_ta_rating&#34;    : [&#34;3&#34;,&#34;4&#34;,&#34;5&#34;],
    &#34;modify_stay&#34;         : &#34;true&#34;,
    &#34;num_of_adults&#34;       : &#34;2&#34;,
    &#34;num_of_children&#34;     : &#34;3&#34;,
    &#34;num_of_nights&#34;       : &#34;5&#34;,
    &#34;num_of_rooms&#34;        : &#34;1&#34;,
    &#34;page_name&#34;           : &#34;homepage&#34;,
    &#34;search_city&#34;         : &#34;Chula Vista&#34;,
    &#34;search_country&#34;      : &#34;USA&#34;,
    &#34;search_full&#34;         : &#34;Chula Vista, California, United States&#34;,
    &#34;search_rate&#34;         : &#34;Corporate&#34;,
    &#34;search_rate_value&#34;   : &#34;Tealium&#34;,
    &#34;search_results&#34;      : &#34;22&#34;,
    &#34;search_state&#34;        : &#34;WA&#34;,
    &#34;selected_rate_price&#34; : [&#34;100.00&#34;,&#34;150.00&#34;],
    &#34;selected_rate_type&#34;  : [&#34;Best Rate&#34;,&#34;loyalty&#34;,&#34;AAA&#34;],
    &#34;selected_room_type&#34;  : [&#34;2 double beds&#34;,&#34;Ocean View&#34;],
    &#34;tealium_event&#34;       : &#34;select_dropdown&#34;
}
```

### 部屋位置選択

|イベント名|説明|
|---|---|
| `select_room_position`| Select Roomページで、Select Hotelページから表示された料金の最高位置を記録します。|

サンプル:  
```javascript
{  
  &#34;select_room_position&#34; : &#34;1&#34;,     
  &#34;tealium_event&#34;        : &#34;select_room_position&#34;
}
```

### ソーシャルクリック

|イベント名|説明|
|---|---|
| `social_click`| コンテンツの共有やいいねをクリックします。|

サンプル:  
```javascript
{
    &#34;social_channel&#34; : &#34;facebook&#34;,
    &#34;tealium_event&#34;  : &#34;social_click&#34;
}
```

### ソート順序

|イベント名|説明|
|---|---|
| `sort_order`| ユーザーがホテルの結果ページのソート順を変更します。|

サンプル:  
```javascript
{
    &#34;sort_by&#34;      : &#34;distance&#34;,
    &#34;sort_order&#34;   : [&#34;roomtype&#34;,&#34;distance&#34;],
    &#34;tealium_event&#34;: &#34;sort_order&#34;
}
```

### ユーザーログイン

|イベント名|説明|
|---|---|
| `user_login`| ユーザーがログインに成功した際に発生します。|

サンプル:  
```javascript
{
    &#34;customer_email&#34; : &#34;example@example.com&#34;,
    &#34;login_status&#34;   : &#34;logged in&#34;,
    &#34;tealium_event&#34;  : &#34;user_login&#34;
}
```

### ユーザーログアウト

|イベント名|説明|
|---|---|
| `user_logout`| ユーザーがログアウトに成功した際に発生します。|

サンプル:  
```javascript
{
    &#34;customer_email&#34;       : &#34;example@example.com&#34;,
    &#34;customer_first_name&#34;  : &#34;Tealium&#34;,
    &#34;customer_id_type&#34;     : &#34;loyalty id&#34;,
    &#34;customer_last_name&#34;   : &#34;Tealium&#34;,
    &#34;customer_postal_code&#34; : &#34;92121&#34;,
    &#34;customer_state&#34;       : &#34;CA&#34;,
    &#34;login_status&#34;         : &#34;logged in&#34;,
    &#34;tealium_event&#34;        : &#34;user_logout&#34;
}
```

### ユーザー登録

|イベント名|説明|
|---|---|
| `user_register`| ユーザー登録が成功した際に発生します。|

サンプル:  
```javascript
{
    &#34;customer_email&#34; : &#34;example@example.com&#34;
    &#34;page_joined&#34;    : &#34;homepage&#34;,
    &#34;tealium_event&#34;  : &#34;user_register&#34;
}
```

### ユーザー更新

|イベント名|説明|
|---|---|
| `user_update`| ユーザーアカウントの更新が成功した際に発生します。|

サンプル:  
```javascript
{
    &#34;customer_email&#34; : &#34;example@example.com&#34;,
    &#34;tealium_event&#34;  : &#34;user_update&#34;
}
```

### ビデオ

|イベント名|説明|
|---|---|
| `video`| ユーザーがサイト上のビデオと対話します。|

サンプル:  
```javascript
{
    &#34;tealium_event&#34;      : &#34;video&#34;,
    &#34;video_action&#34;       : &#34;play&#34;,
    &#34;video_content_type&#34; : &#34;Property Video&#34;,
    &#34;video_name&#34;         : &#34;Video Name&#34;,
    &#34;video_segments&#34;     : &#34;75&#34;
}
```