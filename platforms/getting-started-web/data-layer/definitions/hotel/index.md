---
title: Hotel data layer specification
description: This article provides the data layer definition for hotels.
url: https://docs.tealium.com/platforms/getting-started-web/data-layer/definitions/hotel/
---## Data layer attributes


|Variable| Description| Example| Type|
|---| ---| ---| ---|
|`avg_room_rate`| An array of the average rate for each room in an order| `["100.25"]`| Array|
|`cancellation_id`| ID given when reservation is cancelled| `12254875`| String|
|`check_in`| User's date of arrival| `02/18/2017`| String|
|`check_out`| User's date of departure| `02/24/2017`| String|
|`check_reservation`| Captures how guests access reservation (confirmation or information)| `information`| String|
|`currency`| Currency of rate amount| `USD`| String|
|`customer_city`| Contains booker's city of residence| `San Diego`| String|
|`customer_country`| Contains booker's country of residence| `USA`| String|
|`customer_email`| Contains booker's email address| `example@example.com`| String|
|`customer_first_name`| The first name of the booker| `Tealium`| String|
|`customer_id_type`| Type of ID used to login to loyalty site email or loyalty id| `loyalty id`| String|
|`customer_last_name`| The last name of the booker| `Tealium`| String|
|`customer_postal_code`| Contains booker's postal code| `92121`| String|
|`customer_state`| Contains booker's state| `CA`| String|
|`days_till_checkin`| Number of days between today and check in date| `45`| String|
|`displayed_properties`| An array of property IDs of each and all properties listed on the Select Hotel page| `["345","4567"]`| Array|
|`displayed_rate_amount`| The displayed rate amount on the Select Room page| `150.00`| String|
|`displayed_rate_amounts`| An array of rate amounts for each and all properties listed on the Select Hotel page| `["100.25","150.00","340.00"]`| Array|
|`displayed_rate_codes`| An array of rate codes for each and all properties listed on the Select Hotel page| `["economy","economy","luxury"]`| Array|
|`displayed_room_rates`| An array of the displayed rates grouped by room type on the Select Room page| `["340.00","500.00","650.00"]`| Array|
|`displayed_room_types`| An array of the displayed room types on the Select Room page| `["2 Queen Beds","Ocean View","Ocean Front"]`| Array|
|`error_message`| Any error text displayed to user| `Room no longer available`| String|
|`favorite_property_id`| Captures property ID that is "favorited"| `123`| String|
|`filter_amenities`| An array of the selections applied| `["pool","microwave"]`| Array|
|`filter_distance`| filter distance from event| `20`| String|
|`filter_hotel_type`| An array of hotel types filtered by user| `["economy","luxury"]`| Array|
|`filter_max_rate`| captures rate that is applied| `150`| String|
|`filter_rate_change`| filter changes| `AAA to 20% Off`| String|
|`filter_ta_rating`| An array of Travel Advisor ratings filtered by user| `["3","4","5"]`| Array|
|`language_code`| Language Code| `us`| String|
|`link_category`| During click tracking events, the category of the element clicked| `Navigation`| String|
|`link_name`| During click tracking events, the name of the element clicked | `properties`| String|
|`login_status`| Is user logged in or logged out| `logged in`| String|
|`loyalty_id`| Loyalty membership number| `99568784521`| String|
|`loyalty_point_balance`| Current point balance for user's loyalty account| `1000`| String|
|`loyalty_tier`| Membership Status Level| `Silver`| String|
|`modify_stay`| Event tracking; set every time a stay is modified| `true`| String|
|`num_of_adults`| Total number of adults| `2`| String|
|`num_of_children`| Total number of children| `3`| String|
|`num_of_nights`| Total number of nights| `5`| String|
|`num_of_rooms`| Total number of rooms| `1`| String|
|`occupancy_detail`| An array of the total occupancy in each room as searched| `["4","2"]`| Array|
|`order_cancellation_policy`| An array of the cancellation policy for each room in an order| `["24hours","5days"]`| Array|
|`order_corp_id`| Corporate ID attached to an order, if any| `987646`| String|
|`order_discount_amount`| Contains the order-level discount amount| `100.00`| String|
|`order_iata`| International Air Transport Association number attached to an order (ie Travel Agent Number)| `646879`| String|
|`order_id`| Unique ID for an order, should only be populated on Order Confirmation page| `1234`| String|
|`order_payment_method`| Payment method| `visa`| String|
|`order_payment_type`| Standard revenue or points| `revenue`| String|
|`order_points_used`| An array of the total point amounts of each room in an order| `["1000","5000"]`| Array|
|`order_postal_code`| Postal code of property booked| `00267`| String|
|`order_promo_code`| Promotional code attached to an order, if any| `SALE`| String|
|`order_rate_code`| An array of the rate code booked for each room in an order| `["AAA",""]`| Array|
|`order_room_occupancy`| An array of the total occupancy in each room for an order| `["5","2"]`| Array|
|`order_room_type`| An array of rooms booked for each room in order| `["double","ocean view"]`| Array|
|`order_special_requests`| The free text entered in "Special Requests" field on Review &amp; Res page (by room)| `No Feathers`| String|
|`order_subtotal`| The total subtotal including any product or order level discounts, but excluding taxes and fees with only digits and decimal| `1000.00`| String|
|`order_tax_amount`| The total taxes and fees| `75.00`| String|
|`order_total`| The total amount of the order| `1175.00`| String|
|`order_total_occupancy`| Overall total occupancy for order at time of booking| `5`| String|
|`page_joined`| Page that guest joins loyalty - Page Name| `homepage`| String|
|`page_name`| Tealium variable to identify the page name| `homepage`| String|
|`page_type`| High Level page type such as grouping home, property, confirmation| `home`| String|
|`promo_registration_page`| Page where registration for promotion occurred| `offers`| String|
|`property_brand`| Name of the brand for the property| `["economy brand"]`| Array|
|`property_city`| City the property is located in| `["Chula Vista"]`| Array|
|`property_country`| Country the property is located in| `["USA"]`| Array|
|`property_id`| An array of the property number| `["354498765467"]`| Array|
|`property_name`| An array of the property name| `["hotel Chula Vista"]`| Array|
|`property_position`| An array of the index of the property selected| `["1"]`| Array|
|`property_postal_code`| An array of the Zip code for the property| `["92121"]`| Array|
|`property_state`| An array of the State the property is located in| `["CA"]`| Array|
|`proximity`| An array of the Distance between city center and property location in miles| `["24"]`| Array|
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
|`selected_rate_price`| An array rate price for room selected by user on Select Room page| `["100.00","150.00"]`| Array|
|`selected_rate_type`| An array rate type for room selected by user on Select Room page| `["Best Rate","loyalty","AAA"]`| Array|
|`selected_room_type`| An array room type for room selected by user on Select Room page| `["2 double beds","Ocean View"]`| Array|
|`show_available`| Setting for Show Only Available Hotels| `true`| String|
|`site`| This should be the site user is on| `economy site`| String|
|`site_section`| The high-level sections of your site| `offers`| String|
|`social_channel`| Used with event to capture when information is shared on social media| `facebook`| String|
|`sort_by`| Sort By selection (distance, low to high, high to low)| `distance`| String|
|`sort_order`| An array of the room type, rate code, rate amount and currency presented on the Select Room page| `["room type","distance"]`| Array|
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

