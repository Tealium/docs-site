---
title: Hotel data layer specification
description: This article provides the data layer definition for hotels.
url: https://docs.tealium.com/platforms/getting-started-web/data-layer/definitions/hotel/
---## Data layer attributes


|Variable| Description| Example| Type|
|---| ---| ---| ---|
|`avg_room_rate`| An array of the average rate for each room in an order| `[&#34;100.25&#34;]`| Array|
|`cancellation_id`| ID given when reservation is cancelled| `12254875`| String|
|`check_in`| User&#39;s date of arrival| `02/18/2017`| String|
|`check_out`| User&#39;s date of departure| `02/24/2017`| String|
|`check_reservation`| Captures how guests access reservation (confirmation or information)| `information`| String|
|`currency`| Currency of rate amount| `USD`| String|
|`customer_city`| Contains booker&#39;s city of residence| `San Diego`| String|
|`customer_country`| Contains booker&#39;s country of residence| `USA`| String|
|`customer_email`| Contains booker&#39;s email address| `example@example.com`| String|
|`customer_first_name`| The first name of the booker| `Tealium`| String|
|`customer_id_type`| Type of ID used to login to loyalty site email or loyalty id| `loyalty id`| String|
|`customer_last_name`| The last name of the booker| `Tealium`| String|
|`customer_postal_code`| Contains booker&#39;s postal code| `92121`| String|
|`customer_state`| Contains booker&#39;s state| `CA`| String|
|`days_till_checkin`| Number of days between today and check in date| `45`| String|
|`displayed_properties`| An array of property IDs of each and all properties listed on the Select Hotel page| `[&#34;345&#34;,&#34;4567&#34;]`| Array|
|`displayed_rate_amount`| The displayed rate amount on the Select Room page| `150.00`| String|
|`displayed_rate_amounts`| An array of rate amounts for each and all properties listed on the Select Hotel page| `[&#34;100.25&#34;,&#34;150.00&#34;,&#34;340.00&#34;]`| Array|
|`displayed_rate_codes`| An array of rate codes for each and all properties listed on the Select Hotel page| `[&#34;economy&#34;,&#34;economy&#34;,&#34;luxury&#34;]`| Array|
|`displayed_room_rates`| An array of the displayed rates grouped by room type on the Select Room page| `[&#34;340.00&#34;,&#34;500.00&#34;,&#34;650.00&#34;]`| Array|
|`displayed_room_types`| An array of the displayed room types on the Select Room page| `[&#34;2 Queen Beds&#34;,&#34;Ocean View&#34;,&#34;Ocean Front&#34;]`| Array|
|`error_message`| Any error text displayed to user| `Room no longer available`| String|
|`favorite_property_id`| Captures property ID that is &#34;favorited&#34;| `123`| String|
|`filter_amenities`| An array of the selections applied| `[&#34;pool&#34;,&#34;microwave&#34;]`| Array|
|`filter_distance`| filter distance from event| `20`| String|
|`filter_hotel_type`| An array of hotel types filtered by user| `[&#34;economy&#34;,&#34;luxury&#34;]`| Array|
|`filter_max_rate`| captures rate that is applied| `150`| String|
|`filter_rate_change`| filter changes| `AAA to 20% Off`| String|
|`filter_ta_rating`| An array of Travel Advisor ratings filtered by user| `[&#34;3&#34;,&#34;4&#34;,&#34;5&#34;]`| Array|
|`language_code`| Language Code| `us`| String|
|`link_category`| During click tracking events, the category of the element clicked| `Navigation`| String|
|`link_name`| During click tracking events, the name of the element clicked | `properties`| String|
|`login_status`| Is user logged in or logged out| `logged in`| String|
|`loyalty_id`| Loyalty membership number| `99568784521`| String|
|`loyalty_point_balance`| Current point balance for user&#39;s loyalty account| `1000`| String|
|`loyalty_tier`| Membership Status Level| `Silver`| String|
|`modify_stay`| Event tracking; set every time a stay is modified| `true`| String|
|`num_of_adults`| Total number of adults| `2`| String|
|`num_of_children`| Total number of children| `3`| String|
|`num_of_nights`| Total number of nights| `5`| String|
|`num_of_rooms`| Total number of rooms| `1`| String|
|`occupancy_detail`| An array of the total occupancy in each room as searched| `[&#34;4&#34;,&#34;2&#34;]`| Array|
|`order_cancellation_policy`| An array of the cancellation policy for each room in an order| `[&#34;24hours&#34;,&#34;5days&#34;]`| Array|
|`order_corp_id`| Corporate ID attached to an order, if any| `987646`| String|
|`order_discount_amount`| Contains the order-level discount amount| `100.00`| String|
|`order_iata`| International Air Transport Association number attached to an order (ie Travel Agent Number)| `646879`| String|
|`order_id`| Unique ID for an order, should only be populated on Order Confirmation page| `1234`| String|
|`order_payment_method`| Payment method| `visa`| String|
|`order_payment_type`| Standard revenue or points| `revenue`| String|
|`order_points_used`| An array of the total point amounts of each room in an order| `[&#34;1000&#34;,&#34;5000&#34;]`| Array|
|`order_postal_code`| Postal code of property booked| `00267`| String|
|`order_promo_code`| Promotional code attached to an order, if any| `SALE`| String|
|`order_rate_code`| An array of the rate code booked for each room in an order| `[&#34;AAA&#34;,&#34;&#34;]`| Array|
|`order_room_occupancy`| An array of the total occupancy in each room for an order| `[&#34;5&#34;,&#34;2&#34;]`| Array|
|`order_room_type`| An array of rooms booked for each room in order| `[&#34;double&#34;,&#34;ocean view&#34;]`| Array|
|`order_special_requests`| The free text entered in &#34;Special Requests&#34; field on Review &amp;amp; Res page (by room)| `No Feathers`| String|
|`order_subtotal`| The total subtotal including any product or order level discounts, but excluding taxes and fees with only digits and decimal| `1000.00`| String|
|`order_tax_amount`| The total taxes and fees| `75.00`| String|
|`order_total`| The total amount of the order| `1175.00`| String|
|`order_total_occupancy`| Overall total occupancy for order at time of booking| `5`| String|
|`page_joined`| Page that guest joins loyalty - Page Name| `homepage`| String|
|`page_name`| Tealium variable to identify the page name| `homepage`| String|
|`page_type`| High Level page type such as grouping home, property, confirmation| `home`| String|
|`promo_registration_page`| Page where registration for promotion occurred| `offers`| String|
|`property_brand`| Name of the brand for the property| `[&#34;economy brand&#34;]`| Array|
|`property_city`| City the property is located in| `[&#34;Chula Vista&#34;]`| Array|
|`property_country`| Country the property is located in| `[&#34;USA&#34;]`| Array|
|`property_id`| An array of the property number| `[&#34;354498765467&#34;]`| Array|
|`property_name`| An array of the property name| `[&#34;hotel Chula Vista&#34;]`| Array|
|`property_position`| An array of the index of the property selected| `[&#34;1&#34;]`| Array|
|`property_postal_code`| An array of the Zip code for the property| `[&#34;92121&#34;]`| Array|
|`property_state`| An array of the State the property is located in| `[&#34;CA&#34;]`| Array|
|`proximity`| An array of the Distance between city center and property location in miles| `[&#34;24&#34;]`| Array|
|`registration_id`| ID entered by user to register for special offer or promo; email or loyalty ID| `example@example.com`| String|
|`search_city`| City of destination searched| `Chula Vista`| String|
|`search_country`| Country of destination searched| `USA`| String|
|`search_full`| Full description of destination searched as powered by Google| `Chula Vista, California, United States`| String|
|`search_rate`| Rate selected from the Select Rate drop down menu on booking widget| `Corporate`| String|
|`search_rate_value`| Value entered for promotion and corporate selection from the Select Rate drop down menu on booking widget| `Tealium`| String|
|`search_results`| Number of results returned by search| `22`| String|
|`search_state`| State of destination searched| `WA`| String|
|`search_type`| Type of destination such as airport, locality, national park as defined by Google| `airport`| String|
|`select_room_position`| Highest position on Select Room page where rate from Select Hotel page was displayed| `1`| String|
|`selected_rate_price`| An array rate price for room selected by user on Select Room page| `[&#34;100.00&#34;,&#34;150.00&#34;]`| Array|
|`selected_rate_type`| An array rate type for room selected by user on Select Room page| `[&#34;Best Rate&#34;,&#34;loyalty&#34;,&#34;AAA&#34;]`| Array|
|`selected_room_type`| An array room type for room selected by user on Select Room page| `[&#34;2 double beds&#34;,&#34;Ocean View&#34;]`| Array|
|`show_available`| Setting for Show Only Available Hotels| `true`| String|
|`site`| This should be the site user is on| `economy site`| String|
|`site_section`| The high-level sections of your site| `offers`| String|
|`social_channel`| Used with event to capture when information is shared on social media| `facebook`| String|
|`sort_by`| Sort By selection (distance, low to high, high to low)| `distance`| String|
|`sort_order`| An array of the room type, rate code, rate amount and currency presented on the Select Room page| `[&#34;room type&#34;,&#34;distance&#34;]`| Array|
|`video_action`| The action that is currently taking place with the video, play, playing, pause, stop, complete| `play`| String|
|`video_content_type`| Type of video viewed| `Property Video`| String|
|`video_name`| Name of video viewed| `Video Name`| String|
|`video_segments`| Percent of video viewed| `75`| String|

