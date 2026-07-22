---
title: RTB House Connector Setup Guide
description: This article describes how to set up the RTB House connector.
url: https://docs.tealium.com/server-side-connectors/rtb-house-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:
* **RTB House Partner Key**  
  * A unique identifier assigned to your organization by RTB House. This key is required to authenticate your integration. Contact your RTB House account manager to obtain it.
* **RTB House Tagging Hash**  
  * A unique hash used by RTB House to correctly associate tagging events with your account. Contact your RTB House account manager to retrieve your Tagging Hash value.
* **RTB House Region**  
  * The regional subdomain your RTB House account is associated with. This ensures proper routing of events and requests. If you're unsure of your region, contact your RTB House account manager.

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
| Event Code | Available options are: <ul><li>**Home** - For visiting the home page of your website.</li><li>**Category2** - For visiting a category page.</li><li>**Offer** - For visiting a product page.</li><li>**Listing** - For visiting a search result page.</li><li>**Basket add** - For adding a product to the cart.</li><li>**Basket status** - For displaying the shopping cart page.</li><li>**Start order** - For visiting the page that begins order processing, such as a checkout page.</li><li>**Conversion Order** - For the order confirmation page.</li></ul> |

#### Event Attributes

| **Parameter** | **Description** |
| --- | --- |
| UID | Anonymous user ID (same as used on Web Pixel). |
| Time | Time of the event in milliseconds since the UNIX epoch (January 1, 1970 00:00:00 UTC). |
