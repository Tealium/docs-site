---
title: About events
description: This article provides an introduction to our event system.
url: https://docs.tealium.com/iq-tag-management/events/about/
---
## How it works

The events system replaces previous event tracking solutions, such as the JQuery extension.

Event listeners, also known as _events_, are prebuilt, configurable JavaScript listeners that track specific visitor actions on pages. 

An event listener tracks when a visitor performs a specified action on a page, such as clicking on an element, scrolling down the page, and using video players. When a visitor performs the action, a tracking call is triggered that includes the event listener variables.

With no-code event listeners, you can do the following:

* Configure an event listener for your own unique needs.
* Select from various scopes that determine when the event listener loads on the page.
* Set up advanced rule logic to determine which pages load the event listeners.
* Set unique Event Triggers that you can configure based on your tracking needs.
* Target specific elements on the page with event listeners.
* Configure a data payload to be sent when the action takes place.


## Event types and variables

The following types of events are available through this feature:

* [**Click**]() - When a visitor clicks their mouse on a page.
* [**Mouseover**]() - When a visitor hovers their mouse over a specific element on a page.
* [**Form Submission**]() - When a visitor submits a form on a page.
* [**YouTube**]() - When a visitor interacts with an embedded YouTube video on a page.
* [**Vimeo**]() - When a visitor interacts with an embedded Vimeo video on a page.
* [**HTML5 Video**]() - When a visitor interacts with an embedded HTML5 video on a page.
* [**Page Load**]() - When a visitor loads a page.
* [**Scroll**]() - When a visitor scrolls through a page, vertically or horizontally.
* [**Element Visibility**]() - When the page displays a screen element to a visitor.
* [**Browser History Change**]() - When a visitor navigates through a single page application (SPA).
* [**Hash Change**]() - When the anchor part of the page&#39;s URL after the hash symbol (`#`) changes.

Each of these events is preconfigured with a `tealium_event` value specific to that event (for example, `scroll` for scroll events). Some of these event types include additional event variables by default, and you can customize or add event variables as needed.

For more information, see [Best Practices - Event tracking]().
