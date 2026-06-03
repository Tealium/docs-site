---
title: Install the Tealium app in Shopify
description: This article provides information about installing the Tealium Shopify app.
url: https://docs.tealium.com/platforms/shopify/install/
---
Before you install and configure the Tealium Shopify app, configure the following in Tealium:

* Tealium HTTP API data source
* Event specifications
* A data layer `restock` variable

For information about these configuration tasks, see [Tealium configuration]().

## Installation

The following sections provide instructions for installing the Tealium App in Shopify, enabling the Shopify theme, and configuring the Checkout Pixel.

### Install the Tealium app

1. In Shopify under **Apps**, select the **Tealium** app.
1. On the **Config** tab, enter your **Account**, **Profile**, and **Environment** information.  
    Environment values are `prod`, `dev`, or `qa`.
1. Select a **Checkout Tracking** option:  
    * **Client Side Only**: Select this option if you only have Tealium iQ Tag Management.
    * **Client and Server Side**: Select this option if you use Shopify Webhooks to send data to EventStream.
1. If you selected **Client and Server Side**, do the following:  
    1. In Tealium, go to **Server-Side &gt; Data Sources**, and select the data source you created for Shopify.  
    1. Copy the **Data Source Key** for the selected data source.  
    1. In Shopify, paste the data source key into the **Server Side Data Source ID** field. 
1. Click **Submit** when you have finished the configuration. Webhooks are immediately created.

### Enable the Shopify theme

Use the following steps to enable the Shopify theme:

1. In Shopify, go to **Online Store &gt; Themes &gt; Customize**.
1. Click **App Embeds** and enable the Tealium extension.  
This loads the Tealium library `utag.js` and the standard data layer for Shopify events.
1. Set **Tealium Settings** to `On`.
1. Click **Save**.

### Configure the checkout pixel

The Tealium app uses a custom checkout pixel to send checkout event data to EventStream. If you do not have EventStream enabled, you do not need to configure the checkout pixel.

Use the following steps to configure the Checkout Pixel: 

1. In **Shopify Admin**, go to **Settings &gt; Customer Events**.  
You will see the Tealium pixel that the Tealium app has installed. The checkout pixel must be added manually.
1. Click **Add Custom Pixel** and enter `Tealium Checkout` for the **Pixel Name**.
1. Under **Customer Privacy**, the recommended options are as follows:
    * **Permission**: select **Analytics**.
    * **Data sale**: select **Data collected does not qualify as data sale**.  
    This may change depending on the data your store is collecting in Tealium. 
1. Delete the example code shown in the **Code** box.
1. Paste the code copied from the **Customer Events** tab into the **Code** box.  
1. Click **Save**.
1. Click **Connect**.

## Privacy and consent

The Tealium app uses a custom template for consent integrations that makes use of the [Shopify Customer Privacy API](https://shopify.dev/docs/api/customer-privacy). This section shows how to configure the recommended approach to consent management and privacy with Shopify. 

For more information, see [About consent integrations]().

The Tealium Shopify app can use the built-in Shopify cookie banner and the Shopify Privacy platform. Use client-side consent integrations to configure third-party banners or other consent management platforms.

### Configure client-side consent integrations

Configuration of client-side consent integrations consists of the following:

* Create a purpose group and purposes
* Map tags to purposes
* Add a consent integration for Shopify

#### Create a purpose group and purposes

To add a consent integration for Shopify, create a purpose group and one or more purposes. Each purpose you create requires a name and a key. The name must correspond to one of the Shopify consent categories. The following table shows the keys and names for Shopify consent purposes:

| Key | Name |
|----|----|
| `analytics` | `analytics` |
| `marketing` | `marketing` |
| `preferences` | `personalization/preferences` |
| `sale_of_data` | `sale_of_data` |

Assign the appropriate Tealium iQ purpose before mapping tags to the different purposes. For each Tag, select the **Map** drop-down menu and assign the most appropriate purpose for the tag.

For more information about creating a purpose group and purposes, see [Add a purpose group]().

#### Add a custom consent integration

Use the following settings when configuring a custom integration for Shopify:

| Option | Value |
|----|----|
| Name | `Shopify` |
| Vendor | `Custom` |
| Vendor ID | `_tracking_consent` |
| Enforcement Rule | Use the default |
| Publish Locations | &lt;ul&gt;&lt;li&gt;`Dev` for testing&lt;/li&gt;&lt;li&gt;`Prod` when testing is complete&lt;/li&gt;&lt;/ul&gt; |
| Purpose Group | The purpose group created for Shopify. |

For more information about adding a custom consent integration, see [Add an integration]().

## Validate your installation

Shopify Custom Pixels run in an iFrame sandbox that makes most tag monitoring plugins incompatible, including the Tealium Universal Tag Debugger. This section provides information on manually implementing debug mode.

To enable this debug mode, follow these steps:

1. Add a cookie named `tealium_debug` to the page that you are testing.
1. Set the cookie value to `dev`.  
This automatically sets `utagdb=true`, which enables verbose output and loads the Tealium `dev` environment version. 
1. To see the additional output, open the browser console.

Debug mode applies only to the client-side. It cannot be used to validate server-side data collection. 

Debugging of webhooks and events sent to EventStream can be done using the Live Events page in EventStream. The page being tested needs to be reloaded to see the events. This works on the whole site, including checkout. For more information, see [About Live Events]().

1. In **Shopify Admin**, go to **Online Store &gt; Themes &gt; Customize &gt; App embeds**.
1. Enable debugging in the Tealium extension settings and click **Save**.
1. Reload your website and check the browser console to see detailed debugging information.

## Server events management

The **Server Events** tab lets you select which Shopify webhooks are registered for server-side tracking. Enable or disable individual webhooks based on your tracking requirements:

| Tealium Event | Shopify Webhook | 
|----------------|-----------------|
| cart_update | CARTS_UPDATE |
| cart_create | CARTS_CREATE |
| checkouts_create | CHECKOUTS_CREATE |
| purchase | ORDERS_CREATE |
| shopify_refund | REFUNDS_CREATE |
| Shopify New Customer | CUSTOMERS_CREATE |
| sms_consent_change | CUSTOMERS_MARKETING_CONSENT_CREATE |
| email_consent_change | CUSTOMERS_EMAIL_MARKETING_CONSENT_CREATE |

Selected webhooks are automatically registered with Shopify and configured to send data to Tealium EventStream.

## Split cookie mode

Split cookie mode provides more transparency about cookies by writing individual cookies instead of a single combined `utag_main` cookie. Split cookie settings are available if `utag.js` version 4.50 or higher is detected.

To split the combined cookie into individual cookies, use the following steps:

1. Click **Detect utag.js Version** to check your `utag.js` version.
1. Select the **Enable split cookie mode** checkbox.
1. Select which cookie values to keep in the `utag_main` cookie. Unchecked values are written as individual cookies with the `utag_main_` prefix.  
The `ses_id`, `_st`, and `_ss` cookies are required and marked with red badges to prevent visitor/session count inflation.
1. Click **Save Cookie settings**.

## Uninstall the Tealium Shopify app

To remove the Tealium app from Shopify, use the following steps:

1. In Shopify, go to **Visit Settings &gt; Custom data**.
1. In the list, click **Tealium**, which will be near the bottom of the list.  
The Tealium metadata fields will be listed.
1. Scroll down in the list of fields and click **Delete**.