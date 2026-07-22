---
title: Delayed actions
description: This article provides information about delayed connector actions and how they work.
url: https://docs.tealium.com/server-side/connectors/delayed-actions/
---
## How it works

A delayed action is an AudienceStream connector action that is delayed based on a set of conditions or time criteria. A delayed action can be configured for an AudienceStream connector when the trigger is set to **In Audience at the end of visit**, as shown in the following example:

![](https://docs.tealium.com/images/server-side/001.png) 

A delay can be scheduled for an action for a specific number of hours or days and is scheduled only if the visitor is in the audience at the end of current visit. The delayed action is triggered only if the visitor is still in the audience at the scheduled activation time.

If a visitor returns for a second visit after a delayed action has been triggered, and the visitor meets the condition **In Audience at the end of visit** when the second visit ends, then a new delayed action is scheduled.

This article uses the following terms:

* **Scheduling time** - The time at the end of a visit when connector actions are scheduled for delayed activation.
* **Activation time** - The time after the delay when connector actions are triggered.
* **In Audience at end of visit** - The visitor is in the selected audience when the visit ends.

The end of a visit is determined by user inactivity. For more information, see [Session length](https://docs.tealium.com/server-side-session-length/).

Delayed actions can only be scheduled for activated connectors. To learn more about audience connectors and the trigger setting, see [Add a Connector](https://docs.tealium.com/server-side/connectors/add/#select-a-source-for-audiencestream).

### How delayed actions are scheduled and processed

Scheduled actions are checked at regular intervals to determine which of the scheduled actions have expired and are ready to be triggered, as shown in the following figure:
![](https://docs.tealium.com/images/server-side/connectors-process-delayed-action-flow.png)

The activation time (the time at which the action is triggered) is based on the time delay you specify.

At activation time, the visitor profile is evaluated again to verify that the visitor is still in the audience. If the visitor is in the audience and the action frequency has not been capped, the delayed action is triggered.


<blockquote>
If the connector or action is changed between the scheduling time and the activation time, the changes could prevent triggering the action. For more information, see [Changing a connector after delayed actions are scheduled]().
</blockquote>


### Supported attribute types

Delayed actions only work on audiences with conditions that use visitor-scoped attributes and can send only visitor attribute data. Visit attributes are not supported because the data stored in these attributes only persists for the length of the visit.

In addition, the audience that triggers the delayed action should not use visit attributes. When the visitor profile is re-evaluated at activation time, and the audience uses visit attributes, the visitor may no longer be in the audience.


<blockquote>
No error or warning is generated if you configure a delayed action for an audience that uses visit attributes.
</blockquote>


## Delay an action for hours or days

To delay an action for a specific number of hours or days, use the **DELAY Action for 1 Days** option. If a visitor is in the audience when the visit ends, a delayed action is scheduled for the specified time period. In the following example, the action would be scheduled for the following day if the visitor is in the audience.

![](https://docs.tealium.com/images/server-side/002.png)

If the visitor returns for a second visit 12 hours after the first visit ended AND the visitor meets the condition **In Audience at end of visit** when the second visit ends, then the original delayed action will be rescheduled to 1 day (24 hours) after the second visit ends. In other words, the delayed action is now scheduled to 36 hours after the first visit ends.

The maximum allowed delay for an action is 365 days or 8760 hours. The number of days or hours must be a whole number, decimal values such as `1.5` or `0.75` are not allowed. The smallest delay that can be configured is 1 hour.

## Delay an action only if the visitor joined the audience during the current visit

The **In Audience at the end of visit** condition is easily met, and may include visitors that were in the audience at the start of the visit. The **AND was not a member of this Audience at start of visit** option can be used to schedule a delayed action only if the visitor is in the audience at the end of the visit AND the visitor joined the audience during this visit.

![](https://docs.tealium.com/images/server-side/003.png)

## Changing a connector after delayed actions are scheduled

A connector or an action could be changed between the scheduling time and the activation time. How the changes affect a delayed action depends on what was changed, as follows:

* The values of visitor attributes have changed.  
The attribute values at activation time are used in the connector action.
* The audience criteria for the audience associated with the connector action was changed.  
The visitor profile is reevaluated at activation time to see if it remains in the audience. If the visitor does not meet the current audience conditions, the action is not triggered.
* The connector action was changed to use a different audience.  
The connector action is not triggered. The audience ID for the connector action must be the same at scheduling time and activation time.
* The delay period was changed.  
This does not have any effect on already scheduled delayed actions.
* The connector action was deactivated.  
This does not affect already scheduled delayed actions. They will still trigger. Deactivating a delayed connector action only prevents new delayed actions from being scheduled.
* The connector action was deleted.  
Scheduled delayed actions will not trigger because their configuration cannot be retrieved.
* The connector action was changed in some other way (for example, the attributes mapped have been changed).  
The connector configuration at activation time (not scheduling time) is used.