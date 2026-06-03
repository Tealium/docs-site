---
title: Microsoft Fabric Eventhouse connector
description: This article describes how to set up the Microsoft Fabric Eventhouse connector.
url: https://docs.tealium.com/server-side-connectors/microsoft-fabric-eventhouse-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Tenant ID**  
  * The unique identifier for your Azure Active Directory instance, representing your organization.
* **Client ID**  
  * The unique identifier assigned to your application registered in Azure Active Directory.
* **Client Secret**  
  * The string that acts like a password, used by the application to authenticate with Azure Active Directory.
* **Workspace**  
  * Specify the workspace to connect to.
* **Eventhouse**  
  * Specify the Eventhouse instance to connect to.
* **Database**  
  * Select the database to connect to.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Custom Record | ✓ | ✓ |
| Send Custom Record (Batch) | ✓ | ✓ |
| Send Entire Event Data | ✗ | ✓ |
| Send Entire Event Data (Batch) | ✗ | ✓ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Entire Visitor Data (Batch) | ✓ | ✗ |
| Send Log Event | ✗ | ✓ |
| Send Entire Log Event | ✗ | ✓ |

Enter a name for the action and select the action type.

The following section describes how to set up parameters and options for each action.

### Send Custom Record

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Table | Provide the table name you want to connect to. |

#### Event parameters

Map the parameters to the columns of the table. You must map at least one parameter.

### Send Custom Record (Batch)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Table | Provide the table name you want to connect to. |

#### Event parameters

Map the parameters to the columns of the table. You must map at least one parameter.

| **Parameter** | **Description** |
| --- | --- |
| Batch time to live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Entire Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Table | Provide the table name you want to connect to. |
| Timestamp | Choose the column to record the timestamp. |
| Payload | Choose the dynamic column to record the JSON payload. |
| Timestamp Attribute | Select an attribute to assign as the timestamp if you want to send the timestamp in a different format. If an attribute is assigned and produces an empty value, the connector sends the current timestamp. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Note that if the attribute names are updated, the payload names reflect these changes. |

### Send Entire Event Data (Batch)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Table | Provide the table name you want to connect to. |
| Timestamp | Choose the column to record the timestamp. |
| Payload | Choose the dynamic column to record the JSON payload. |
| Timestamp Attribute | Select an attribute to assign as the timestamp if you want to send the timestamp in a different format. If an attribute is assigned and produces an empty value, the connector sends the current timestamp. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Note that if the attribute names are updated, the payload names reflect these changes. |
| Batch time to live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Entire Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Table | Provide the table name you want to connect to. |
| Timestamp | Choose the column to record the timestamp. |
| Payload | Choose the dynamic column to record the JSON payload. |
| Timestamp Attribute | Select an attribute to assign as the timestamp if you want to send the timestamp in a different format. If an attribute is assigned and produces an empty value, the connector sends the current timestamp. |
| Include All Visitor Events | Include current visit data with visitor data. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Note that if the attribute names are updated, the payload names reflect these changes. |

### Send Entire Visitor Data (Batch)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Table | Provide the table name you want to connect to. |
| Timestamp | Choose the column to record the timestamp. |
| Payload | Choose the dynamic column to record the JSON payload. |
| Timestamp Attribute | Select an attribute to assign as the timestamp if you want to send the timestamp in a different format. If an attribute is assigned and produces an empty value, the connector sends the current timestamp. |
| Include All Visitor Events | Include current visit data with visitor data. |
| Print Attribute Names | By default, the attribute keys are used. If you want to use the attribute names as keys instead, enable this checkbox. Consider that the payload names reflect the update if the attribute names are updated. |
| Batch time to live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Send Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Table | Provide the table name you want to connect to. |

#### Event parameters

Map the parameters to the columns of the table. You must map at least one parameter.

### Send Entire Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Table | Provide the table name you want to connect to. |
| Timestamp | Choose the column to record the timestamp. |
| Payload | Choose the dynamic column to record the JSON payload. |