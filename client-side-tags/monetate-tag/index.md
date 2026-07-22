---
title: Monetate Tag Setup Guide
description: This article describes how to configure the Monetate tag in your iQ Tag Management (TiQ) account.
url: https://docs.tealium.com/client-side-tags/monetate-tag/
---
## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

After adding the tag, configure the below settings:

* **Library loaded on page**: Set to True if you will be loading Monetate on your page instead of through Tealium
* **Monetate HTTPS URL**: The URL provided to you by Monetate in your tracking code snippet
* **Use addCartRows on all pages**: Allow the cart data to be sent with all page types automatically

## Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag on your site.

Recommended Load Rule: **All Pages**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The destination variables for the Monetate tag are built into its **Data Mapping** tab. Available categories are:

### Standard

| **Destination Name**                | **Description**                                                                                                                                                                                             |
|:------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Monetate HTTPS URL (`base_url`)     | The URL provided to you by Monetate in your tracking code snippet                                                                                                                                           |
| Page Type (`page_type`)             | Used to identify the page the user is viewing. Used in `setPageType` method whenever populated. Use to override the default Page Types                                                                      |
| Breadcrumbs (`breadcrumbs`)         | An ordered array representing the breadcrumb trail for a user's navigation. Used in the `addBreadcrumbs` method whenever populated. Sent with all Page Types                                                |
| Custom Variable (`variable.custom`) | Used with `setCustomVariables` to set a custom variable. Map to the variable containing the  value you want and replace `custom` in the mapping name with the name of your variable. Sent with all Page Types |

### E-Commerce

Since the Monetate tag is e-commerce enabled, it will automatically use the default E-Commerce Extension mappings. Manually mapping in this category is generally not needed unless:

* You want to override any extension mappings
* An e-commerce variable you want is not offered in the extension

| **Destination Name**                    | **Description**                                                                                                                                                                                                                                                                                  |
|:----------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Custom Order Data (`orderData.custom`)  | A custom item of order data for the current page or transaction. Map to the variable containing the value you want and replace `custom` in the mapping name with the name of your variable in format `_CUSTOM`. Sent with all events, use Event Parameters to set properties for specific events. |
| Order Discount (`order_discount`)       | The order discount for the current page or transaction.                                                                                                                                                                                                                                          |
| Order ID (`order_id`)                   | The unique order Id for the current transaction. Use this to override the default e-commerce value `_corder`                                                                                                                                                                                     |
| Sub Total (`order_subtotal`)            | The order subtotal for the current page or transaction. Use this to override the default e-commerce value `_csubtotal`                                                                                                                                                                           |
| Shipping Amount (`order_shipping`)      | The order shipping for the current page or transaction. Use this to override the default e-commerce value `_cship`                                                                                                                                                                               |
| Tax Amount (`order_tax`)                | The order tax for the current page or transaction. Use this to override the default e-commerce value `_ctax`                                                                                                                                                                                     |
| Currency (`order_currency`)             | The order currency for the current page or transaction. Use this to override the default e-commerce value `_ccurrency`                                                                                                                                                                           |
| List of Product IDs (`product_id`)      | A list of product IDs for the current page or transaction. Use this to override the default e-commerce value `_cprod`                                                                                                                                                                            |
| List of SKUs (`product_sku`)            | A list of product SKUs for the current page or transaction. Use this to override the default e-commerce value `_csku`                                                                                                                                                                            |
| List of Categories (`product_category`) | A list of product categories. Used in the `addCategories` method whenever populated. Use this to override the default e-commerce value `_ccat`                                                                                                                                                   |
| List of Quantities (`product_quantity`) | A list of product quantities for the current page or transaction. Use this to override the default e-commerce value `_cquan`                                                                                                                                                                     |
| List of Prices (`product_unit_price`)   | A list of product prices for the current page or transaction. Use this to override the default e-commerce value `_cprice`                                                                                                                                                                        |

### Non-Monetary Conversion

