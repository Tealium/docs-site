---
title: PulsePoint NPI List Connector Setup Guide
description: This article describes how to set up the PulsePoint NPI List connector.
url: https://docs.tealium.com/server-side-connectors/pulsepoint-npi-list-connector/
---
This integration connects you to Life by PulsePoint. Life is a DSP focused on healthcare advertising and lets you plan, activate, and analyze digital healthcare ad campaigns aimed at HCPs across endemic and non-endemic publishers. Our PulsePoint NPI List Connector provides you direct access and complete control to Life’s NPI List, creating a seamless integration to our [Tealium for Pharma CDP](/industries/tealium-for-pharma/).

## API Information

This connector uses the following vendor API:

* API Name: PulsePoint API
* API Version: v2
* API Endpoint: `https://lifeapi.pulsepoint.com/RestApi/v2/npi/npi-list/`

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Create NPI List | ✓ | ✗ |
| Add NPIs to a List | ✓ | ✗ |
| Delete NPIs from a List | ✓ | ✗ |

## Configure Settings

Navigate to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors]().


After adding the connector, configure the following settings:

* **Client ID**  
(Required) ID for the account in PulsePoint.
* **Client Secret**  
(Required) Secret for the account in PulsePoint, provided by a PulsePoint representative.
* **Username**  
(Required) PulsePoint Life username for the client.
* **Password**  
(Required) PulsePoint Life password for the client’s username.
* **Account ID**  
(Required) Account ID associated with the client and that holds all the NPI lists.

## Actions

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Create NPI List

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Name | (Required) Name of the advertiser that is linked to the NPI list. |
| Advertisers | (Required) NPI list name. |
| NPI | (Required) List of NPIs to include in the NPI list. |

### Add NPIs to a List

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| List ID | (Required) List number that the requested NPIs belong to. |
| NPI | (Required) List of NPIs to include in the NPI list. |

### Delete NPIs from a List

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| List ID | (Required) List number that the requested NPIs belong to. |
| NPI | (Required) List of NPIs to delete in the NPI list. |

    