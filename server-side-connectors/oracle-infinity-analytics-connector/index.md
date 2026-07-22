---
title: Oracle Infinity Analytics Connector Setup Guide
description: This article describes how to set up the Oracle Infinity Analytics connector.
url: https://docs.tealium.com/server-side-connectors/oracle-infinity-analytics-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Oracle Infinity Analytics Data Collection API
* API Version: v3
* API Endpoint: `https://dc.oracleinfinity.io`
* Documentation: [Oracle Infinity Analytics Data Collection API](https://docs.oracle.com/en/cloud/saas/marketing/infinity-user/Help/data_collection/dcapi.htm)

### Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
|:----------------|:-------------------|:----------------|
| Send Event      | ✓                  | ✓               |

### Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Account GUID**
  * The account GUID displayed in the **Oracle Infinity** user interface.
  * For more information see th [Oracle Infinity Analytics Data collection API documentation](https://docs.oracle.com/en/cloud/saas/marketing/infinity-user/Help/data_collection/dcapi.htm).

### Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

#### Action - Send Event

##### Parameters

| **Parameter**                | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|:-----------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| URI Stem                     | <ul><li>(Required) The URI stem, which is the portion of a URL that appears after the host and port and precedes the query string.</li><li>Typically the requested file or page that a user accessed.</li></ul>                                                                                                                                                                                                                              |
| Kind of Event                | <ul><li>(Required) Specifies a numeric identifier for the kind of event tracked, which are used for event-level filtering and reporting.</li></ul>                                                                                                                                                                                                                                                                                           |
| Visitor ID                   | <ul><li>(Required) Random value used as a visitor ID and stored in a first-party cookie.</li></ul>                                                                                                                                                                                                                                                                                                                                           |
| Unix Time Stamp              | <ul><li>Random value used as a visitor ID and stored in a first-party cookie.</li></ul>                                                                                                                                                                                                                                                                                                                                                            |
| Domain Visited               | <ul><li>Required if sent from a website.</li><li>The domain visited, such as `http://www.example.com`.</li></ul>                                                                                                                                                                                                                                                                                                                                   |
| Custom Visitor ID            | <ul><li>Identifies an optional unique custom visitor ID that you can assign to your visitors in other systems.</li><li>This is separate and distinct from automatically generated Visitor ID parameters sent by the Oracle Infinity tag.</li><li>If you do not send a custom value, this parameter will not be present on the "hit".</li></ul>                                                                                                     |
| Custom Event Data (Advanced) | <ul><li>For descriptions of the possible parameters that can be passed to data collection see the [parameter reference](https://docs.oracle.com/en/cloud/saas/marketing/infinity-user/Help/parameters/reference.htm).</li><li>Specify key-value pairs to be added to the event being sent.</li><li>Key-value pairs will be added "as-is" with no checks or formatting.</li><li>Array elements are joined with semicolon (`;`) separator.</li></ul> |