## Page Tracking

### Home Page

|Event Name|Description|
|---|---|
| `page_view`| Home page.|

Sample:  
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

### Select Hotel Page

|Event Name|Description|
|---|---|
| `page_view`| Select Hotel/Search Results page.|

Sample:  
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

### Select Room Page

|Event Name|Description|
|---|---|
| `page_view`| Select Room/Property Detail page.|

Sample:  
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
   &#34;num_of_children&#34;       : &#34;3&#34;,     
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

### Review Reserve Page

|Event Name|Description|
|---|---|
| `page_view`| Review and Reserve page.|

Sample:  
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

### Confirmation Page

|Event Name|Description|
|---|---|
| `purchase`| Confirmation page.|


Sample:  
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
   \&#34;loyalty_id&#34;                : &#34;99568784521&#34;,     
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

### Loyalty Page

|Event Name|Description|
|---|---|
|`page_view`| Loyalty Program Home page.|

Sample:  
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

### Offers Page

|Event Name|Description|
|---|---|
| `page_view`| Offers and Promotions page.|

Sample:  
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

### Hotels Destinations Page

|Event Name|Description|
|---|---|
| `page_view`| General info for hotels (non booking).|

Sample:  
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

### Reservations Page

|Event Name|Description|
|---|---|
| `page_view`| Looking up already booked reservations.|