| **Destination Name**                                | **Description**                                                                                        |
|:----------------------------------------------------|:-------------------------------------------------------------------------------------------------------|
| List of Conversion IDs (conversion_id)              | Used with `addConversionRows` to set the itemId property associated with a non-monetary conversion.    |
| List of Conversion Quantities (conversion_quantity) | Used with `addConversionRows` to set the quantity property associated with a non-monetary conversion.  |
| List of Conversion Prices (conversion_unit_price)   | Used with `addConversionRows` to set the unitPrice property associated with a non-monetary conversion. |

### Page Types

Map to these destinations for triggering specific page type events on a page. To trigger an event:

1. Select a page type from the dropdown list. You may also send a Custom Page Event from the dropdown list. For a Custom Page Event, enter a name with which to identify it.
1. In the **Trigger** field, enter the value of the variable being mapped.
1. To map more events, click the **+** button and repeat steps #1 and #2.
1. Click **Apply**.

The page type event triggers when the supplied value is found in the data layer.

| **Destination Name**                        | **Description**                                                                                                                                                                                |
|:--------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Home Page View (`home`)                     | This is generally the first page that a site visitor lands on when navigating your website.                                                                                                    |
| Login Page View (`login`)                   | Login pages appear when a site visitor clicks **Log In**, **My Account**, or **Sign up** somewhere on your site other than during the checkout process.                                        |
| Category Page View (`category`)             | This page usually provides thumbnail images or links that drive your site visitors to specific index pages.                                                                                    |
| Checkout Page View (`checkout`)             | Checkout is the page that is presented to a site visitor right before they place an order.                                                                                                     |
| Product Index Page View (`product_index`)   | These pages generally display a thumbnail view of products, their description, and their price.                                                                                                |
| Search (`search`)                           | This page usually provides thumbnail images or links that relate to your site visitors specific request.                                                                                       |
| Product Detail Page View (`product_detail`) | This is a page that you navigate to from an index page when you click on a product image or link. It display specific product information in detail and lets you add an item to the cart. |
| Cart (`cart`)                               | This is the page that displays all products that a site visitor is ready to purchase.                                                                                                          |
| Purchase (`purchase`)                       | Purchase is the page displayed to your customer after completing an order.                                                                                                                     |
| Custom Page Event                           | Provides a way to indicate that something important has happened on your site. Event name will be sent to Monetate as the event key                                                            |

### Travel Events

Map to these destinations for triggering specific events on a page. To trigger an event:

1. Select an event from the dropdown list. You may choose from the predefined list or create a 'Custom' event. For a 'Custom' event, enter a name with which to identify it. Please consult with your BloomReach representative before configuring any custom parameters or events.
1. In the **Trigger** field, enter the value of the variable being mapped.
1. To map more events, click the **+** button and repeat steps #1 and #2.
1. Click **Apply**.

The event triggers when the supplied value is found in the data layer.

| **Destination Name**              | **Description**                                                                              |
|:----------------------------------|:---------------------------------------------------------------------------------------------|
| Cruise Search (`cruise_search`)   | Passes information from your site to Monetate when a user searches for a cruise              |
| Cruise Review (`cruise_review`)   | Passes information from your site to Monetate when a user adds a cruise to the cart          |
| Cruise Booking (`cruise_booking`) | Passes information from your site to Monetate when a user completes the purchase of a cruise |
| Hotel Search (`hotel_search`)     | Passes information from your site to Monetate when a user searches for a hotel               |
| Hotel Review (`hotel_review`)     | Passes information from your site to Monetate when a user adds a hotel to the cart           |
| Hotel Booking (`hotel_booking`)   | Passes information from your site to Monetate when a user completes the purchase of a hotel  |
| Flight Search (`flight_search`)   | Passes information from your site to Monetate when a user searches for a flight              |
| Flight Review (`flight_review`)   | Passes information from your site to Monetate when a user adds a flight to the cart          |
| Flight Booking (`flight_booking`) | Passes information from your site to Monetate when a user completes the purchase of a flight |