### Select Hotel Page

|Event Name|Description|
|---|---|
| `page_view`| Select Hotel/Search Results page.|

Sample:  
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

### Select Room Page

|Event Name|Description|
|---|---|
| `page_view`| Select Room/Property Detail page.|

Sample:  
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
   "num_of_children"       : "3",     
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

### Review Reserve Page

|Event Name|Description|
|---|---|
| `page_view`| Review and Reserve page.|

Sample:  
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

### Confirmation Page

|Event Name|Description|
|---|---|
| `purchase`| Confirmation page.|


Sample:  
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
   \"loyalty_id"                : "99568784521",     
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

### Loyalty Page

|Event Name|Description|
|---|---|
|`page_view`| Loyalty Program Home page.|

Sample:  
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

### Offers Page

|Event Name|Description|
|---|---|
| `page_view`| Offers and Promotions page.|

Sample:  
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

### Hotels Destinations Page

|Event Name|Description|
|---|---|
| `page_view`| General info for hotels (non booking).|

Sample:  
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

### Reservations Page

|Event Name|Description|
|---|---|
| `page_view`| Looking up already booked reservations.|

Sample:  
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

### Generic Page

|Event Name|Description|
|---|---|
| `page_view`| All other pages.|

Sample:  
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

## Event Tracking

