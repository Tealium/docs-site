---
title: Audiences
description: This document provides information about audiences and describes how to create an audience.
url: https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/audiences/
---
An audience is a group of visitors identified by a shared set of attributes. The conditions for an audience specify the attribute values for visitors in that audience. The more conditions you add, the more specific your audience becomes. Audiences are dynamic, meaning visitors can join or leave audiences as events come in from active visitor sessions.

![](/images/server-side/audiencestream-audience.jpg)

The more conditions you use to create an audience, the more specific it becomes. Audiences are used to trigger vendor actions (connectors) in real-time.

The following example creates a basic VIP audience using [the previously created badge](). Since we’re targeting this audience with an email campaign, we’ll also check for a known email address. Finally, we’ll show how to expand the audience with additional conditions.

## Create an audience

Use the following steps to create an audience:

1. Go to **Activate &gt; Audiences** and click **&#43; Add Audience**.
1. Enter a **Name** to uniquely identify the audience, such as `VIP`. If you use a [DataAccess]() product (EventStore, AudienceStore, EventDB, or AudienceDB), the audience name must be fewer than 128 characters in length. Otherwise, DataAccess may trim the audience name and errors may occur.
1. Use the **Conditions** drop-downs to create a filter:
    ```
    VIP (badge) is assigned
    AND
    Has Email Address is assigned
    ```
1. Click **Save**.
1. Save and publish your account.

This audience contains visitors who have the VIP badge assigned. You can now take action on these **VIP** customers using connectors. You could further refine this audience by creating more visitor attributes and defining additional conditions. Here are some examples:

* **VIP - Recent Purchasers (or Past Purchasers)**  
Combine the **VIP** badge with a **Last Purchase Date** attribute to create an audience of your best customers that have purchased recently (or not so recently).
* **VIP - iOS Fans (or Android Fans)**  
Combine the **VIP** badge with the **Lifetime operating systems used (favorite)** attribute to create an audience that targets specific device users.

Click **Next** to learn how to activate your audiences with connectors.