### Page Type Parameters

Map to these destinations if you want to pass additional or override data with the page type(s) you mapped earlier.

To pass a parameter with a pre-defined event:

1. Event: Select a Monetate page type from the dropdown list.
1. Parameter: Select a Monetate parameter from the dropdown list.
1. For a Custom parameter, enter a name with which to identify it after the default content.
1. Click **+Add**.

| **Destination Name**          | **Description**                                                                                                                                                                                                                                       |
|:------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Page Type                     | Used to identify the page the user is viewing. Use to override the default Page Types. Specific to the selected page type(s)                                                                                                                          |
| Breadcrumbs                   | An ordered array representing the breadcrumb trail for a user's navigation. Used in the `addBreadcrumbs` method whenever populated. Specific to the selected page type(s)                                                                             |
| Custom Variable               | Used with `setCustomVariables` to set a custom variable. Map to the variable containing the value you want and enter a name with which to identify it after the default content. Specific to the selected page type(s)                                 |
| Custom Order Data             | A custom item of order data for the current page or transaction. Map to the variable containing the value you want and enter a name with which to identify it after the default content in format `_CUSTOM`. Specific to the selected page type(s) |
| Order ID                      | The unique order Id for the current transaction. Specific to the selected page type(s)                                                                                                                                                                |
| Shipping Amount               | The order shipping for the current page or transaction. Specific to the selected page type(s)                                                                                                                                                         |
| Tax Amount                    | The order tax for the current page or transaction. Specific to the selected page type(s)                                                                                                                                                              |
| Currency                      | The order currency for the current page or transaction. Specific to the selected page type(s)                                                                                                                                                         |
| Order Discount                | The order discount for the current page or transaction. Specific to the selected page type(s)                                                                                                                                                         |
| List of Product IDs           | A list of product IDs for the current page or transaction. Specific to the selected page type(s)                                                                                                                                                      |
| List of SKUs                  | A list of product SKUs for the current page or transaction. Specific to the selected page type(s)                                                                                                                                                     |
| List of Categories            | A list of product categories. Specific to the selected page type(s)                                                                                                                                                                                   |
| List of Quantities            | A list of product quantities for the current page or transaction. Specific to the selected page type(s)                                                                                                                                               |
| List of Prices                | A list of product prices for the current page or transaction. Specific to the selected page type(s)                                                                                                                                                   |
| List of Conversion IDs        | Used with `addConversionRows` to set the itemId property associated with a non-monetary conversion. Specific to the selected page type(s)                                                                                                             |
| List of Conversion Quantities | Used with `addConversionRows` to set the quantity property associated with a non-monetary conversion. Specific to the selected page type(s)                                                                                                           |
| List of Conversion Prices     | Used with `addConversionRows` to set the unitPrice property associated with a non-monetary conversion. Specific to the selected page type(s)                                                                                                          |

### Event Parameters

Map to these destinations if you want to pass additional or override data with the event(s) you mapped earlier.

To pass a parameter with a pre-defined event:

1. Event: Select a Monetate Travel event from the dropdown list.
1. Parameter: Select a Monetate Travel parameter from the dropdown list.
1. Click **+Add**.

