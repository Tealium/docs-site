---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/angular/track/
---
Once `TealiumUtagService` has been initialized, add tracking calls throughout the application code.

## Track Views

The [`view()`](/platforms/angular/api/#view) method tracks page views. This method takes an object of key-value pairs as the single parameter, as shown in the following example:

```javascript
this.tealium.view({
    &#34;tealium_event&#34;  : &#34;SCREEN_NAME&#34;,
    &#34;page_type&#34;      : &#34;PAGE_TYPE&#34;,
    &#34;product_id&#34;     : [&#34;PRODUCT_ID&#34;]});
```
## Track Events

The [`link()`](/platforms/angular/api/#link) method tracks in-page events. This method takes an object of key-value pairs as the single parameter, as shown in the following example:

```javascript
this.tealium.link({
    &#34;tealium_event&#34; : &#34;EVENT_NAME&#34;,
    &#34;customer_id&#34;   : &#34;CUSTOMER_ID&#34;});
```
