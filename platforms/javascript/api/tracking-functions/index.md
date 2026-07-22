---
title: Tracking Functions
description: Reference guide for tracking functions provided by Tealium for JavaScript.
url: https://docs.tealium.com/platforms/javascript/api/tracking-functions/
---
The following tracking functions are available:

| Function | Description |
| --- | --- |
| `utag.link()` | Tracks non-page views, page interactions, and other dynamic page events |
| `utag.track()` | Tracks either page views or events, based on the first parameter value |
| `utag.view()` | Tracks page views, virtual page views, and Ajax page flows |


<blockquote>
Using the `uid_array` parameter bypasses load rules. When using load rules for consent enforcement, the `uid_array` parameter will also ignore the consent conditions. For more information, see [About Load Rules](https://docs.tealium.com/about-load-rules/#load-rules-and-consent-enforcement).
</blockquote>


## `utag.link()`

Tracks non-page views, page interactions, and other dynamic page events. Calling this function triggers the corresponding vendor tracking functionality within your configured tags. 

```javascript
utag.link(data_object, callback, [uid_array]);
```

| Parameter | Description |
| --- | --- |
| `data_object`| A data object containing the data layer variables associated with the event.|
| `callback`| A function to be executed after the tracking call has completed. |
| `uid_array`| An array of tag UID's to trigger. |

## `utag.track()`

Tracks either page views or events, based on the first parameter value. Both [`utag.link()`](#utag-link) and [`utag.view()`](#utag-view) wrap around this function.

```javascript
utag.track(event_type, data_object, callback, [uid_array]);
```

| Parameter | Description |
| --- | --- |
| `event_type` | The type of event. Set to `view` for page views, or `link` for events |
| `data_object`| A data object containing the data layer variables associated with the event.|
| `callback`| A function to be executed after the tracking call has completed. |
| `uid_array`| An array of tag UID's to trigger. |

## `utag.view()`

Tracks page views, virtual page views, and Ajax page flows. Calling this function triggers the corresponding page tracking functionality within your configured vendor tags. `utag.js` automatically triggers this function on every page load.

```javascript
utag.view(data_object, callback, [uid_array]);
```

| Parameter | Type | Description |
| --- | --- | --- |
| `data_object` | Object | (Optional) A data object containing the attributes associated with this specific tracking call. Uses the same format and variable names as the Universal Data Object.  |
| `callback` | Function | (Optional) A function to be executed after the tracking call has completed.  |
| `uid_array` | Array | (Optional) An array of tag IDs. Limits the tracking call for the vendor tags specified by the UID's in this array.  |
