---
title: Manage Context API engines
description: Create and configure Context API engines, including access controls and attribute selection.
url: https://docs.tealium.com/server-side/context-api/manage/
---

<blockquote>
Context API must be enabled for your account before you can create engines. [Contact support](https://docs.tealium.com/support/) to enable it.
</blockquote>


## Create an engine


<blockquote>
Ensure profile changes have been published before selecting engine attributes.
</blockquote>


To create an engine, complete the following steps:

1. Go to **Activate > Context API** and click **+ New Engine**.
1. In the **Details** screen, configure the following engine details:
    * **Name**: Enter a name for the engine.
    * **Enable Engine**: Toggle the engine on and off. The engine endpoint is off by default. Data for visitors becomes available after you enable the engine and visitors log active sessions and generate events in the system.
    
<blockquote>
Authentication and Allow PII are only available by request. If you are interested in trying these features, [contact support](https://docs.tealium.com/support/).
</blockquote>

    * **Authentication**: Controls whether requests to this endpoint require authentication.
        * **Public** (default): Any caller with the engine ID can call the endpoint.
        * **Require Authentication**: Only authenticated clients can call the engine. Unauthenticated requests return a 401 error. Callers must subscribe to the Context API in the Developer Portal and include a bearer token in the `Authorization` header. For more information, see [dev-portal-subscriptions](https://docs.tealium.com/dev-portal-subscriptions/).
    * **Allow PII**: Available only when **Require Authentication** is selected. When on, restricted (PII-marked) attributes are available for selection in the **Response** screen alongside standard attributes. Nothing is selected automatically.
        * Turning off **Allow PII** removes all restricted attributes from the engine immediately. A confirmation dialog lists the affected attributes before the change takes effect. These attributes cannot be restored.
        * Turning off **Allow PII** does not delete previously saved PII. To make previously stored data inaccessible, purge the engine data after turning off **Allow PII**. For more information, see [Purge data](#purge-data).
        * Switching back to **Public** turns off **Allow PII** automatically and triggers the same confirmation dialog.
    * **Domain Allow List**: Specify domains that can use this endpoint. For more information, see [About Context API > Domain allow list](https://docs.tealium.com/about-context-api/#domain-allowlist).
1. Click **Next**.
1. In the **Response** screen, select the audiences, badges, and attributes to include in the engine. Verify your selections using the **Example Response** panel. 
<blockquote>
If you use the **Select all current and future audiences** feature, if an audience is deleted later, it could still be included in the Context API engine until you purge the engine data or the data expires.
</blockquote>

1. Select whether to use the ID (UID) or name for audiences and visitor attributes in the payload. Using audience, badge, and attribute names instead of IDs in large responses  may impact payload size.
1. Click **Next** to create the engine.
1. On the **Summary** screen, review endpoint details, including the unique endpoint URL.
1. Click **Done**. You do not need to publish your profile after creating an engine.

Visitor data is collected after the engine is enabled and your visitors have active sessions.

## Edit engine

To edit an engine, go to the Context API screen and click the engine you want to update. From the edit screen, you can update the engine details and response configuration, purge engine data, toggle engines on and off, and adjust authentication and PII settings.

Turning off **Allow PII** from the edit screen triggers the same confirmation dialog described in [Create an engine](#create-an-engine).


<blockquote>
You do not need to publish your profile after editing an engine. Changes to Context API engines are available five minutes after saving any configuration changes.
</blockquote>


## Purge data

We recommend purging engine data in the following situations:

* Renaming or deleting an audience, badge, or attribute included in your engine configuration.
* Removing an audience, badge, or attribute from an engine configuration.
* Turning off **Allow PII** on an engine. Restricted attributes are removed from future responses immediately, but previously stored data remains in the engine until you purge. Purging makes that data inaccessible.

For more information about purging data, see [About Context API > Purge data](https://docs.tealium.com/about-context-api/#purge-data).

Context API provides two ways for you to purge engine data when needed:

1. In the **Context API** screen, click the action menu next to the engine you want to purge data from and select **Purge Data**.
1. In the **Edit Engines** screen, click **Purge Data** from the slideout actions.

After a data purge, previously stored engine data is no longer returned.
