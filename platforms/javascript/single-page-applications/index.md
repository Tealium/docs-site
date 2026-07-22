---
title: Single-Page Applications
description: Learn to track links and events for single-page applications.
url: https://docs.tealium.com/platforms/javascript/single-page-applications/
---

<blockquote>
The [events system](https://docs.tealium.com/about-events/) replaces previous event tracking solutions, such as the JQuery extension. The [Browser History Change](https://docs.tealium.com/browser-history-change-event/), [Page Load](https://docs.tealium.com/page-load-event/), and [Hash Change](https://docs.tealium.com/hash-change-event/) event listeners are especially useful for single-page applications.
</blockquote>


## Setup

On a single-page application (SPA) where the page loads `utag.js` only once per visit, suppress the automatic page view tracking call to allow your application to make these calls directly.

To override the automatic page tracking add this line to your page prior to loading `utag.js`:  
```javascript
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {};
window.utag_cfg_ovrd.noview = true
```

Once your application is loaded (and `utag.js `is loaded), trigger `utag.view()` tracking calls in your page code. These calls are typically triggered at the DOM-ready event or any event that causes a content view refresh. [Learn more](https://docs.tealium.com/platforms/javascript/settings/) about the available settings to adjust the behavior of `utag.js`.

The `utag_data` object declared on initial page landing is _not_ re-purposed with these calls. To use data from the initial page landing, it needs to be re-declared and passed again in the function call.

Global and Tag-scoped Extensions are executed during these calls. Pre-loader and DOM Ready extensions are not executed during these calls.


## Track Views

Track views in single-page applications with the [`utag.view()`](https://docs.tealium.com/platforms/javascript/api/tracking-functions/#utag-view) function.

The following `utag.view()` function call demonstrates how to pass data using key-value pairs:  
```javascript
utag.view({ variable1:"VARIABLE1 VALUE", variable2:"VARIABLE2 VALUE", variable3:"VARIABLE3 VALUE" });
```

### Examples

The following is a content site example in which a visitor searched for "politics":  
```javascript
utag.view({tealium_event:"search", search_keyword:"politics", search_results: 42});
```

The following example demonstrates how to track views:  
```javascript
utag.view({
    "demo_site" : "Tealium React Demo",
    "demo_event" : "View " + name
})
```

## Track Events

Track links and events in single-page applications with the [`utag.link()`](https://docs.tealium.com/platforms/javascript/api/tracking-functions/#utag-view) function.


<blockquote>
If jQuery is installed you have the option to use the [jQuery onHandler](https://docs.tealium.com/jquery-onhandler-extension/) extension. This extension is configurable for specific event bindings to trigger the `utag.link()` and `utag.view()` functions. This lets you avoid hard-coding the tracking logic in your side code.
</blockquote>


The following `utag.link()` function call demonstrates how to pass data using key-value pairs:  
```javascript
utag.link({ variable1:'VARIABLE1 VALUE', variable2:'VARIABLE2 VALUE' });
```

### Queue for early tracking events

In version 4.52 and later, a queuing system handles early tracking events in SPAs. This ensures that `utag.view`, `utag.link`, and `utag.track` functions are available immediately on page load, preventing errors or lost events when these functions are called before `utag.js` fully loads. For more information on how to enable this feature, see [Queue for early tracking events](https://docs.tealium.com/platforms/javascript/version-4-52/#queue-for-early-tracking-events).

### Examples

The following is a content site example of tracking social media sharing actions:

```javascript
utag.link({
    "content_id"         : "38121",
    "page_friendly_url" : "/travel/national_parks",
    "page_name"          : "Travel: National Parks",
    "social_network"     : "facebook",
    "tealium_event"      : "social_share"
})
```

The following ReactJS example, from the [Tealium demo application](http://react.tealiumdemo.com/), demonstrates how to track events for add, edit, save and remove function. Each function call triggers the `utag.link()` function.  
```javascript
add(text) {
    utag.link({
        "page_type": "react",
        "view_name": "board",
        "event_type": "click",
        "event_name": "add_note",
        "tealium_event": "add_note"
    })
    var notes = [
        ...this.state.notes,
        {
            id: this.nextId(),
            note: text
        }
    ]
    this.setState({notes})
}

edit() {
    utag.link({
        "page_type": "react",
        "view_name": "board",
        "event_type": "click",
        "event_name": "edit_note",
        "tealium_event": "edit_note"
    })
    this.setState({editing: true});
}
save() {
    utag.link({
        "page_type": "react",
        "view_name": "board",
        "event_type": "click",
        "event_name": "save_note",
        "tealium_event": "save_note"
    })
    this.props.onChange(this.refs.newText.value, this.props.id)
    this.setState({editing: false});
}
remove() {
    utag.link({
        "page_type": "react",
        "view_name": "board",
        "event_type": "click",
        "event_name": "remove_note",
        "tealium_event": "remove_note"
    })

    this.props.onRemove(this.props.id)
}
```
