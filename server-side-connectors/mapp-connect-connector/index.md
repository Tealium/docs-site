---
title: Mapp Connect Connector Setup Guide
description: This article describes how to set up the Mapp Connect connector.
url: https://docs.tealium.com/server-side-connectors/mapp-connect-connector/
---
## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Create  or Update Contact | ✓ | ✓ |
| Remove Contact from Group | ✓ | ✓ |

## Configuration

Navigate to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Integration ID**  
The ID of the Mapp integration to send data to.
* **API URL**  
The URL for the API endpoint, which does not need to include the protocol.
* **API Secret**  
The secret key generated within Mapp for generating a JWT for authentication. For more information, see [Mapp: Create an integration](https://documentation.mapp.com/latest/en/create-an-integration-10525713.html).

## Actions

The following section lists the supported parameters for each action.

### Create or Update Contact

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Group ID | The group ID to add the contact to. This is required when the contact does not exist in Mapp. |

#### User Parameters

| **Parameter** | **Description** |
| --- | --- |
| Email | (Required) The contact&#39;s email address. |

### Remove Contact from Group

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Group ID | The group ID to remove the contact from. This is required when the contact does not exist in Mapp. |

#### User Parameters

| **Parameter** | **Description** |
| --- | --- |
| Email | (Required) The contact&#39;s email address. |

