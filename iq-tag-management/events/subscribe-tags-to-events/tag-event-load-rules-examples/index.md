---
title: Tag, event, and load rules examples
description: This article provides examples of how tags, event listeners, and load rules work together.
url: https://docs.tealium.com/iq-tag-management/events/subscribe-tags-to-events/tag-event-load-rules-examples/
---
## Examples without load rules

For the following examples, we will use a website with a home page and product pages. On that site, we will use a set of tags and event listeners with various configurations and relationships.

### Tag not subscribed to event

A user creates an event listener with the following settings:

* Element Visibility event type.
* An ad banner CSS element ID.
* Fully visible for five seconds.
* Trigger only once.
* Uses the DOM Ready scope (by default).
* Uses the All Pages and event listeners load rule.
* A Tealium Collect tag exists on the page, which uses the All Pages and Events load rule.

![](/images/iq-tag-management/events/tag_event_loadrules_example_1.png)

**All pages:**

* The product details page loads this event listener after the page is DOM Ready.
* The page loads the Tealium Collect tag.
* The tag fires and sends its payload to the tag endpoint.
* The first time the visitor sees an entire ad banner on that page for more than five seconds, the event listener fires and sends its variables in a tracking call.

### Tag subscribed to event

A user creates an event listener with the following settings:

* Element Visibility event type.
* An ad banner CSS element ID.
* Fully visible for five seconds.
* Trigger only once.
* Uses the DOM Ready scope (by default).
* Uses the All Pages and Events load rule.
* A Tealium Collect tag exists on the page, which is subscribed to the Element visible event.

![](/images/iq-tag-management/events/tag_event_loadrules_example_2.png)

**All pages:**

* The product details page loads this event listener after the page is DOM Ready.
* The page loads the Tealium Collect tag.
* The first time the visitor sees an entire ad banner on that page for more than five seconds, the event listener fires the Tealium Collect tag and sends its variables in a tracking call along with the Tealium Collect tag payload.

## Examples with load rules

For the following examples, we will use a website with a home page and product pages. On that site, we will use a set of tags, event listeners, and load rules with various configurations and relationships.

### Tag not subscribed to event

A user creates an event listener with the following settings:

* Element Visibility event type.
* An ad banner CSS element ID.
* Fully visible for five seconds.
* Trigger only once.
* Uses the DOM Ready scope (by default).
* Uses a load rule so it only loads on product details pages.
* A Tealium Collect tag exists on the page, which uses the All Pages and Events load rule.

![](/images/iq-tag-management/events/tag_event_loadrules_example_3.png)

**Product Page**

* The product details page loads this event listener after the page is DOM Ready.
* The page loads the Tealium Collect tag.
* The tag fires and sends its payload to the tag endpoint.
* The first time the visitor sees an entire ad banner on that page for more than five seconds, the event listener fires and sends its variables in a tracking call.

**Home Page**

* The home page does not load this event because the load rules specify that the event listener only loads on product pages.
* The home page loads the Tealium Collect tag.
* The tag fires and sends its payload to the tag endpoint.

### Tag subscribed to event (AND logic)

A user creates an event listener with the following settings:

* Element Visibility event type.
* An ad banner CSS element ID.
* Fully visible for five seconds.
* Trigger only once.
* Uses the DOM Ready scope (by default).
* Uses a load rule so it only loads on product details pages.
* Added to the Tealium Collect tag rules and event listeners with AND logic, where the rest of the tag rules and event listeners evaluate to `true`.![](/images/iq-tag-management/events/tag_event_loadrules_example_4.png)

**Product Page:**

* The product details page loads this event listener after the page is DOM Ready.
* The page also loads the Tealium Collect tag because its load rules and the event listener load rule all evaluate to `true`, but it does not immediately fire.
* The first time the visitor sees an entire ad banner on that page for more than five seconds, the event listener fires the Tealium Collect tag and sends its variables in a tracking call along with the Tealium Collect tag payload.

**Home Page:**

* The home page does not load this event because the load rules specify that the event listener only loads on product pages.
* Because the Tealium Connect tag is subscribed to the event with AND logic, the tag load rules and the event listener rule combined all evaluate to `false`.
* The home page does not load the Tealium Connect tag.

### Tag subscribed to event (OR logic)

A user creates an event listener with the following settings:

* Element Visibility event type.
* An ad banner CSS element ID.
* Fully visible for five seconds.
* Trigger only once.
* Uses the DOM Ready scope (by default).
* Uses a load rule so it only loads on product details pages.
* Added to the Tealium Collect tag rules and event listeners with OR logic, where the rest of the tag rules and event listeners evaluate to `true`.![](/images/iq-tag-management/events/tag_event_loadrules_example_5.png)

**Product Page:**

* The product details page loads this event listener after the page is DOM Ready.
* The page loads the Tealium Collect tag.
* The tag fires and sends its payload to the tag endpoint.
* The first time the visitor sees an entire ad banner on that page for more than five seconds, the event listener fires the Tealium Collect tag and sends its variables in a tracking call along with the Tealium Collect tag payload.

**Home Page:**

* The home page does not load this event listener because the load rules specify that the event listener only loads on product pages.
* Because the Tealium Connect tag is subscribed to the event listener with OR logic, the tag load rules and the event listener rule all evaluate to `true`.
* The home page loads the Tealium Connect tag and fires it.

### Tag subscribed to two event listeners (OR logic)

A user creates two event listeners with the following settings:

**Event #1 - Element visible**

* Element Visibility event type.
* An ad banner CSS element ID.
* Fully visible for five seconds.
* Trigger only once.
* Uses the DOM Ready scope (by default).
* Uses a load rule so it only loads on product details pages.
* Added to the Tealium Collect tag rules and event listeners with OR logic, where the rest of the tag rules and event listeners evaluate to `true`.

**Event #2 - Form submission**

* Form Submission event type.
* A form CSS element ID.
* Trigger only once.
* Uses the DOM Ready scope (by default).
* Uses a load rule so it only loads on product details pages.
* Added to the Tealium Collect tag rules and event listeners with OR logic, where the rest of the tag rules and event listeners evaluate to `true`.
![](/images/iq-tag-management/events/tag_event_loadrules_example_6.png)

**Product Page:**

* The product details page loads these two event listeners after the page is DOM Ready.
* The page loads the Tealium Collect tag.
* The tag fires and sends its payload to the tag endpoint.
* The first time the visitor sees an entire ad banner on that page for more than five seconds, the event listener fires the Tealium Collect tag and sends its variables in a tracking call along with the Tealium Collect tag payload.
* The first time the visitor submits the form, the event listener fires the Tealium Collect tag and sends its variables in a tracking call along with the Tealium Collect tag payload

**Home page:**

* The home page does not load either event listener because the load rules specify that the event listeners only load on product pages.
* Because the Tealium Connect tag is subscribed to the event listeners with OR logic, the tag load rules and the event listener rule combined all evaluate to `true`.
* The home page loads the Tealium Connect tag and fires it.
