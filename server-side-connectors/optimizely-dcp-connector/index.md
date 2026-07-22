---
title: Optimizely DCP Connector Setup Guide
description: This article describes how to set up the Optimizely Dynamic Customer Profiles connector.
url: https://docs.tealium.com/server-side-connectors/optimizely-dcp-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Optimizely Dynamic Customer Profiles API
* API Version: v2
* API Endpoint: `https://vis.optimizely.com/api/customer_profile`
* Documentation: [Optimizely Dynamic Customer Profiles API](https://docs.developers.optimizely.com/web-experimentation/docs/dcp#write-customer-profile)

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Update Customer Profile| ✓| ✓|

## Configure Settings

Navigate to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **API Key**: Visit the [Optimizely Tokens API](http://app.optimizely.com/tokens) to generate an API key, or the [Optimizely documentation](http://developers.optimizely.com/classic/token) for more information.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Update Customer Profile

#### Parameters

|**Parameter**| **Description**|
|---| ---|
| DCP Service ID | For more information about the DCP Service ID, see [Optimizely: Create Audiences with Dynamic Customer Profiles](https://support.optimizely.com/hc/en-us/articles/4410289305357-Create-audiences-with-Dynamic-Customer-Profiles). |
| DCP Datasource ID | For more information about the DCP Datasource ID, see [Optimizely: Create Audiences with Dynamic Customer Profiles](https://help.optimizely.com/Target_Your_Visitors/Personalization%3A_Create_Audiences_with_Dynamic_Customer_Profiles). |
| Optimizely Customer ID | For more information about the Optimizely Customer ID, see [Optimizely: Create Audiences with Dynamic Customer Profiles](https://help.optimizely.com/Target_Your_Visitors/Personalization%3A_Create_Audiences_with_Dynamic_Customer_Profiles). We recommend that you use the Optimizely end user ID found in the first party cookie. |
| Customer Profile Attributes | A customer profile attribute describes one aspect of a customer's profile within a data source. The specified attribute value overwrites any existing value specified earlier. If a key does not correspond to a registered attribute name or a value does not respect the attribute datatype/format, the write will fail. |
