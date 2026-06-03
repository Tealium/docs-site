---
title: RTB House Connector Setup Guide
description: This article describes how to set up the RTB House connector.
url: https://docs.tealium.com/server-side-connectors/rtb-house-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:
* **RTB House Partner Key**  
  * A unique identifier assigned to your organization by RTB House. This key is required to authenticate your integration. Contact your RTB House account manager to obtain it.
* **RTB House Tagging Hash**  
  * A unique hash used by RTB House to correctly associate tagging events with your account. Contact your RTB House account manager to retrieve your Tagging Hash value.
* **RTB House Region**  
  * The regional subdomain your RTB House account is associated with. This ensures proper routing of events and requests. If you&#39;re unsure of your region, contact your RTB House account manager.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Code | Available options are: &lt;ul&gt;&lt;li&gt;**Home** - For visiting the home page of your website.&lt;/li&gt;&lt;li&gt;**Category2** - For visiting a category page.&lt;/li&gt;&lt;li&gt;**Offer** - For visiting a product page.&lt;/li&gt;&lt;li&gt;**Listing** - For visiting a search result page.&lt;/li&gt;&lt;li&gt;**Basket add** - For adding a product to the cart.&lt;/li&gt;&lt;li&gt;**Basket status** - For displaying the shopping cart page.&lt;/li&gt;&lt;li&gt;**Start order** - For visiting the page that begins order processing, such as a checkout page.&lt;/li&gt;&lt;li&gt;**Conversion Order** - For the order confirmation page.&lt;/li&gt;&lt;/ul&gt; |

#### Event Attributes

| **Parameter** | **Description** |
| --- | --- |
| UID | Anonymous user ID (same as used on Web Pixel). |
| Time | Time of the event in milliseconds since the UNIX epoch (January 1, 1970 00:00:00 UTC). |
