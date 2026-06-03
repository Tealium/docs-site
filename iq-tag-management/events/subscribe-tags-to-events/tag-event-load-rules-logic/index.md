---
title: Tag and event load rules logic
description: This article explains tag and event load rules logic.
url: https://docs.tealium.com/iq-tag-management/events/subscribe-tags-to-events/tag-event-load-rules-logic/
---
Load rules for an event listener combined with event listeners and load rules for a tag can result in complex logic and behaviors for loading and firing.

## How tags and events load

Subscribed tags and event listeners use the following logic to determine when they load:

* The event listener load rules determine when the event loads, regardless of the load rules of any tag that subscribes to it.
* If a tag is subscribed to an event listener in an AND logical relationship, the event listener load rules determine when a tag loads.
* If an tag is subscribed to an event listener in an OR logical relationship, the tag load rules determine when the tag loads.

## How tags and event listeners fire

How the event listener appears in tag load rules logic determines whether the event includes the tag data in the event listener payload:

* An event listener fires and sends its variables when the visitor performs its action, regardless of any tags that subscribes to it.
* If a tag is subscribed to an event listener in an AND logical relationship, when the visitor performs the event listener action, the event listener fires the tag and sends the event listener variables with the tag data to the tag endpoint.
* If a tag is subscribed to an event listener in an OR logical relationship, the tag fires when the page is loaded and sends its variables to the endpoint. When the visitor performs the event listener action, the event listener fires the tag and sends the event listener variables with the tag data to the tag endpoint.
