---
title: Add an Event Feed
description: This step shows how to create an event feed to capture search events that contain zero results.
url: https://docs.tealium.com/server-side/getting-started/eventstream-api-hub/add-feed/
---
## Create a feed

To create an event feed:

1. Go to **Validate &gt; Live Events** and click **&#43; Add Event Feed**.  
1. Set the **Title**, **Notes**, and **Labels**.  
Ignore **Event Data Storage** for now, since this setting requires your account to be enabled for [DataAccess]().
1. Set the conditions for the feed:
    * Select an event attribute from the drop-down menu.
    * Select an operator.
    * Select another attribute, or Custom Value then enter a value.  
    ![](/images/server-side/getting-started-eventstream-event-feed-condition.png)
    * Repeat this for additional AND/OR condition logic.
1. Click **Save**.
1. Save and publish your account.

## Revisit Live Events

Now that you have event specs and feeds set up, it&#39;s a good time to revisit your installation to send more events so you can see how they appear in **Live Events**.

Here are some things to try to get more familiar with **Live Events** and feeds:

* Send `search` events without other attributes. Do they appear red, green, or blue in **Live Events**?
* Send `search` events with all required attributes. Are they valid in **Live Events**?
* In the **Live Events** drop-down for **Event Feeds**, select your new feed. Trigger more events to get them to appear in this view.

After you&#39;re familiar with event feeds, go to the next tutorial to learn about connectors and how they work.