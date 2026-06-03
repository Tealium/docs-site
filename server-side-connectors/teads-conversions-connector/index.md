---
title: Teads Conversions Connector Setup Guide
description: This article describes how to set up the Teads Conversions connector.
url: https://docs.tealium.com/server-side-connectors/teads-conversions-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Teads Conversions API
* API Version: v1
* API Endpoint: `https://ca.teads.tv/`

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:
* **Conversion API Token**  
  * To generate the Conversion API Token, go to the settings panel, click **Conversion API Tokens &gt; Generate Conversion API Token**.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Conversion Event | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Conversion Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event ID (`auctid`) | Unique identifier for the event. Can be retrieved from `URL` (`auctid` parameter) or cookies (`tfpai`). |
| Buyer Pixel ID | `ID` of the pixel installed on the website. |
| Event Source URL | `URL` of the page visited by the user. |
| Conversion Type | Type of conversion event: `pageView`, `AddToCart`, `AddToWishlist`, `CompleteRegistration`, `InitiateCheckout`, `Lead`, `Purchase`, `Search`, `ViewContent`. The default is `pageView` event. |
| Event Time | Timestamp of the event in epoch seconds. |

#### Conversion Parameters

| **Parameter** | **Description** |
| --- | --- |
| Name | (string) The name, up to `100` characters. |
| Price | (decimal) The monetary price, in units of the specified currency parameter. |
| Currency | (string) A three-letter `ISO 4217` currency code representing the currency. |

#### First Party Cookies

| **Parameter** | **Description** |
| --- | --- |
| `tfpai` | Contains the `auctid` value. |
| `tfpvi` | Contains the user identifier. |
| `tfpsi` | Contains the user session `ID` that is used to compute the user session. |

