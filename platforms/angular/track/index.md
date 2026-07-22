---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/angular/track/
---
Once `TealiumUtagService` has been initialized, add tracking calls throughout the application code.

## Track Views

The [`view()`](https://docs.tealium.com/platforms/angular/api/#view) method tracks page views. This method takes an object of key-value pairs as the single parameter, as shown in the following example:

```javascript
this.tealium.view({
    "tealium_event"  : "SCREEN_NAME",
    "page_type"      : "PAGE_TYPE",
    "product_id"     : ["PRODUCT_ID"]});
```
## Track Events

The [`link()`](https://docs.tealium.com/platforms/angular/api/#link) method tracks in-page events. This method takes an object of key-value pairs as the single parameter, as shown in the following example:

```javascript
this.tealium.link({
    "tealium_event" : "EVENT_NAME",
    "customer_id"   : "CUSTOMER_ID"});
```
