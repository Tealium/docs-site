---
title: SAS 360 Match Connector Setup Guide
description: This article describes how to set up the SAS 360 Match connector.
url: https://docs.tealium.com/server-side-connectors/sas-360-match-connector/
---
## Actions

| Action name | Visitor profile | Event data |
| --- | :---: | :---: |
| Send State Vector Tags | ✓ | ✓ |

## Configuration

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **API Key**: The API key provided by SAS. Contact a SAS Technical Support to enable the API.
* **Base URL**: The SAS endpoint base URL, up to but not including `/setsv/`. For example, `https://mydomain.aimatch.com/mycompany`.

After you configure the connector, click **Done**.

## Actions

The following section lists the supported parameters for each action.

### Send State Vector Tags

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User Identifier (State Vector ID) | (Required) Map a relevant visitor identifier as custom text. |
| State Vector Tag Data | Add custom mapping for one or more tags. |

## Vendor documentation

* [SAS 360 Match: Advanced Features Guide](https://support.sas.com/documentation/prod-p/iap/default/en/PDF/Advanced_Features_SASIA.pdf)