Sample:  
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

### Generic Page

|Event Name|Description|
|---|---|
| `page_view`| All other pages.|

Sample:  
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

## Event Tracking

### Add Favorite

|Event Name|Description|
|---|---|
| `add_favorite`| Add property to your favorites list.|

Sample:  
```javascript
{
    &#34;favorite_property_id&#34; : &#34;123&#34;,
    &#34;tealium_event&#34;        : &#34;add_favorite&#34;
}
```

### Button Selection

|Event Name|Description|
|---|---|
| `button_selection`| Trip advisor ratings;brands.|

Sample:  
```javascript
{
    &#34;selected_rate_price&#34; : [&#34;100.00&#34;,&#34;150.00&#34;],
    &#34;selected_rate_type&#34;  : [&#34;Best Rate&#34;,&#34;loyalty&#34;,&#34;AAA&#34;],
    &#34;selected_room_type&#34;  : [&#34;2 double beds&#34;,&#34;Ocean View&#34;],
    &#34;tealium_event&#34;       : &#34;button_selection&#34;
}
```

### Cancellation

|Event Name|Description|
|---|---|
|  `cancellation`| When users cancels reservation.|

Sample:  
```javascript
{
    &#34;cancellation_id&#34;           : &#34;12254875&#34;,
    &#34;order_cancellation_policy&#34; : [&#34;24hours&#34;,&#34;5days&#34;],
    &#34;tealium_event&#34;             : &#34;cancellation&#34;
}
```

### Check Reservation

|Event Name|Description|
|---|---|
|  `check_reservation`| User checks an existing reservation.|

Sample:  
```javascript
{
    &#34;check_reservation&#34; : &#34;information&#34;,
    &#34;tealium_event&#34;     : &#34;check_reservation&#34;
}
```

### Email Signup

|Event Name|Description|
|---|---|
| `email_signup`| Upon successful signup for email updates or newsletter.|

Sample:  
```javascript
{
    &#34;customer_email&#34; : &#34;example@example.com&#34;,
    &#34;tealium_event&#34;  : &#34;email_signup&#34;
}
```

### Error Message

|Event Name|Description|
|---|---|
| `error_message`| An error message is displayed to the user.|

