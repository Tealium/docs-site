---
title: Kayak Tag Connector Setup Guide
description: This article describes how to set up the KAYAK tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/kayak-tag-connector/
---
## Tag tips

* Use event mappings to configure when confirmation and cancellation pixels are fired.
* The Commission Currency value will default to the e-commerce Currency value if one is not provided.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Partner Code**
  * Supplied by KAYAK, this is the internal KAYAK code.
* **Click ID Query Parameter Name**
  * Name of the query parameter that will be used to pass the click id in the tracking url.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Tag configurations

|Variable| Description|
|---| ---|
|Partner Code| (partner\_code)|
|Booked On Date| (bookedon)|
|Kayak Commission Amount| (kayakcommission)|
|Commission Currency| (commissioncurrency)|
|Booking Type| (bookingtype)|
|Kayak Commission Percentage| (commissionpercentage)|
|Custom Field 1| (tag1)|
|Custom Field 2| (tag2)|

### E-Commerce

|Variable| Description|
|---| ---|
|Order ID/Booking ID| (order\_id) (Overrides \_corder)|
|Order Total| (order\_total) (Overrides \_ctotal)|
|Currency| (order\_currency) (Overrides \_ccurrency)|

### Hotel

|Variable| Description|
|---| ---|
|Booking Check In Date| (checkin)|
|Booking Check Out Date| (checkout)|
|Booked Property ID| (hid)|
|Number of Travelers| (travelers)|
|Number of Rooms| (rooms)|

### Flight

|Variable| Description|
|---| ---|
|Itinerary Description| (itin)|
|Origin Airport Code| (origin)|
|Destination Airport Code| (destination)|
|Fare Class| (fareClass)|
|Cabin Type| (cabinType)|

### Car

|Variable| Description|
|---| ---|
|Pick Up Date| (pickup)|
|Drop Off Date| (dropoff)|
|Pick Up Location ID| (pickupid)|
|Drop Off Location ID| (dropoffid)|
|Car Agency ID| (agency)|

### Events

|Variable| Description|
|---| ---|
|Confirmation| Confirmation|
|Cancellation| Cancellation|
