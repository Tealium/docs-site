---
title: Event feeds
description: Event feeds are a collection of events that match specific conditions based on their attributes.
url: https://docs.tealium.com/server-side/getting-started/eventstream-api-hub/event-feeds/
---
The default event feed is named `All Events` and contains all incoming events, but you can create new feeds to identify subsets of events based on their attributes.

## How it works

Feeds identify your most important types of events to take action on using vendor connectors.

Here&#39;s how it works:

* **Feed name**  
An event feed has a name that identifies it throughout the interface, such as when configuring a connector action. Choose a user-friendly name that makes sense to you and your team.  
Example: `Purchases with Order Total Over $1,000`
* **Condition**  
Each feed requires one or more conditions that filters it out of the **All Events** feeds. Use the values of your event attributes to build simple rules that identify a certain type of event.  
Example:  
    ```none
    tealium_event EQUALS &#34;purchase&#34;
    AND
    order_total IS GREATER THAN 1000
    ```
* **View in Live Events**  
After you create a feed, view it in **Live Events** to display only those events. This interface is helpful for debugging, creating new event specifications, or just monitoring the health of your feeds.
* **Use in connectors**  
After an event feed is created, use it in a connector to send data to a vendor. This is the API hub in action.

## Example

Here is an example of an event feed that identifies `search` events that had `0` results. This feed could be used to monitor the health of your search engine and/or help to improve your search capabilities.

Notice that the feed contains two conditions:

* `tealium_event EQUALS &#34;search&#34;`
* `search_results EQUALS 0`

Example event feed: **Search with No Results**

![](/images/server-side/getting-started-eventstream-event-feed-example.png)

In the next tutorial, you will learn how to add an event feed.