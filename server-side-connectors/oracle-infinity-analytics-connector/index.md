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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

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
| URI Stem                     | &lt;ul&gt;&lt;li&gt;(Required) The URI stem, which is the portion of a URL that appears after the host and port and precedes the query string.&lt;/li&gt;&lt;li&gt;Typically the requested file or page that a user accessed.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                              |
| Kind of Event                | &lt;ul&gt;&lt;li&gt;(Required) Specifies a numeric identifier for the kind of event tracked, which are used for event-level filtering and reporting.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                           |
| Visitor ID                   | &lt;ul&gt;&lt;li&gt;(Required) Random value used as a visitor ID and stored in a first-party cookie.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                           |
| Unix Time Stamp              | &lt;ul&gt;&lt;li&gt;Random value used as a visitor ID and stored in a first-party cookie.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                            |
| Domain Visited               | &lt;ul&gt;&lt;li&gt;Required if sent from a website.&lt;/li&gt;&lt;li&gt;The domain visited, such as `http://www.example.com`.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                   |
| Custom Visitor ID            | &lt;ul&gt;&lt;li&gt;Identifies an optional unique custom visitor ID that you can assign to your visitors in other systems.&lt;/li&gt;&lt;li&gt;This is separate and distinct from automatically generated Visitor ID parameters sent by the Oracle Infinity tag.&lt;/li&gt;&lt;li&gt;If you do not send a custom value, this parameter will not be present on the &#34;hit&#34;.&lt;/li&gt;&lt;/ul&gt;                                                                                                     |
| Custom Event Data (Advanced) | &lt;ul&gt;&lt;li&gt;For descriptions of the possible parameters that can be passed to data collection see the [parameter reference](https://docs.oracle.com/en/cloud/saas/marketing/infinity-user/Help/parameters/reference.htm).&lt;/li&gt;&lt;li&gt;Specify key-value pairs to be added to the event being sent.&lt;/li&gt;&lt;li&gt;Key-value pairs will be added &#34;as-is&#34; with no checks or formatting.&lt;/li&gt;&lt;li&gt;Array elements are joined with semicolon (`;`) separator.&lt;/li&gt;&lt;/ul&gt; |
