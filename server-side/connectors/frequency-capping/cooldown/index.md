---
title: Cooldown groups
description: This article describes how to use cooldown groups in frequency capping.
url: https://docs.tealium.com/server-side/connectors/frequency-capping/cooldown/
---
Cooldown groups define how frequency-capped actions interact with each other.

Actions assigned to the same cooldown group share a cooldown period. When one action in the group triggers, other actions in that group are temporarily suppressed.

## Add a new cooldown group

When you create a cooldown group, it becomes available to all frequency-capped actions in your profile.

![](/images/server-side/connectors/frequency-capping/whiteui-tiq-actionfrequencyandcapping-adding-a-new-cooldown-group.png)

To create a cooldown group:

1. In the admin menu, click **Manage Cooldown**.
1. Click **Add New**.
1. In the **Group Name** field, enter a unique name to identify this group.
1. From the **Color** drop-down list, select a color used to identify the group.
1. In **Wait Time Between Actions (Hours)**, enter a custom value (in hours) or select **6**, **12**, **24**, or **48** hours.
      This value determines how long the system waits before another action in the same group can trigger.
1. Click **Save Changes**.

## Using the default cooldown group

![](/images/server-side/connectors/frequency-capping/whiteui-tiq-actionfrequencycappingandprioritization-default-cooldown-group.png)

The default cooldown group applies to frequency-capped actions when no other cooldown is configured in your profile. You can modify the color and duration settings of the default group, but you cannot change its name.

## Choosing cooldown groups

Use cooldown groups to define how actions should interact.

Assign actions to the same cooldown group when they need to share the same frequency limit.

For example, if several promotional campaigns should send no more than one message within 24 hours, assign those actions to the same cooldown group to enforce that limit.

When a visitor qualifies for multiple actions in that group, the system selects the highest-priority action and suppresses the others during the cooldown period.

Use different cooldown groups when actions should operate independently. Common scenarios include:

* Different communication channels, such as email, SMS, or push notifications.
* Different business purposes, such as transactional and marketing messages.
* Situations where multiple actions should be able to trigger within the same time window without competing with each other.

## Apply a cooldown group to a connector action

You can apply a cooldown group to one or more frequency-capped actions in the same connector.

To apply a cooldown group to an existing action:

1. In the sidebar, go to **Connectors &gt; Overview**.
1. Click a connector to expand its details.  
1. Select the **Actions** tab and choose the action to configure.
   The action must use visitor data and an audience source.
1. Click the **Source** tab.
1. Scroll to **Frequency Cap** and turn it on.
1. Under **Action Priority**, use the up or down arrow to assign a priority number.  
      Do not set this value to zero or a negative number. Assign the priorities in increments of 10 instead of consecutive numbers. This makes it easier to insert a new action later without having to update the priority values for other actions.
1. Under **Action Cooldown Group**, select the cooldown group.  
      ![](/images/server-side/connectors/frequency-capping/whiteui-audiencestream-actionfrequencycappingandprioritization-select-action-cooldown-group-for-connector.png)
1. Click **Done**.
1. Save and publish your profile.