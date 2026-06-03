---
title: Single-Page Applications
description: Learn to track links and events for single-page applications.
url: https://docs.tealium.com/platforms/javascript/single-page-applications/
---
 The [events system]() replaces previous event tracking solutions, such as the JQuery extension. The [Browser History Change](), [Page Load](), and [Hash Change]() event listeners are especially useful for single-page applications. 

## Setup

On a single-page application (SPA) where the page loads `utag.js` only once per visit, suppress the automatic page view tracking call to allow your application to make these calls directly.

To override the automatic page tracking add this line to your page prior to loading `utag.js`:  
```javascript
window.utag_cfg_ovrd = window.utag_cfg_ovrd || {};
window.utag_cfg_ovrd.noview = true
```

Once your application is loaded (and `utag.js `is loaded), trigger `utag.view()` tracking calls in your page code. These calls are typically triggered at the DOM-ready event or any event that causes a content view refresh. [Learn more](/platforms/javascript/settings/) about the available settings to adjust the behavior of `utag.js`.

The `utag_data` object declared on initial page landing is _not_ re-purposed with these calls. To use data from the initial page landing, it needs to be re-declared and passed again in the function call.

Global and Tag-scoped Extensions are executed during these calls. Pre-loader and DOM Ready extensions are not executed during these calls.


## Track Views

Track views in single-page applications with the [`utag.view()`](/platforms/javascript/api/tracking-functions/#utag-view) function.

The following `utag.view()` function call demonstrates how to pass data using key-value pairs:  
```javascript
utag.view({ variable1:&#34;VARIABLE1 VALUE&#34;, variable2:&#34;VARIABLE2 VALUE&#34;, variable3:&#34;VARIABLE3 VALUE&#34; });
```

### Examples

The following is a content site example in which a visitor searched for &#34;politics&#34;:  
```javascript
utag.view({tealium_event:&#34;search&#34;, search_keyword:&#34;politics&#34;, search_results: 42});
```

The following example demonstrates how to track views:  
```javascript
utag.view({
    &#34;demo_site&#34; : &#34;Tealium React Demo&#34;,
    &#34;demo_event&#34; : &#34;View &#34; &#43; name
})
```

## Track Events

Track links and events in single-page applications with the [`utag.link()`](/platforms/javascript/api/tracking-functions/#utag-view) function.

If jQuery is installed you have the option to use the [jQuery onHandler]() extension. This extension is configurable for specific event bindings to trigger the `utag.link()` and `utag.view()` functions. This lets you avoid hard-coding the tracking logic in your side code.

The following `utag.link()` function call demonstrates how to pass data using key-value pairs:  
```javascript
utag.link({ variable1:&#39;VARIABLE1 VALUE&#39;, variable2:&#39;VARIABLE2 VALUE&#39; });
```

### Queue for early tracking events

In version 4.52 and later, a queuing system handles early tracking events in SPAs. This ensures that `utag.view`, `utag.link`, and `utag.track` functions are available immediately on page load, preventing errors or lost events when these functions are called before `utag.js` fully loads. For more information on how to enable this feature, see [Queue for early tracking events](/platforms/javascript/version-4-52/#queue-for-early-tracking-events).

### Examples

The following is a content site example of tracking social media sharing actions:

```javascript
utag.link({
    &#34;content_id&#34;         : &#34;38121&#34;,
    &#34;page_friendly_url&#34; : &#34;/travel/national_parks&#34;,
    &#34;page_name&#34;          : &#34;Travel: National Parks&#34;,
    &#34;social_network&#34;     : &#34;facebook&#34;,
    &#34;tealium_event&#34;      : &#34;social_share&#34;
})
```

The following ReactJS example, from the [Tealium demo application](http://react.tealiumdemo.com/), demonstrates how to track events for add, edit, save and remove function. Each function call triggers the `utag.link()` function.  
```javascript
add(text) {
    utag.link({
        &#34;page_type&#34;: &#34;react&#34;,
        &#34;view_name&#34;: &#34;board&#34;,
        &#34;event_type&#34;: &#34;click&#34;,
        &#34;event_name&#34;: &#34;add_note&#34;,
        &#34;tealium_event&#34;: &#34;add_note&#34;
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
        &#34;page_type&#34;: &#34;react&#34;,
        &#34;view_name&#34;: &#34;board&#34;,
        &#34;event_type&#34;: &#34;click&#34;,
        &#34;event_name&#34;: &#34;edit_note&#34;,
        &#34;tealium_event&#34;: &#34;edit_note&#34;
    })
    this.setState({editing: true});
}
save() {
    utag.link({
        &#34;page_type&#34;: &#34;react&#34;,
        &#34;view_name&#34;: &#34;board&#34;,
        &#34;event_type&#34;: &#34;click&#34;,
        &#34;event_name&#34;: &#34;save_note&#34;,
        &#34;tealium_event&#34;: &#34;save_note&#34;
    })
    this.props.onChange(this.refs.newText.value, this.props.id)
    this.setState({editing: false});
}
remove() {
    utag.link({
        &#34;page_type&#34;: &#34;react&#34;,
        &#34;view_name&#34;: &#34;board&#34;,
        &#34;event_type&#34;: &#34;click&#34;,
        &#34;event_name&#34;: &#34;remove_note&#34;,
        &#34;tealium_event&#34;: &#34;remove_note&#34;
    })

    this.props.onRemove(this.props.id)
}
```
