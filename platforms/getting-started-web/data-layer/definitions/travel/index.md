---
title: Travel data layer specification
description: This article provides the data layer definition for travel.
url: https://docs.tealium.com/platforms/getting-started-web/data-layer/definitions/travel/
---
## Data layer attributes

|Variable| Description| Example| Type|
|---| ---| ---| ---|
|`aircraft_capacity`| Seat capacity of the aircraft| `148`| String|
|`aircraft_type`| Type of aircraft| `A320`| String|
|`avg_room_rate`| An array of the average rate for each room in an order| `[&#34;100.00&#34;]`| Array|
|`cancellation_id`| ID given when reservation is cancelled| `987654654`| String|
|`checkout_step`| Specifies which step number the user is on during the checkout process| `3`| String|
|`country_code`| Country Code| `us`| String|
|`currency`| Currency type| `USD`| String|
|`customer_city`| Contains the customer&#39;s city of residence| `San Diego`| String|
|`customer_country`| Contains the customer&#39;s country of residence| `United States`| String|
|`customer_email`| Contains the customer&#39;s email address| `johnsmith@example.com`| String|
|`customer_first_name`| The first name of the primary contact| `John`| String|
|`customer_id`| Contains the unique user ID (as it is on the current page) | `8237572`| String|
|`customer_last_name`| The last name of the primary contact| `Smith`| String|
|`customer_middle_name`| Middle name of the primary contact| `Alberto`| String|
|`customer_nationality`| Specifies the nationality of the primary customer| `Mexican`| String|
|`customer_phone`| Primary Contact Phone| `123-564-7894`| String|
|`customer_postal_code`| Contains the customer&#39;s postal code| `92101`| String|
|`customer_state`| Contains the customer&#39;s state of residence| `CA`| String|
|`customer_type`| Specifies the type of customer | `Web member`| String|
|`days_to_trip_start`| Number of days between today and trip start date| `20`| String|
|`displayed_properties`| An array of property IDs of each and all properties listed when Selecting a Hotel page| `[&#34;234234&#34;,&#34;234256&#34;]`| Array|
|`displayed_rate_amount`| The displayed rate amount on the Select Room page| `100.00`| String|
|`displayed_rate_codes`| An array of rate codes for each and all properties listed on the Select Hotel page| `[&#34;AAA&#34;,&#34;Corporate&#34;]`| Array|
|`displayed_room_rates`| An array of the displayed rates grouped by room type on the Select Room page| `[&#34;100.00&#34;,&#34;75.00&#34;]`| Array|
|`displayed_room_types`| An array of the displayed room types on the Select Room page| `[&#34;2QueenBeds&#34;,&#34;studio&#34;]`| Array|
|`ecommerce_action`| Specifies the action of the e-commerce event| `detail`| String|
|`error_message`| Any error text displayed to User| `Destination City doesn&#39;t match Departure on return`| String|
|`fare_class`| Specifies the fare class| `Class L`| String|
|`favorite_property_id`| Captures property ID that is &#34;favorited&#34;| `79865`| String|
|`filter_amenities`| An array of the selections applied| [`&#34;pool&#34;,&#34;microwave&#34;]`| Array|
|`filter_distance`| filter distance from event| `20`| String|
|`filter_hotel_type`| An array of hotel types filtered by User| `[&#34;economy&#34;,&#34;luxury&#34;,&#34;brand&#34;]`| Array|
|`filter_max_rate`| captures rate that is applied| `150`| String|
|`filter_rating`| An array of ratings filtered by User, site, trip advisor, etc| `[&#34;3&#34;,&#34;4&#34;,&#34;5&#34;]`| Array|
|`flight_route`| Route| `SAN-CUN,CUN-SAN`| String|
|`flight_sku`| An array of product SKUs| `[&#34;Y123&#34;,&#34;Z456&#34;]`| Array|
|`flight_type`| Round, Single,| `Round`| String|
|`language_code`| Language Code| `en`| String|
|`link_action`| During click tracking events, the action of the element clicked| `View Image`| String|
|`link_category`| During click tracking events, the category of the element clicked| `Header`| String|
|`link_name`| During click tracking events, the name of the element clicked| `Login`| String|
|`link_value`| During click tracking events, the value of the element clicked| `10`| String|
|`login_status`| Is User logged in or logged out| `logged in`| String|
|`loyalty_id`| Loyalty ID or membership number| `46794561`| String|
|`loyalty_point_balance`| Current point balance for User&#39;s loyalty account| `10,000`| String|
|`loyalty_tier`| Membership Status Level| `Silver`| String|
|`num_adult_occupants`| Total number of adults| `3`| String|
|`num_adult_passengers`| Adults passengers on the reservation| `1`| String|
|`num_child_occupants`| Total number of children| `3`| String|
|`num_child_passengers`| Children passengers on the reservation| `1`| String|
|`num_of_nights`| Total number of nights| `4`| String|
|`num_of_rooms`| Total number of rooms| `2`| String|
|`occupancy_detail`| An array of the total occupancy in each room as searched| `[&#34;3&#34;,&#34;3&#34;]`| Array|
|`order_cancellation_policy`| An array of the cancellation policy for each room in an order| `[&#34;24 Hours&#34;,&#34;No Cancellation&#34;]`| Array|
|`order_corp_id`| Corporate ID attached to an order, if any| `32132465475`| String|
|`order_discount_amount`| Contains the order-level discount amount| `10.00`| String|
|`order_grand_total`| Total Amount of the Order including tax and shipping but less all discounts as a string with only digits and decimal| `54.47`| String|
|`order_iata`| International Air Transport Association number attached to an order (ie Travel Agent Number)| `654654`| String|
|`order_id`| Unique ID for an order, populated on Order Confirmation page| `132133`| String|
|`order_payment_type`| Contains the type of payment| `Paypal`| String|
|`order_points_used`| An array of the total point amounts of each room in an order| `2000`| String|
|`order_promo_code`| String list of comma separated promotion codes| `MEX30`| String|
|`order_rate_code`| An array of the rate code booked for each room in an order| `[&#34;AAA&#34;]`| Array|
|`order_special_requests`| The free text entered in &#34;Special Requests&#34; field on Review &amp;amp; Res page (by room)| `No Feathers`| String|
|`order_store`| ID of store type | `mobile web`| String|
|`order_subtotal`| Contains price of all items including any product or order level discounts, but excluding tax and shipping as a string with only digits and decimal| `45.98`| String|
|`order_tax_amount`| Total tax amount for this order as a string with only digits and decimal| `2.50`| String|
|`order_total_occupancy`| Overall total occupancy for order at time of booking| `6`| String|
|`origin_flight_route`| Origin Flight| `[&#34;SAN-CUN&#34;]`| Array|
|`page_name`| Tealium variable to identify the page name| `Homepage`| String|
|`page_type`| Type of page | `home`| String|
|`passenger_name`| Passenger name in an array| `[&#34;Steve&#34;,&#34;Jack&#34;]`| Array|
|`passenger_price`| Price per each passenger on the reservation| `[&#34;100.00&#34;,&#34;120.00&#34;]`| Array|
|`product_impression_category`| Specifies the category of the product in the impression (ancillaries or flight)| `[&#34;Flight&#34;]`| Array|
|`product_impression_id`| Specifies the ID of the product in the impression| `[&#34;Y1234&#34;]`| Array|
|`product_impression_name`| Specifies the name of the product in the impression| `[&#34;CUN-MEX&#34;]`| Array|
|`product_impression_position`| Specifies the position of the product in the impression| `[&#34;1&#34;]`| Array|
|`product_impression_price`| Specifies the price of the product in the impression| `[&#34;12.99&#34;]`| Array|
|`product_impression_variant`| Specifies the variant of the product| `[&#34;1A&#34;]`| Array|
|`product_name`| Product name| `[&#34;Seat&#34;,&#34;Room&#34;,&#34;Car&#34;]`| Array|
|`product_price`| Product price| `[&#34;123.00&#34;,&#34;250.00&#34;,&#34;59.30&#34;]`| Array|
|`promo_registration_page`| Page where registration for promotion occurred| `Promo`| String|
|`promotion_creative`| Specifies the creative name for the promotion| `Fall Sale`| String|
|`promotion_name`| Specifies the name of the product in the promotion| `Promo One`| String|
|`property_brand`| Name of the brand for the property| `[&#34;Rest Eazy&#34;,&#34;Best Motels&#34;]`| Array|
|`property_city`| City the property is located in| `[&#34;San Francisco&#34;,&#34;Monterey Bay&#34;]`| Array|
|`property_country`| Country the property is located in| `[&#34;San Francisco&#34;,&#34;Monterey&#34;]`| Array|
|`property_id`| An array of the property number| `[&#34;HI456767&#34;,&#34;BW123&#34;]`| Array|
|`property_name`| An array of the property name| `[&#34;Holiday Inn SF&#34;,&#34;Mont. Best Motels&#34;]`| Array|
|`property_postal_code`| An array of the Zip code for the property| `[&#34;99999&#34;,&#34;11111&#34;]`| Array|
|`property_room_occupancy`| An array of the total occupancy in each room for an order| `[&#34;3&#34;,&#34;3&#34;]`| Array|
|`property_room_type`| An array of rooms booked for each room in order| `[&#34;economy&#34;]`| Array|
|`property_state`| An array of the State the property is located in| `[&#34;CA&#34;,&#34;CA&#34;]`| Array|
|`proximity`| An array of the Distance between city center and property location in miles| `[&#34;20&#34;,&#34;30&#34;]`| Array|
|`quantity`| An array of quantities for each product| `[&#34;2&#34;,&#34;2&#34;]`| Array|
|`returning_flight_route`| Returning flight| `[&#34;CUN-SAN&#34;]`| Array|
|`search_city`| City of destination searched| `Cancun`| String|
|`search_country`| Country of destination searched| `USA`| String|
|`search_rate`| Rate selected from the Select Rate drop down menu on booking widget| `105`| String|
|`search_rate_value`| Value entered for promotion and corporate selection from the Select Rate drop down menu on booking widget| `AAA`| String|
|`search_results`| Number of flights returned by search| `42`| String|
|`search_state`| State of destination searched| `CA`| String|
|`search_type`| Type of destination as defined by Google| `airport`| String|
|`select_room_position`| Highest position on Select Room page where rate from Select Hotel page was displayed| `5`| String|
|`show_available`| Setting for Show Only Available Hotels; true or false| `true`| String|
|`site_section`| The high-level sections of your site| `Loyalty`| String|
|`social_channel`| Used with event to capture when information is shared on social media| `Facebook`| String|
|`sort_by`| Sort By selection (distance, low to high, high to low)| `distance`| String|
|`total_passengers`| Total passengers on the reservation| `3`| String|
|`transactionAffiliation`| Specifies the type of payment used to pay| `Visa`| String|
|`trip_end_date`| User&#39;s date of departure for hotel or car, arrival for airline| `03/12/2017`| String|
|`trip_start_date`| User&#39;s date of arrival for hotel or car, departure for airline| `03/02/2017`| String|
|`variant`| seat number or extras| `[&#34;14F&#34;,&#34;15D&#34;,&#34;baggage&#34;,&#34;car&#34;]`| Array|
|`video_action`| The action that is currently taking place with the video| `play`| String|
|`video_content_type`| Type of video viewed| `hotel promo`| String|
|`video_name`| Name of video viewed| `Stay the Night`| String|
|`video_segments`| Percent of video viewed| `50`| String|

## Page Tracking

### Home Page

|Event Name|Description|
|---|---|
| `page_view`| The home page.|

Sample:  
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

### Flight Page

|Event Name|Description|
|---|---|
| `page_view`| Flight Selection page.|

Sample:  
```javascript
{
    &#34;currency&#34;                    : &#34;USD&#34;,
    &#34;customer_email&#34;              : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;                 : &#34;8237572&#34;,
    &#34;days_to_trip_start&#34;          : &#34;20&#34;,
    &#34;fare_class&#34;                  : &#34;Class L&#34;,
    &#34;flight_route&#34;                : &#34;SAN-CUN,CUN-SAN&#34;,
    &#34;flight_type&#34;                 : &#34;Round&#34;,
    &#34;login_status&#34;                : &#34;logged in&#34;,
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

### Lodging Page

|Event Name|Description|
|---|---|
| `page_view`| Hotel Selection page.|

Sample:  
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

### Rental Page

|Event Name|Description|
|---|---|
| `page_view`| Rental Car Selection page.|

Sample:  
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

### Search Page

|Event Name|Description|
|---|---|
| `search`| Search results page.|

Sample:  
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

### Booking Flow Page

|Event Name|Description|
|---|---|
| `page_view`| Checkout pages.|

Sample:  
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

### Order Page

|Event Name|Description|
|---|---|
| `purchase`| Order Confirmation/Receipt/Thank You page.|

Sample:  
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
    &#34;loyalty_id&#34;                : &#34;46794561&#34;,
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


### Manage Your Booking Page

|Event Name|Description|
|---|---|
| `page_view`| Manage your booking pages.|

Sample:  
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


### Check In Page

|Event Name|Description|
|---|---|
| `page_view`| Checkin Flow.|

Sample:  
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

### Account Page

|Event Name|Description|
|---|---|
| `page_view`| User account login.|

Sample:  
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

### Landing Page

|Event Name|Description|
|---|---|
| `page_view`| Landing pages and form pages (group travel).|

Sample:  
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


### Generic Page

|Event Name|Description|
|---|---|
| `page_view`| All other pages.|

Sample:  
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

## Event Tracking

### Cart Add

|Event Name|Description|
|---|---|
| `cart_add`| Add To Cart event.|

Sample:  
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


### Cart Remove

|Event Name|Description|
|---|---|
| `cart_remove`| Remove from Cart event.|

Sample:  
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


### User Login

|Event Name|Description|
|---|---|
| `user_login`| Upon successful user login.|

Sample:  
```javascript
{
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;    : &#34;8237572&#34;,
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
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;    : &#34;8237572&#34;,
    &#34;login_status&#34;   : &#34;logged in&#34;,
    &#34;tealium_event&#34;  : &#34;user_logout&#34;
}
```


### User Register

|Event Name|Description|
|---|---|
| `user_register`| Upon successful user registrations.|

Sample:  
```javascript
{
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;    : &#34;8237572&#34;,
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
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;customer_id&#34;    : &#34;8237572&#34;,
    &#34;tealium_event&#34;  : &#34;user_update&#34;
}
```

### Email Signup

|Event Name|Description|
|---|---|
| `email_signup`| Upon successful signup for email updates/newsletter.|

Sample:  
```javascript
{
    &#34;customer_email&#34; : &#34;johnsmith@example.com&#34;,
    &#34;tealium_event&#34;  : &#34;email_signup&#34;
}
```

### Custom Click

|Event Name|Description|
|---|---|
| `custom_click`| On click of certain page elements.|

Sample:  
```javascript
{
    &#34;link_action&#34;   : &#34;View Image&#34;,
    &#34;link_category&#34; : &#34;Header&#34;,
    &#34;link_name&#34;     : &#34;Login&#34;,
    &#34;link_value&#34;    : &#34;10&#34;,
    &#34;tealium_event&#34; : &#34;custom_click&#34;
}
```

### Product Click

|Event Name|Description|
|---|---|
| `product_click`| Upon clicking a link that loads a product detail or product quick view.|

Sample:  
```javascript
{
    &#34;ecommerce_action&#34; : &#34;detail&#34;,
    &#34;fare_class&#34;       : &#34;Class L&#34;,
    &#34;tealium_event&#34;    : &#34;product_click&#34;
}
```

### Promo Click

|Event Name|Description|
|---|---|
| `promo_click`| Upon clicking on a promotion.|

Sample:  
```javascript
{
    &#34;ecommerce_action&#34;        : &#34;detail&#34;,
    &#34;promo_registration_page&#34; : &#34;&#34;,
    &#34;promotion_name&#34;          : &#34;Promo One&#34;,
    &#34;tealium_event&#34;           : &#34;promo_click&#34;
}
```

### Error Message

|Event Name|Description|
|---|---|
| `error_message`| User views a message alerting of error.|

Sample:  
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

### Video

|Event Name|Description|
|---|---|
| `video`| User interacts with video on the site.|

Sample:  
```javascript
{
    &#34;tealium_event&#34;      : &#34;video&#34;,
    &#34;video_action&#34;       : &#34;play&#34;,
    &#34;video_content_type&#34; : &#34;hotel promo&#34;,
    &#34;video_name&#34;         : &#34;Stay the Night&#34;,
    &#34;video_segments&#34;     : &#34;50&#34;
}
```