| **Destination Name**    | **Description**                                                                                                                                            |
|:------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cruise Identifier       | A string without spaces that includes an internal ID used to identify a cruise. Specific to the selected event(s)                                          |
| Cruise Quantity         | An integer that includes the number of cruises booked. This is typically `1`. Specific to the selected event(s)                                            |
| Cruise Price            | A string that includes the price of the cruise in the format `XX.XX`. Specific to the selected event(s)                                                    |
| Cruise Booking Currency | A string in ISO 4217 format (three capital letters and no spaces) that includes the currency used to book the cruise. Specific to the selected event(s)     |
| Cruise Purchase ID      | A string that includes the order ID for a purchased cruise. Specific to the selected event(s)                                                              |
| Cruise Start Date       | A string that includes the start date of the cruise in `YYYYMMDD` format. Specific to the selected event(s)                                                |
| Cruise End Date         | A string that includes the end date of the cruise in `YYYYMMDD` format. Specific to the selected event(s)                                                  |
| Cruise Adult Passengers | An integer that includes the total number of adult passengers for the cruise. Specific to the selected event(s)                                            |
| Cruise Total Passengers | An integer that includes the total number of guests for the cruise (adults + children). Specific to the selected event(s)                                  |
| Cruise Duration         | An integer that includes the duration of cruise in days. Specific to the selected event(s)                                                                 |
| Cruise Departure Port   | A string that includes the port of departure for the cruise. Specific to the selected event(s)                                                             |
| Cruise Destination Port | A string that includes the port of destination for the cruise. Specific to the selected event(s)                                                           |
| Cruise Ship Name        | A string that includes the name of the cruise ship. Specific to the selected event(s)                                                                      |
| Cruise Room Class       | A string that includes the type of room selected for the cruise. Specific to the selected event(s)                                                         |
| Cruise Room Number      | A string or integer that includes the room number selected for the cruise. Specific to the selected event(s)                                               |
| Cruise Child Passengers | An integer that includes the total number of child passengers for the cruise. Specific to the selected event(s)                                            |
| Hotel Identifier        | A string without spaces that includes an internal ID used to identify a hotel. Specific to the selected event(s)                                           |
| Hotel Room Quantity     | An integer that includes the number of hotel rooms booked. Specific to the selected event(s)                                                               |
| Hotel Room Price        | A string that includes the price of the hotel in the format `XX.XX`. Specific to the selected event(s)                                                     |
| Hotel Booking Currency  | A string in ISO 4217 format (three capital letters and no spaces) that includes the currency used to book the hotel. Specific to the selected event(s)       |
| Hotel Purchase ID       | A string that includes the order ID for a purchased hotel. Specific to the selected event(s)                                                               |
| Hotel Check-in Date     | A string that includes the check-in date for the hotel stay in `YYYYMMDD` format. Specific to the selected event(s)                                        |
| Hotel Check-out Date    | A string that includes the check-out date for the hotel stay in `YYYYMMDD` format. Specific to the selected event(s)                                       |
| Hotel Total Guests      | An integer that includes the total number of guests staying in a hotel room (adults + children). Specific to the selected event(s)                         |
| Hotel City              | A string that includes the city where a hotel was searched for. Specific to the selected event(s)                                                          |
| Hotel Country           | A string that includes the country where a hotel was searched for. Specific to the selected event(s)                                                       |
| Number of Hotel Rooms   | An integer that includes the total number of hotel rooms searched for. Specific to the selected event(s)                                                   |
| Hotel Airport Code      | A string that includes the three character airport code to search for adjacent airports. Specific to the selected event(s)                                 |
| Hotel Airport Code City | A string that includes the adjacent city for the airport included in airport. Specific to the selected event(s)                                            |
| Hotel Postal Code       | A string that includes the postal code where a hotel was searched for. Specific to the selected event(s)                                                   |
| Hotel Region            | A string that includes the state, province, or region where a hotel was searched for. Specific to the selected event(s)                                    |
| Hotel Room Type         | A string that includes the type of hotel room searched for. Specific to the selected event(s)                                                              |
| Hotel Child Guests      | An integer that includes the total number of children staying in a hotel room. Specific to the selected event(s)                                           |
| Hotel Adult Guests      | An integer that includes the total number of adults staying in a hotel room. Specific to the selected event(s)                                             |
| Flight Identifier       | A string without spaces that includes an ID used to identify a flight. Specific to the selected event(s)                                                   |
| Flight Quantity         | An integer that includes the number of flights booked. Specific to the selected event(s)                                                                   |
| Flight Price            | A string that includes the price of the flight in the format `XX.XX`. Specific to the selected event(s)                                                    |
| Flight Booking Currency | A string in ISO 4217 format (three capital letters and no spaces) that includes the currency used to book the flight. Specific to the selected event(s)     |
| Flight Purchase ID      | A string that includes the order ID for a purchased flight. Specific to the selected event(s)                                                              |
| Flight Departure Date   | A string that includes the departure date of the flight in `YYYYMMDD` format. Specific to the selected event(s)                                            |
| Flight Return Date      | A string that includes the return date of the flight in `YYYYMMDD` format. Specific to the selected event(s)                                               |
| Flight Origin           | A string that includes the point of origin for a flight (airport or city). Specific to the selected event(s)                                               |
| Flight Destination      | A string that includes the destination for a flight (airport or city). Specific to the selected event(s)                                                   |
| Flight Service Clas     | A string that includes the service class for the seats on a flight searched (`Business`, `Economy`, `First`, et cetera). Specific to the selected event(s) |
| Flight Total Travelers  | An integer that includes the number of travelers on a flight. Specific to the selected event(s)                                                            |
| Flight Infant Travelers | An integer that includes the total number of infants booking a flight. Specific to the selected event(s)                                                   |
| Flight Minor Travelers  | An integer that includes the total number of minors booking a flight. Specific to the selected event(s)                                                    |
| Flight Senior Travelers | An integer that includes the total number of seniors booking a flight. Specific to the selected event(s)                                                   |
| Flight Adult Travelers  | An integer that includes the total number of adults booking a flight. Specific to the selected event(s)                                                    |

