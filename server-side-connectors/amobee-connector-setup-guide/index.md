---
title: Amobee Connector Setup Guide
description: This article describes how to set up the Amobee connector.
url: https://docs.tealium.com/server-side-connectors/amobee-connector-setup-guide/
---

Amobee is a global digital marketing technology company and a wholly-owned subsidiary of Singtel.

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add user to category| ✓| ✗|
|Remove user from category| ✓| ✗|

## How it works

Amobee unifies audiences to drive customers’ growth for brands, agencies, and media companies so they can optimize results across all TV, connected TV, and digital and social media. This integration relies on ID syncing to ingest data into the Amobee DMP from Tealium with a server-to-server format. The Amobee Cookie Matching Service tag available within the Tealium iQ platform makes this happen.

For more information, please see how to configure the [Amobee Cookie Matching Service tag]().

This ID sync value will be passed as a User ID to Amobee to subscribe a user to Categories available within the Amobee taxonomy in this Connector configuration.

The Amobee taxonomy file is an Excel document (`.xls/xlsx` format) that helps to categorize data into a meaningful format, and can be accessed by reaching out to your Amobee account contact. The categories within the taxonomy can be structured to form a hierarchy that includes parent and child categories. Through this connector, you will be able to add users to this category hierarchy.

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Add user to category

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Amobee User ID| ID obtained through the Amobee Cookie Sync Tag or a mobile device ID.|
|Category IDs| A list of Amobee Category IDs.|
|Amobee Pixel ID| Overwrites the pixel ID set in the connector configuration.|

### Action — Remove user from category

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Amobee User ID| ID obtained through the Amobee Cookie Sync Tag or a mobile device ID.|
|Category IDs| A list of Amobee Category IDs.|
|Amobee Pixel ID| Overwrites the pixel ID set in the connector configuration.|
