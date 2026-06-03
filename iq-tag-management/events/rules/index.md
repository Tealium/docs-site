---
title: Event rules
description: This article describes event rules.
url: https://docs.tealium.com/iq-tag-management/events/rules/
---
Use rules to select which pages load your event listener. Events can re-use existing load rules, or you can create new ones.

The configuration dialog provides a drag-and-drop interface for setting up the logic for a rule.

## Tags with events

You can subscribe a tag to an event in the **Rules and Events** section for your tag. Precisely control when a tag fires and when the data that is sent to the tag endpoint by combining load rules for a tag and an event listener conditions.

For more information about tags and events, see [Subscribe a tag to an event]().

If you do not select any rules for an event listener, the event listener will load and listen on every page. This condition can cause performance issues for your visitors as well as your data collection. We recommend that you only load events listeners on pages that you expect the event listener actions to happen, and only when you want to collect data from those actions.


## Events and load rules

Build rules using the following logical operators:

* **OR** - Load the event listener if _any_ of its load rules evaluate to true.
* **AND** - Load the event listener if _all_ of its load rules evaluate to true.
* **AND NOT** - Load the event listener if the load rules before **AND NOT** evaluate to true and the load rules after **AND NOT** evaluate to false.

When you drag and drop load rules into the logic boxes, the dialog will automatically generate more empty **OR** logic boxes. Click the &#43; **AND** button to generate another top-level AND logic box.

### AND operators

To create conditions where an event listener will load on product pages and when the visitor&#39;s cart is empty, drag the **Product page** load rule and the **Cart is empty** load rule into an **AND** relationship:

![](/images/guides/iq/event-and-rules.png)

### OR operators

To change the event listener to load on product pages or when the visitor&#39;s cart is empty, drag the **Cart is empty** load rule into the **OR** logic box:

![](/images/guides/iq/event-or-rules.png)

### AND NOT operators

To change the event listener to load on product pages or when the visitor&#39;s cart is not empty, drag the **Cart is empty** load rule to the **AND NOT** logic box:

![](/images/guides/iq/event-and-not-rules.png)

### Nested operators

You can nest the rules with multiple levels of these conditions to create advanced logic for your load rules. The following example will load an event listener if the viewer is looking at a product page or a product list page on their US site, but only if their cart is not empty and they are not on the home page.

![](/images/guides/iq/event-rules-advanced.png)
