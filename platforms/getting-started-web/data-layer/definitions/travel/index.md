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
|`avg_room_rate`| An array of the average rate for each room in an order| `["100.00"]`| Array|
|`cancellation_id`| ID given when reservation is cancelled| `987654654`| String|
|`checkout_step`| Specifies which step number the user is on during the checkout process| `3`| String|
|`country_code`| Country Code| `us`| String|
|`currency`| Currency type| `USD`| String|
|`customer_city`| Contains the customer's city of residence| `San Diego`| String|
|`customer_country`| Contains the customer's country of residence| `United States`| String|
|`customer_email`| Contains the customer's email address| `johnsmith@example.com`| String|
|`customer_first_name`| The first name of the primary contact| `John`| String|
|`customer_id`| Contains the unique user ID (as it is on the current page) | `8237572`| String|
|`customer_last_name`| The last name of the primary contact| `Smith`| String|
|`customer_middle_name`| Middle name of the primary contact| `Alberto`| String|
|`customer_nationality`| Specifies the nationality of the primary customer| `Mexican`| String|
|`customer_phone`| Primary Contact Phone| `123-564-7894`| String|
|`customer_postal_code`| Contains the customer's postal code| `92101`| String|
|`customer_state`| Contains the customer's state of residence| `CA`| String|
|`customer_type`| Specifies the type of customer | `Web member`| String|
|`days_to_trip_start`| Number of days between today and trip start date| `20`| String|
|`displayed_properties`| An array of property IDs of each and all properties listed when Selecting a Hotel page| `["234234","234256"]`| Array|
|`displayed_rate_amount`| The displayed rate amount on the Select Room page| `100.00`| String|
|`displayed_rate_codes`| An array of rate codes for each and all properties listed on the Select Hotel page| `["AAA","Corporate"]`| Array|
|`displayed_room_rates`| An array of the displayed rates grouped by room type on the Select Room page| `["100.00","75.00"]`| Array|
|`displayed_room_types`| An array of the displayed room types on the Select Room page| `["2QueenBeds","studio"]`| Array|
|`ecommerce_action`| Specifies the action of the e-commerce event| `detail`| String|
|`error_message`| Any error text displayed to User| `Destination City doesn't match Departure on return`| String|
|`fare_class`| Specifies the fare class| `Class L`| String|
|`favorite_property_id`| Captures property ID that is "favorited"| `79865`| String|
|`filter_amenities`| An array of the selections applied| [`"pool","microwave"]`| Array|
|`filter_distance`| filter distance from event| `20`| String|
|`filter_hotel_type`| An array of hotel types filtered by User| `["economy","luxury","brand"]`| Array|
|`filter_max_rate`| captures rate that is applied| `150`| String|
|`filter_rating`| An array of ratings filtered by User, site, trip advisor, etc| `["3","4","5"]`| Array|
|`flight_route`| Route| `SAN-CUN,CUN-SAN`| String|
|`flight_sku`| An array of product SKUs| `["Y123","Z456"]`| Array|
|`flight_type`| Round, Single,| `Round`| String|
|`language_code`| Language Code| `en`| String|
|`link_action`| During click tracking events, the action of the element clicked| `View Image`| String|
|`link_category`| During click tracking events, the category of the element clicked| `Header`| String|
|`link_name`| During click tracking events, the name of the element clicked| `Login`| String|
|`link_value`| During click tracking events, the value of the element clicked| `10`| String|
|`login_status`| Is User logged in or logged out| `logged in`| String|
|`loyalty_id`| Loyalty ID or membership number| `46794561`| String|
|`loyalty_point_balance`| Current point balance for User's loyalty account| `10,000`| String|
|`loyalty_tier`| Membership Status Level| `Silver`| String|
|`num_adult_occupants`| Total number of adults| `3`| String|
|`num_adult_passengers`| Adults passengers on the reservation| `1`| String|
|`num_child_occupants`| Total number of children| `3`| String|
|`num_child_passengers`| Children passengers on the reservation| `1`| String|
|`num_of_nights`| Total number of nights| `4`| String|
|`num_of_rooms`| Total number of rooms| `2`| String|
|`occupancy_detail`| An array of the total occupancy in each room as searched| `["3","3"]`| Array|
|`order_cancellation_policy`| An array of the cancellation policy for each room in an order| `["24 Hours","No Cancellation"]`| Array|
|`order_corp_id`| Corporate ID attached to an order, if any| `32132465475`| String|
|`order_discount_amount`| Contains the order-level discount amount| `10.00`| String|
|`order_grand_total`| Total Amount of the Order including tax and shipping but less all discounts as a string with only digits and decimal| `54.47`| String|
|`order_iata`| International Air Transport Association number attached to an order (ie Travel Agent Number)| `654654`| String|
|`order_id`| Unique ID for an order, populated on Order Confirmation page| `132133`| String|
|`order_payment_type`| Contains the type of payment| `Paypal`| String|
|`order_points_used`| An array of the total point amounts of each room in an order| `2000`| String|
|`order_promo_code`| String list of comma separated promotion codes| `MEX30`| String|
|`order_rate_code`| An array of the rate code booked for each room in an order| `["AAA"]`| Array|
|`order_special_requests`| The free text entered in "Special Requests" field on Review &amp; Res page (by room)| `No Feathers`| String|
|`order_store`| ID of store type | `mobile web`| String|
|`order_subtotal`| Contains price of all items including any product or order level discounts, but excluding tax and shipping as a string with only digits and decimal| `45.98`| String|
|`order_tax_amount`| Total tax amount for this order as a string with only digits and decimal| `2.50`| String|
|`order_total_occupancy`| Overall total occupancy for order at time of booking| `6`| String|
|`origin_flight_route`| Origin Flight| `["SAN-CUN"]`| Array|
|`page_name`| Tealium variable to identify the page name| `Homepage`| String|
|`page_type`| Type of page | `home`| String|
|`passenger_name`| Passenger name in an array| `["Steve","Jack"]`| Array|
|`passenger_price`| Price per each passenger on the reservation| `["100.00","120.00"]`| Array|
|`product_impression_category`| Specifies the category of the product in the impression (ancillaries or flight)| `["Flight"]`| Array|
|`product_impression_id`| Specifies the ID of the product in the impression| `["Y1234"]`| Array|
|`product_impression_name`| Specifies the name of the product in the impression| `["CUN-MEX"]`| Array|
|`product_impression_position`| Specifies the position of the product in the impression| `["1"]`| Array|
|`product_impression_price`| Specifies the price of the product in the impression| `["12.99"]`| Array|
|`product_impression_variant`| Specifies the variant of the product| `["1A"]`| Array|
|`product_name`| Product name| `["Seat","Room","Car"]`| Array|
|`product_price`| Product price| `["123.00","250.00","59.30"]`| Array|
|`promo_registration_page`| Page where registration for promotion occurred| `Promo`| String|
|`promotion_creative`| Specifies the creative name for the promotion| `Fall Sale`| String|
|`promotion_name`| Specifies the name of the product in the promotion| `Promo One`| String|
|`property_brand`| Name of the brand for the property| `["Rest Eazy","Best Motels"]`| Array|
|`property_city`| City the property is located in| `["San Francisco","Monterey Bay"]`| Array|
|`property_country`| Country the property is located in| `["San Francisco","Monterey"]`| Array|
|`property_id`| An array of the property number| `["HI456767","BW123"]`| Array|
|`property_name`| An array of the property name| `["Holiday Inn SF","Mont. Best Motels"]`| Array|
|`property_postal_code`| An array of the Zip code for the property| `["99999","11111"]`| Array|
|`property_room_occupancy`| An array of the total occupancy in each room for an order| `["3","3"]`| Array|
|`property_room_type`| An array of rooms booked for each room in order| `["economy"]`| Array|
|`property_state`| An array of the State the property is located in| `["CA","CA"]`| Array|
|`proximity`| An array of the Distance between city center and property location in miles| `["20","30"]`| Array|
|`quantity`| An array of quantities for each product| `["2","2"]`| Array|
|`returning_flight_route`| Returning flight| `["CUN-SAN"]`| Array|
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
|`trip_end_date`| User's date of departure for hotel or car, arrival for airline| `03/12/2017`| String|
|`trip_start_date`| User's date of arrival for hotel or car, departure for airline| `03/02/2017`| String|
|`variant`| seat number or extras| `["14F","15D","baggage","car"]`| Array|
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

### Flight Page

|Event Name|Description|
|---|---|
| `page_view`| Flight Selection page.|

Sample:  
```javascript
{
    "currency"                    : "USD",
    "customer_email"              : "johnsmith@example.com",
    "customer_id"                 : "8237572",
    "days_to_trip_start"          : "20",
    "fare_class"                  : "Class L",
    "flight_route"                : "SAN-CUN,CUN-SAN",
    "flight_type"                 : "Round",
    "login_status"                : "logged in",
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

### Lodging Page

|Event Name|Description|
|---|---|
| `page_view`| Hotel Selection page.|

Sample:  
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

### Rental Page

|Event Name|Description|
|---|---|
| `page_view`| Rental Car Selection page.|

Sample:  
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

### Search Page

|Event Name|Description|
|---|---|
| `search`| Search results page.|

Sample:  
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

### Booking Flow Page

|Event Name|Description|
|---|---|
| `page_view`| Checkout pages.|

Sample:  
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

### Order Page

|Event Name|Description|
|---|---|
| `purchase`| Order Confirmation/Receipt/Thank You page.|

Sample:  
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
    "loyalty_id"                : "46794561",
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


### Manage Your Booking Page

|Event Name|Description|
|---|---|
| `page_view`| Manage your booking pages.|

Sample:  
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


### Check In Page

|Event Name|Description|
|---|---|
| `page_view`| Checkin Flow.|

Sample:  
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

### Account Page

|Event Name|Description|
|---|---|
| `page_view`| User account login.|

Sample:  
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

### Landing Page

|Event Name|Description|
|---|---|
| `page_view`| Landing pages and form pages (group travel).|

Sample:  
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


### Generic Page

|Event Name|Description|
|---|---|
| `page_view`| All other pages.|

Sample:  
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

## Event Tracking

### Cart Add

|Event Name|Description|
|---|---|
| `cart_add`| Add To Cart event.|

Sample:  
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


### Cart Remove

|Event Name|Description|
|---|---|
| `cart_remove`| Remove from Cart event.|

Sample:  
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


### User Login

|Event Name|Description|
|---|---|
| `user_login`| Upon successful user login.|

Sample:  
```javascript
{
    "customer_email" : "johnsmith@example.com",
    "customer_id"    : "8237572",
    "login_status"   : "logged in",
    "tealium_event"  : "user_login"
}
```


### User Logout

|Event Name|Description|
|---|---|
| `user_logout`| Upon successful user logout.|

Sample:  
```javascript
{
    "customer_email" : "johnsmith@example.com",
    "customer_id"    : "8237572",
    "login_status"   : "logged in",
    "tealium_event"  : "user_logout"
}
```


### User Register

|Event Name|Description|
|---|---|
| `user_register`| Upon successful user registrations.|

Sample:  
```javascript
{
    "customer_email" : "johnsmith@example.com",
    "customer_id"    : "8237572",
    "tealium_event"  : "user_register"
}
```


### User Update

|Event Name|Description|
|---|---|
| `user_update`| Upon successful update of user account.|

Sample:  
```javascript
{
    "customer_email" : "johnsmith@example.com",
    "customer_id"    : "8237572",
    "tealium_event"  : "user_update"
}
```

### Email Signup

|Event Name|Description|
|---|---|
| `email_signup`| Upon successful signup for email updates/newsletter.|

Sample:  
```javascript
{
    "customer_email" : "johnsmith@example.com",
    "tealium_event"  : "email_signup"
}
```

### Custom Click

|Event Name|Description|
|---|---|
| `custom_click`| On click of certain page elements.|

Sample:  
```javascript
{
    "link_action"   : "View Image",
    "link_category" : "Header",
    "link_name"     : "Login",
    "link_value"    : "10",
    "tealium_event" : "custom_click"
}
```

### Product Click

|Event Name|Description|
|---|---|
| `product_click`| Upon clicking a link that loads a product detail or product quick view.|

Sample:  
```javascript
{
    "ecommerce_action" : "detail",
    "fare_class"       : "Class L",
    "tealium_event"    : "product_click"
}
```

### Promo Click

|Event Name|Description|
|---|---|
| `promo_click`| Upon clicking on a promotion.|

Sample:  
```javascript
{
    "ecommerce_action"        : "detail",
    "promo_registration_page" : "",
    "promotion_name"          : "Promo One",
    "tealium_event"           : "promo_click"
}
```

### Error Message

|Event Name|Description|
|---|---|
| `error_message`| User views a message alerting of error.|

Sample:  
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

### Video

|Event Name|Description|
|---|---|
| `video`| User interacts with video on the site.|

Sample:  
```javascript
{
    "tealium_event"      : "video",
    "video_action"       : "play",
    "video_content_type" : "hotel promo",
    "video_name"         : "Stay the Night",
    "video_segments"     : "50"
}
```
