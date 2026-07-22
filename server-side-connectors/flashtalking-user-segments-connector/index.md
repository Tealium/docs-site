---
title: Flashtalking User Segments Connector Setup Guide
description: You can use the Flashtalking connector to add users to segments created in the Flashtalking Pixel Manager. These segments can then be targets using a Decision Tree or Hedge import in the Campaign Manager or Creative Manager interface.
url: https://docs.tealium.com/server-side-connectors/flashtalking-user-segments-connector/
---
For additional information, log into your Flashtalking account and go to [Flashtalking: Tealium Integration.](https://flashtalkingsupport.zendesk.com/hc/en-us/articles/360043723153-Tealium-Integration)

## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
| --- | --- | --- |
| Add User to Segment | ✓ | ✓ |
| Remove User from Segment | ✓ | ✓ |
| Remove User from All Segments | ✓ | ✓ |

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/server-side/connectors/manage/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

*   **Advertiser ID:** Find your Advertiser ID within the Flashtalking Pixel Manager.
*   **Username:** Enter the username you use to log into the Flashtalking hub.
*   **Password:** Enter the password you use to log into the Flashtalking hub.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Add User to Segment

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| DAID | Android advertising ID. |
| IDFA | Apple advertising ID. |
| UID | Unique ID from cookie sync. |
| Segment(s) | Identify the target segments by the segment string. Pass either a single segment or a comma separated list of segments. If you pass a list of segments, do not include brackets "`[]`". |

### Action - Remove User from Segment

### Parameters

| **Parameter** | **Description** |
| --- | --- |
| DAID | Android advertising ID. |
| IDFA | Apple advertising ID. |
| UID | Unique ID from cookie sync. |
| Segment(s) | Identify the target segment(s) by the Segment String. Pass either a single segment or a comma separated list of segments. If you pass a list of segments, do not include brackets "`[]`". |

### Action - Remove User from All Segments

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| DAID | Android advertising ID. |
| IDFA | Apple advertising ID. |
| UID  | Unique ID from cookie sync. |