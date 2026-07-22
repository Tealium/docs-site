---
title: Configure EventStore
description: This article provides information about enabling an event feed for EventStore.
url: https://docs.tealium.com/server-side/data-storage/audiencestore-eventstore/configure-eventstore/
---

<blockquote>
To have EventStore enabled for your account and profile, contact your account manager.
</blockquote>


## Enable an event feed for EventStore
1. Navigate to **Validate > Live Events**.
1. Select an event feed and click **Edit**.  
1. Set **Event Data Storage** to `EventStore`.
1. Save and publish.


<blockquote>
If EventStore is disabled for a profile, EventStore is disabled for all event feeds. If EventStore is enabled again, the event feeds must be manually enabled again.
</blockquote>


After enabling an event feed, go to **Store > EventStore** to view and download JSON files. Each JSON file contains a list of events from EventStream. You can also use third-party tools to view the files. For more information, see [View files]().