### Add Favorite

|Event Name|Description|
|---|---|
| `add_favorite`| Add property to your favorites list.|

Sample:  
```javascript
{
    "favorite_property_id" : "123",
    "tealium_event"        : "add_favorite"
}
```

### Button Selection

|Event Name|Description|
|---|---|
| `button_selection`| Trip advisor ratings;brands.|

Sample:  
```javascript
{
    "selected_rate_price" : ["100.00","150.00"],
    "selected_rate_type"  : ["Best Rate","loyalty","AAA"],
    "selected_room_type"  : ["2 double beds","Ocean View"],
    "tealium_event"       : "button_selection"
}
```

### Cancellation

|Event Name|Description|
|---|---|
|  `cancellation`| When users cancels reservation.|

Sample:  
```javascript
{
    "cancellation_id"           : "12254875",
    "order_cancellation_policy" : ["24hours","5days"],
    "tealium_event"             : "cancellation"
}
```

### Check Reservation

|Event Name|Description|
|---|---|
|  `check_reservation`| User checks an existing reservation.|

Sample:  
```javascript
{
    "check_reservation" : "information",
    "tealium_event"     : "check_reservation"
}
```

### Email Signup

|Event Name|Description|
|---|---|
| `email_signup`| Upon successful signup for email updates or newsletter.|

Sample:  
```javascript
{
    "customer_email" : "example@example.com",
    "tealium_event"  : "email_signup"
}
```

### Error Message

|Event Name|Description|
|---|---|
| `error_message`| An error message is displayed to the user.|

Sample:  
```javascript
{
    "error_message" : "Room no longer available",
    "tealium_event" : "error_message"
}
```

### Form Submit

|Event Name|Description|
|---|---|
| `form_submit`| User submits a form.|

Sample:  
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

### Custom Click

|Event Name|Description|
|---|---|
| `custom_click`| On click of certain page elements.|

Sample:  
```javascript
{
    "link_category" : "Navigation",
    "link_name"     : "properties",
    "tealium_event" : "custom_click"
}
```

### Map Engagement

|Event Name|Description|
|---|---|
| `map_engagement`| User interacts with map.|

Sample:  
```javascript
{
    "link_category" : "Navigation",
    "link_name"     : "properties",
    "tealium_event" : "map_engagement"
}
```

### Modify Stay

|Event Name|Description|
|---|---|
| `modify_stay`| Captures when guest modifies a stay.|

Sample:  
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

### Register Offer

|Event Name|Description|
|---|---|
| `register_offer`| Capture when a user registers for an offer or promo.|

Sample:  
```javascript
{
    "page_joined"             : "homepage",
    "promo_registration_page" : "offers",
    "registration_id"         : "example@example.com",
    "tealium_event"           : "register_offer"
}
```

### Select Dropdown

|Event Name|Description|
|---|---|
| `select_dropdown`| User changes a drop down filter on hotel search results page.|

Sample:  
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

### Select Room Position

|Event Name|Description|
|---|---|
| `select_room_position`| Capture the highest position on Select Room page where rate from Select Hotel page was displayed.|

Sample:  
```javascript
{  
  "select_room_position" : "1",     
  "tealium_event"        : "select_room_position"
}
```

### Social Click

|Event Name|Description|
|---|---|
| `social_click`| Click to share or like content.|

Sample:  
```javascript
{
    "social_channel" : "facebook",
    "tealium_event"  : "social_click"
}
```

### Sort Order

|Event Name|Description|
|---|---|
| `sort_order`| User changes the sort order on the hotel results page.|

Sample:  
```javascript
{
    "sort_by"      : "distance",
    "sort_order"   : ["roomtype","distance"],
    "tealium_event": "sort_order"
}
```

### User Login

|Event Name|Description|
|---|---|
| `user_login`| Upon successful user login.|

Sample:  
```javascript
{
    "customer_email" : "example@example.com",
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

### User Register

|Event Name|Description|
|---|---|
| `user_register`| Upon successful user registrations.|

Sample:  
```javascript
{
    "customer_email" : "example@example.com"
    "page_joined"    : "homepage",
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
    "customer_email" : "example@example.com",
    "tealium_event"  : "user_update"
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
    "video_content_type" : "Property Video",
    "video_name"         : "Video Name",
    "video_segments"     : "75"
}
```
