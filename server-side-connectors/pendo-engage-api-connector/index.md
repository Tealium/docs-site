---
title: Pendo Engage API Connector Setup Guide
description: This article describes how to set up the Pendo Engage API connector.
url: https://docs.tealium.com/server-side-connectors/pendo-engage-api-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Pendo API
* API Version: v1.0
* API Endpoint: `https://app.pendo.io/data/track`
* Documentation: [Pendo API](https://engageapi.pendo.io/?bash#e45be48e-e01f-4f0a-acaa-73ef6851c4ac)

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send a Track Event | ✗ | ✓ |

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Track Event Secret Key**  
 (Required) To obtain the Track Event Secret Key, follow these steps: go to your Pendo dashboard and select **Settings**. Click on **Subscription Settings** in the menu. Choose your app and, under **App Details**, copy the **Track Event Shared Secret**.

## Action Settings - Parameters and Options

Enter a name for the action and select the action type from the drop-down list.

The following section describes how to set up parameters and options for each action.

### Action - Send a Track Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event | (Required) Name of the action that a user has performed. |
| Visitor ID | (Required) Unique string identifier for the visitor. |
| Timestamp | (Required) Time (in milliseconds after the epoch) that the event occurred. |
| Account ID | (Recommended) Unique string identifier for the account to which the visitor belongs. |
| Properties | Free-form object of properties of the event. |
| IP | (Recommended) Current user's IP address. |
| User Agent | (Recommended) User agent of the device making the request. |
| URL | URL of the current page in the browser. |
| Title | Title of the current page in the browser. |
    