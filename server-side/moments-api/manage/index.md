---
title: Manage Moments API engines
description: This article describes how to create and manage Moments API engines.
url: https://docs.tealium.com/server-side/moments-api/manage/
---

<blockquote>
Contact your account manager to enable Moments API for your account.
</blockquote>


## Create an engine


<blockquote>
Ensure profile changes have been published before selecting engine attributes.
</blockquote>


To create an engine, complete the following steps:

1. Go to **Activate > Moments API** and click **+ New Engine**.
1. In the **Details** screen, configure the following engine details:
    * **Name**: Enter a name for the engine.
    * **Enable Engine**: Toggle the engine on and off. The engine endpoint is off by default. Data for visitors becomes available after you enable the engine and visitors log active sessions and generate events in the system.
    * **Domain Allow List**: Specify domains that can use this endpoint. For more information, see [About Moments API > Domain allow list](https://docs.tealium.com/about-moments-api/#domain-allowlist).
1. Click **Next**.
1. In the **Response** screen, select the audiences, badges, and attributes to include in the engine. Verify your selections using the **Example Response** panel. 
<blockquote>
If you use the **Select all current and future audiences** feature, if an audience is deleted later, it could still be included in the Moments API engine until you purge the engine data or the data expires.
</blockquote>

1. Select whether to use the ID (UID) or name for audiences and visitor attributes in the payload. Using audience, badge, and attribute names instead of IDs in large responses  may impact payload size.
1. Click **Next** to create the engine.
1. On the **Summary** screen, review endpoint details, including the unique endpoint URL.
1. Click **Done**. You do not need to publish your profile after creating an engine.

Visitor data is collected after the engine is enabled and your visitors have active sessions.

## Edit engine

To edit an engine, go to the Moments API screen and click the engine you want to update. From the **Edit Engine** screen, you can update the engine details and response configuration, purge engine data, and toggle engines on and off as needed.


<blockquote>
You do not need to publish your profile after editing an engine. Changes to Moments API engines are available five minutes after saving any configuration changes.
</blockquote>


## Purge data

If a user deletes or renames an audience, badge, and attribute used in an engine, it may cause unexpected results in the endpoint responses. In these cases, you may want to consider purging the engine data. For more information about purging data, see [About Moments API > Purge Data](https://docs.tealium.com/about-moments-api/#purge-data).

Moments API provides two ways for you to purge engine data when needed:

1. In the **Moments API** screen, click the action menu next to the engine you want to purge data from and select **Purge Data**.
1. In the **Edit Engines** screen, click **Purge Data** from the slideout actions.

After a data purge, previously stored visitor data will not be available.