#### Travel - Cruise

| **Destination Name**                        | **Description**                                                                                                    |
|:--------------------------------------------|:-------------------------------------------------------------------------------------------------------------------|
| Cruise Identifier (`cruise_pid`)            | A string without spaces that includes an internal ID used to identify a cruise                                     |
| Cruise Quantity (`cruise_quantity`)         | An integer that includes the number of cruises booked. This is typically `1`.                                      |
| Cruise Price (`cruise_unitPrice`)           | A string that includes the price of the cruise in the format `XX.XX`                                               |
| Cruise Booking Currency (`cruise_currency`) | A string in ISO 4217 format (three capital letters and no spaces) that includes the currency used to book the cruise |
| Cruise Purchase ID (`cruise_purchaseId`)    | A string that includes the order ID for a purchased cruise                                                         |
| Cruise Start Date (`dtBegin`)               | A string that includes the start date of the cruise in `YYYYMMDD` format                                           |
| Cruise End Date (`dtEnd`)                   | A string that includes the end date of the cruise in `YYYYMMDD` format                                             |
| Cruise Adult Passengers (`cruise_adults`)   | An integer that includes the total number of adult passengers for the cruise                                       |
| Cruise Total Passengers (`cruise_guests`)   | An integer that includes the total number of guests for the cruise (adults + children)                             |
| Cruise Duration (`duration`) [Days]         | An integer that includes the duration of cruise in days                                                            |
| Cruise Departure Port (`port`)              | A string that includes the port of departure for the cruise                                                        |
| Cruise Destination Port (`dest`)            | A string that includes the port of destination for the cruise                                                      |
| Cruise Ship Name (`ship`)                   | A string that includes the name of the cruise ship                                                                 |
| Cruise Room Class (`rmClass`)               | A string that includes the type of room selected for the cruise                                                    |
| Cruise Room Number (`rmNumber`)             | A string or integer that includes the room number selected for the cruise                                          |
| Cruise Child Passengers (`cruise_children`) | An integer that includes the total number of child passengers for the cruise                                       |

### Travel - Hotel

