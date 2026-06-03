---
title: Veeva CRM Connector Setup Guide
description: This article describes how to set up the Veeva CRM connector.
url: https://docs.tealium.com/server-side-connectors/veeva-crm-connector/
---
## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
| --- | --- | --- |
| Insert into Custom Object | ✓ | ✗ |
| Update Custom Object | ✓ | ✗ |

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](/server-side/connectors/manage/) article.

After adding the connector, configure the following settings:

*   **Endpoint URL**  
(Required) Provide the endpoint URL. Default URL is `https://login.salesforce.com/services/oauth2/authorize`
*   **Establish** **Connection**  
Click **Establish Connection** to connect to your Salesforce account.

Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Insert into Custom Object

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Custom Object Name | Name of custom object. |
| Insert Data Map | Insert data map configured in Salesforce. |

### Action — Update Custom Object

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Custom Object Name | Name of custom object. |
| Lookup Data Map | Select attribute to look up custom object by. |
| Update Data Map | Update data map configured in Salesforce. |