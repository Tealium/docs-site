---
title: Track
description: Learn about the functions for tracking user activity.
url: https://docs.tealium.com/platforms/javascript/track/
---
## Track Views

The [`utag.view()`](https://docs.tealium.com/platforms/javascript/api/tracking-functions/#utag-view) function tracks page views, virtual page views, and Ajax page flows. Calling this function triggers the corresponding page tracking functionality within your configured vendor tags. `utag.js` automatically triggers this function on every page load.

`utag.view()` is commonly used for Ajax page flows where the URL does not refresh as the user navigates the site. For example, single-page checkout or single-page application.

The Universal Data Object (UDO) declared on the initial page load, `utag_data`, is not re-purposed with these calls. You must explicitly pass a new data object to this function.  


<blockquote>
Best practice is to use the variable [`tealium_event`](#tealium-event) to identify important page view events and `page_type` to uniquely identify page templates.
</blockquote>


The following example tracks a "Product Quick View" view:

```javascript
utag.view({
    "tealium_event": "product_view",
    "page_type"    : "product_quick_view",
    "page_name"    : "Quick View: Shirts: Lucky Shirt",
    "product_id"   : ["12345"],
    "product_name" : ["Lucky Shirt"]
});
```

## Track Events

The [`utag.link()`](https://docs.tealium.com/platforms/javascript/api/tracking-functions/#utag-link) function tracks events such as non-page views, page interactions, and other dynamic page events. Event tracking collects information about your visitors’ interactions _within_ a page. While page view tracking gathers information about the navigation path a visitor takes, event tracking monitors what visitors do in-between navigation steps.

The following example tracks an "Add to Cart" event: 

```javascript
utag.link({
    "tealium_event"    : "cart_add",
    "product_id"       : ["12345"],
    "product_name"     : ["Lucky Shirt"],
    "product_quantity" : ["2"],
    "product_price"    : ["12.99"]
});
```

## `tealium_event`

To uniquely identify each type of interaction to be tracked, use the reserved variable `tealium_event`. This variable is referenced throughout Tealium iQ to configure load rules, extensions, and data mappings. Use additional variables names of your choosing for all other event data.

The suggested `tealium_event` values include, but are not limited to:

| Value of `tealium_event` | Event Description |
| --- | --- |
| `page_view` | Page view |
| `product_view` | Product detail page view |
| `search` | Internal search |
| `cart_add` | Add to Shopping Cart |
| `cart_remove` | Remove from Shopping Cart |
| `cart_view` | View Shopping Cart |
| `purchase` | Complete a purchase |
| `user_register` | User Registration Complete |
| `user_login` | User Login |
| `email_signup` | Newsletter Email Signup |
| `social_share` | Share a Link on a Social Site |

The following example adds additional information related to the event in the tracking call:

```javascript
utag.link({
    "tealium_event"  : "social_share",
    "social_network" : "LinkedIn",
    "shared_link"    : "https://tealium.com/"
});
```

Learn more about [the data layer and Tealium events](https://docs.tealium.com/an-introduction-to-the-data-layer/).

## Implementation Options

Just as page view tracking requires a data layer object to give context about which page is being tracked, event tracking also requires a data layer object be included in the tracking calls. Include variables relevant to the event in the data object of the tracking call.

The following sections describe the approaches for implementing Tealium’s event tracking into your website.

### jQuery and HTML5

Use the [jQuery Extension](https://docs.tealium.com/jquery-onhandler-extension/) to track basic interactions within a page, such as clicking, expanding, and selecting. Use HTML5 [data attributes](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_data_attributes) to implement informational properties of tracked elements. Requires a web page with [semantic HTML](https://en.wikipedia.org/wiki/Semantic_HTML).

* Best used for link clicks, button clicks, form field interactions.
* Not recommended for Ajax page flows, or form submissions.

An element with data attributes might look like this in the page code:

```html
<a href="/logout" data-click_name="Sign Out" data-click_category="header">Log out</a> 
```

Reference these attributes in the jQuery Extension to track clicks on this link and to set the relevant event data using the "JS Code" option.

*   Use a selector to identify elements with a specific data attribute. For example, `a[data-click_name]`.
*   Set a variable using the "JS Code" option to reference a data attribute in the clicked element. For example, `$(this).data('click_name')`.

### Page Code

Page code is used for tracking dynamic page content refreshes, Ajax pages, modal form submissions or any event that requires a round-trip request/response to the client’s web server to fetch additional data not already present on the page.

* Best used for modal forms, product quick view, single page websites, add to cart from non-product pages.
* Not recommended for link tracking.

### Video Tracking

Video tracking often requires a custom solution coding to the specifications of the video platform API.

Learn more about Tealium's current solution in the [YouTube Video Tracking Setup Guide](https://docs.tealium.com/youtube-event/).

### Single Page Applications

Learn about tracking views and events for [single page applications](https://docs.tealium.com/platforms/javascript/single-page-applications/).