| **Destination Name**                        | **Description**                                                                                                   |
|:--------------------------------------------|:------------------------------------------------------------------------------------------------------------------|
| Hotel Identifier (`hotel_pid`)              | A string without spaces that includes an internal ID used to identify a hotel                                     |
| Hotel Room Quantity (`hotel_quantity`)      | An integer that includes the number of hotel rooms booked                                                         |
| Hotel Room Price (`hotel_unitPrice`)        | A string that includes the price of the hotel in the format `XX.XX`                                               |
| Hotel Booking Currency (`hotel_currency`)   | A string in ISO 4217 format (three capital letters and no spaces) that includes the currency used to book the hotel |
| Hotel Purchase ID (`hotel_purchaseId`)      | A string that includes the order ID for a purchased hotel                                                         |
| Hotel Check-in Date (`checkIn`)             | A string that includes the check-in date for the hotel stay in `YYYYMMDD` format                                  |
| Hotel Check-out Date (`checkOut`)           | A string that includes the check-out date for the hotel stay in `YYYYMMDD` format                                 |
| Hotel Total Guests (`hotel_guests`)         | An integer that includes the total number of guests staying in a hotel room (adults + children)                   |
| Hotel City (`city`)                         | A string that includes the city where a hotel was searched for                                                    |
| Hotel Country (`country`)                   | A string that includes the country where a hotel was searched for                                                 |
| Number of Hotel Rooms (`rooms`)             | An integer that includes the total number of hotel rooms searched for                                             |
| Hotel Airport Code (`airport`)              | A string that includes the three character airport code to search for adjacent airports                           |
| Hotel Airport Code City (`airportCodeCity`) | A string that includes the adjacent city for the airport included in airport                                      |
| Hotel Postal Code (`postalCode`)            | A string that includes the postal code where a hotel was searched for                                             |
| Hotel Region (`region`)                     | A string that includes the state, province, or region where a hotel was searched for                              |
| Hotel Room Type (`type`)                    | A string that includes the type of hotel room searched for                                                        |
| Hotel Child Guests (`hotel_children`)       | An integer that includes the total number of children staying in a hotel room                                     |
| Hotel Adult Guests (`hotel_adults`)         | An integer that includes the total number of adults staying in a hotel room                                       |

### Travel - Flight

| **Destination Name**                        | **Description**                                                                                                         |
|:--------------------------------------------|:------------------------------------------------------------------------------------------------------------------------|
| Flight Identifier (`flight_pid`)            | A string without spaces that includes an ID used to identify a flight                                                   |
| Flight Quantity (`flight_quantity`)         | An integer that includes the number of flights booked                                                                   |
| Flight Price (`flight_unitPrice`)           | A string that includes the price of the flight in the format `XX.XX`                                                    |
| Flight Booking Currency (`flight_currency`) | A string in ISO 4217 format (three capital letters and no spaces) that includes the currency used to book the flight     |
| Flight Purchase ID (`flight_purchaseId`)    | A string that includes the order ID for a purchased flight                                                              |
| Flight Departure Date (`depDate`)           | A string that includes the departure date of the flight in `YYYYMMDD` format                                            |
| Flight Return Date (`retDate`)              | A string that includes the return date of the flight in `YYYYMMDD` format. This is not used for multiple flights.       |
| Flight Origin (`origin`)                    | A string that includes the point of origin for a flight (airport or city)                                               |
| Flight Destination (`destination`)          | A string that includes the destination for a flight (airport or city)                                                   |
| Flight Service Clas (`serviceClass`)        | A string that includes the service class for the seats on a flight searched (`Business`, `Economy`, `First`, et cetera) |
| Flight Total Travelers (`travelers`)        | An integer that includes the number of travelers on a flight                                                            |
| Flight Infant Travelers (`infants`)         | An integer that includes the total number of infants booking a flight                                                   |
| Flight Minor Travelers (`minors`)           | An integer that includes the total number of minors booking a flight                                                    |
| Flight Senior Travelers (`seniors`)         | An integer that includes the total number of seniors booking a flight                                                   |
| Flight Adult Travelers (`flight_adults`)    | An integer that includes the total number of adults booking a flight                                                    |
