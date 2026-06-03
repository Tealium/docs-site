---
title: About audiences
description: This article provides information about audiences, segments, and visitor retention time.
url: https://docs.tealium.com/server-side/audiences/about/
---
Tealium AudienceStream CDP Audiences provides a streamlined and powerful audience management experience with the following features:
* The ability to create a set of conditions to define a dynamic, real-time audience.
* The ability to connect an audience to a connector and define triggers that determine when connectors are fired.
* The ability to save frequently used audience segments (groups of conditions) and reuse them in other audiences.

## How it works

An audience is a group of visitors identified by a shared set of attributes. The conditions for an audience specify the attribute values for visitors in that audience. The more conditions you add, the more specific your audience becomes. Audiences are dynamic, meaning visitors can join or leave audiences as events come in from active visitor sessions.

The **Audiences** page has the following tabs:
* **Audiences**: Displays the list of audiences in the profile.
* **Segments**: Displays the list of saved segments. For more information, see [Saved segments]().

## Audience details

When you select an audience on the **Audiences** page, the audience details page is displayed and has the following tabs:  
* **Configuration**: Displays the audience conditions and lets you edit the conditions.
* **Insights**: Displays graphs of visitors and audience activity, refreshed every day at 12 AM UTC. The time period for the graphs can be one of the following: **Today**, last 7 days (**7D**), last 30 days (**30D**), last 2 months (**2M**), or last 3 months (**3M**). The default time period is **7D**.
    * The **Visits** graph shows the number of visits in the selected time period where the visitor joined or is already part of the audience.   
    * The **Activity** graph shows the number of visitors that left (orange bar) or joined (green bar) the audience per day. The following figure shows an example of **Insights** graphs:  
    ![](/images/server-side/audience-insights.png) 
* **Activations**: Displays a list of activations for the audience and lets you edit, activate, or deactivate activations.
* **Functions**: Displays a list of the functions that are triggered by the audience.

## Audience conditions and segments

An audience is created by defining one or more conditions using visit or visitor attributes. An audience segment is a set of conditions that can be saved and used as a building block in multiple audiences.

Segments can be layered with AND or OR logic to create an audience. You can use excluding logic to remove visitors that meet the audience conditions. Visitors that meet these audience conditions are added or removed from an audience in real-time based on user-generated events.

### AND logic example

This example shows a segment for visitors who have spent over $1000 and have the Fan badge, which combines the following conditions with AND logic:

* `Fan badge is assigned`
* `lifetime_spending is greater than 1000`

![](/images/guides/server-side/int-aud-fan-spent-1000.png)

### OR logic example

Additional visitors can be added to an audience by combining segments with OR logic. If two segments are combined with OR logic, visitors that match the conditions for either segment are included in the audience.

This example shows a segment for visitors with the `Fan` badge or visitors who have spent over $500, which combines the following conditions with OR logic:

* `Fan badge is assigned`
* `lifetime_spending is greater than 500`

![](/images/guides/server-side/int-aud-fan-or-spent-500.png)

### Excluding logic example

To exclude specific visitors from an audience, use excluding logic. For example, to create an audience of frequent visitors that have not visited in the last three days, you could combine the following conditions with excluding logic:

* `Frequent visitor is assigned`
* `Days since last visit is less than 4`

![](/images/guides/server-side/int-aud-excluding-logic.png)

## Saved segments

Saved segments can be used in multiple audiences, avoiding the need to create the same conditions for each audience. You can save segments while you are adding conditions to an audience, as shown in the following figure:
![](/images/guides/server-side/audiences-save-a-segment.png)

You can also create segments on the **Segments** tab on the **Audiences** page. After you save or create a segment, it is automatically saved. Save and publish is not required. For more information, see [Manage segments]().

Segments are only evaluated when they are used in an audience and the audience is evaluated. Segments are not available in Data Layer Enrichment (DLE) as part of a visitor profile. Segments are used in audiences and the audiences a visitor has joined are returned as part of DLE.

Segments used in audiences cannot be edited.

### Segment examples

**Example 1: Audience of loyalty members who have previously purchased and have abandoned their cart**

In this example, two saved segments are used to create an audience of loyalty members who have previously purchased and have abandoned their cart. The loyalty members segment has the following conditions:
![](/images/server-side/audiences-segment-loyalty.png)

The cart abandoned and have previously purchased segment has the following conditions:
![](/images/server-side/audiences-segment-abandoned-purchases.png)

The audience of loyalty members who have previously purchased and have abandoned their cart uses these two segments, as follows:
![](/images/server-side/audiences-loyal-purchases-abandoned.png)

**Example 2: Audience of loyalty members who have not visited in the last 60 days**

This example uses the loyalty members segment from the previous example and the following segment for visitors with no visits in the last 60 days that checks to see if the **Last Visit** attribute is greater than 60:
![](/images/server-side/audiences-segment-last-visit-60days.png)

The `Loyalty member, no visits in last 60 days` audience uses both of these segments as follows:
![](/images/server-side/audiences-loyal-novisit-60d.png)

### Favorite segments

You can save segments to your favorites on the **Segments** tab, which lets you filter on favorites for easy access to frequently used segments. For example:
![](/images/guides/server-side/audiences-favorites-example.png)

You can filter the list of segments by **Favorites** and only favorite segments are displayed. For example:
![](/images/guides/server-side/audiences-filter-segments-example.png)

## Visitor retention time

Visitor retention time refers to how long Tealium AudienceStream retains visitor profiles after their last recorded activity. Each incoming event associated with a visitor profile resets the retention timer. If a visitor remains inactive for the length of the retention period, their profile is permanently deleted from the system.

Retention time is specified in two places:

* **Profile Retention Time** in [Server-side account settings](), which is set for the account and cannot be modified.

* **Audience Retention Time** overrides the profile retention time for a specific audience. You cannot modify this setting. Contact Tealium Support to request changes.

The retention time applied to a visitor is determined by one of the following:

* **Longest audience retention time**  
    If the visitor is a member of multiple audiences with a retention time specified, the longest retention time is used, even if it is shorter than the profile retention time.

* **Profile retention time**  
    If the visitor is not a member of any audiences with a retention time specified, then the profile retention time is used.

The maximum allowed profile and audience retention times are determined by your contract terms.

### Example

If your account has a profile retention time of 395 days, all visitor profiles with a last event activity timestamp older than 395 days are removed from AudienceStream. This means the entire visitor profile is deleted. If that same visitor returns and triggers event activity, AudienceStream creates a new visitor profile for them.

To store visitor profiles longer than your account or profile retention period, the visitor must belong to an audience that has a longer retention time.

The following example illustrates how visitor profile retention works with audiences that have longer and shorter retention times than the profile retention time.

* **Profile Retention Time**: 395 days
* **&#34;Window Shopper&#34; audience retention time**: 30 days
* **&#34;VIP Purchaser (&gt; $500)&#34; audience retention time**: 400 days

|Action| Day| Days Inactive| &#34;Window Shopper&#34;| &#34;VIP Purchaser&#34;| AudienceStream|
|---| ---| ---| ---| ---| ---|
|Visits Website,&lt;br&gt; browses products| May 1, 2024 | 0 | ✓ Added| | ✓ New profile |
|N/A| May 31, 2024 | 30| ✗ Removed | | ✗ Removed|
|Visits Website,&lt;br&gt; Purchases $550| Aug 1, 2024 | 0 | | ✓ Added| ✓ New profile |
|N/A| Aug 31, 2025 | 395| | ✓ Retained| ✓ Retained|
|N/A| Sep 5, 2025| 400| | ✗ Removed| ✗ Removed|