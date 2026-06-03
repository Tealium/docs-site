---
title: Adition PostTracking Setup Guide
description: This article describes how to set up the Adition PostTracking connector.
url: https://docs.tealium.com/server-side-connectors/adition-posttracking-connector/
---
This article describes how to set up the Adition PostTracking connector.

## API Information

This connector uses the following vendor API:

* API Name: Adition API
* API Endpoint: `http://adfarm1.adition.com/trackdata`

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **TrackingSpot ID (SID)**  
  * Internal ID for the TrackingSpot.
* **LandingPage ID (TID)**  
  * Internal ID for the LandingPage.
* **Adition instance**  
  * (Optional). Specify the Adition server farm you are running on. This will be added as a prefix to the base URL: `https://{adition_instance}.adfarm1.adition.com.`

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Track event | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Track event

#### Tracking Parameters

| **Parameter** | **Description** |
| --- | --- |
| kid | Campaign ID. |
| bid | Banner ID. |
| wp_id | Content unit ID. |

#### Revenue Tracking Parameters

| **Parameter** | **Description** |
| --- | --- |
| orderid | Unique identifier for the order. |
| itemno | Unique identifier for the item. |
| quantity | Number of items ordered. |
| descr | Description of the item. |
| price | Price per item. |
| total | Total price for the quantity ordered. |