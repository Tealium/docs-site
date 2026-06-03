---
title: Event scope
description: This article describes the scope used for event listeners.
url: https://docs.tealium.com/iq-tag-management/events/event-scope/
---
The event listener scope determines when the initialization code runs for the event. Even though an event can trigger multiple times, the initialization code runs only once.

The following scope options are available:

* **DOM ready** – Runs at the [DOMContentLoaded browser event.](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded) Events listeners are loaded asynchronously to optimize page performance and visitor experience. The exact order of DOM Ready event listeners, extensions, and tags cannot be guaranteed.
* **After Load Rules** - Runs after load rules are evaluated. Load rules are reevaluated after each tracking call.

We recommend using the default scope of **DOM Ready** for standard site implementations and **After Load Rules** for Single Page Applications (SPA). DOM Ready ensures that the visitor&#39;s browser loads all of the page elements for tracking, while SPAs may use fewer DOM event listeners and give you a limited view of the trackable elements. When you use **After Load Rules** for an SPA, the load rules are reevaluated after every event to see if the criteria has changed to load the event listener on the page. 

In most standard implementations, the **DOM Ready** scope occurs sequentially after **After Load Rules**, but this timing is not guaranteed.

For a detailed overview of event execution order, see [Order of Operations]().