Sample:  
```javascript
{
    &#34;error_message&#34; : &#34;Room no longer available&#34;,
    &#34;tealium_event&#34; : &#34;error_message&#34;
}
```

### Form Submit

|Event Name|Description|
|---|---|
| `form_submit`| User submits a form.|

Sample:  
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

### Custom Click

|Event Name|Description|
|---|---|
| `custom_click`| On click of certain page elements.|

Sample:  
```javascript
{
    &#34;link_category&#34; : &#34;Navigation&#34;,
    &#34;link_name&#34;     : &#34;properties&#34;,
    &#34;tealium_event&#34; : &#34;custom_click&#34;
}
```

### Map Engagement

|Event Name|Description|
|---|---|
| `map_engagement`| User interacts with map.|

Sample:  
```javascript
{
    &#34;link_category&#34; : &#34;Navigation&#34;,
    &#34;link_name&#34;     : &#34;properties&#34;,
    &#34;tealium_event&#34; : &#34;map_engagement&#34;
}
```

### Modify Stay

|Event Name|Description|
|---|---|
| `modify_stay`| Captures when guest modifies a stay.|

Sample:  
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

### Register Offer

|Event Name|Description|
|---|---|
| `register_offer`| Capture when a user registers for an offer or promo.|

Sample:  
```javascript
{
    &#34;page_joined&#34;             : &#34;homepage&#34;,
    &#34;promo_registration_page&#34; : &#34;offers&#34;,
    &#34;registration_id&#34;         : &#34;example@example.com&#34;,
    &#34;tealium_event&#34;           : &#34;register_offer&#34;
}
```

### Select Dropdown

|Event Name|Description|
|---|---|
| `select_dropdown`| User changes a drop down filter on hotel search results page.|

Sample:  
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

### Select Room Position

|Event Name|Description|
|---|---|
| `select_room_position`| Capture the highest position on Select Room page where rate from Select Hotel page was displayed.|

Sample:  
```javascript
{  
  &#34;select_room_position&#34; : &#34;1&#34;,     
  &#34;tealium_event&#34;        : &#34;select_room_position&#34;
}
```

### Social Click

|Event Name|Description|
|---|---|
| `social_click`| Click to share or like content.|

Sample:  
```javascript
{
    &#34;social_channel&#34; : &#34;facebook&#34;,
    &#34;tealium_event&#34;  : &#34;social_click&#34;
}
```

### Sort Order

|Event Name|Description|
|---|---|
| `sort_order`| User changes the sort order on the hotel results page.|

Sample:  
```javascript
{
    &#34;sort_by&#34;      : &#34;distance&#34;,
    &#34;sort_order&#34;   : [&#34;roomtype&#34;,&#34;distance&#34;],
    &#34;tealium_event&#34;: &#34;sort_order&#34;
}
```

### User Login

|Event Name|Description|
|---|---|
| `user_login`| Upon successful user login.|

Sample:  
```javascript
{
    &#34;customer_email&#34; : &#34;example@example.com&#34;,
    &#34;login_status&#34;   : &#34;logged in&#34;,
    &#34;tealium_event&#34;  : &#34;user_login&#34;
}
```

### User Logout

|Event Name|Description|
|---|---|
| `user_logout`| Upon successful user logout.|

Sample:  
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

### User Register

|Event Name|Description|
|---|---|
| `user_register`| Upon successful user registrations.|

Sample:  
```javascript
{
    &#34;customer_email&#34; : &#34;example@example.com&#34;
    &#34;page_joined&#34;    : &#34;homepage&#34;,
    &#34;tealium_event&#34;  : &#34;user_register&#34;
}
```

### User Update

|Event Name|Description|
|---|---|
| `user_update`| Upon successful update of user account.|

Sample:  
```javascript
{
    &#34;customer_email&#34; : &#34;example@example.com&#34;,
    &#34;tealium_event&#34;  : &#34;user_update&#34;
}
```

### Video

|Event Name|Description|
|---|---|
| `video`| User interacts with video on the site.|

Sample:  
```javascript
{
    &#34;tealium_event&#34;      : &#34;video&#34;,
    &#34;video_action&#34;       : &#34;play&#34;,
    &#34;video_content_type&#34; : &#34;Property Video&#34;,
    &#34;video_name&#34;         : &#34;Video Name&#34;,
    &#34;video_segments&#34;     : &#34;75&#34;
}
```
