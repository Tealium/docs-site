---
title: AT Internet Piano Analytics Connector Setup Guide
description: This article describes how to set up the AT Internet Piano Analytics connector.
url: https://docs.tealium.com/server-side-connectors/at-internet-piano-analytics-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **Collection Domain**: (Required) The collection endpoint for your organization.
* **Collection Path**: (Required) The collection path.
* **Site ID**: (Required) The data source site ID.

Click **Done** when you are finished configuring the connector.

## Actions

|Action Name| AudienceStream| EventStream|
|---| ---| ---|
|Send Event| ✓| ✓|

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action. For more information about AT Internet Piano Analytics Connector parameters, see the [Collection API](https://developers.atinternet-solutions.com/piano-analytics/data-collection/how-to-send-events/collection-api#marketing-campaigns) documentation.

### Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100
* Max time since oldest request: 5 minutes
* Max size of requests: 1 MB

### Send Event

#### Parameters

|Parameter| Description|
| --- | --- |
|Event Type| All [Standard events](https://developers.atinternet-solutions.com/piano-analytics/data-collection/how-to-send-events/standard-events) are supported. To send a custom, non-standard event, select the **Custom** option and provide the **Custom Event Type** value in the **Event Properties** section.|

#### Event Properties

|Parameter| Description|
| --- | --- |
|Date Formats| Specify the [date format](https://developers.atinternet-solutions.com/piano-analytics/data-collection/how-to-send-events/collection-api#date) when populating an event property.&lt;br&gt; Only milliseconds since epoch UTC (or CDH Date Attributes) are formattable, otherwise the action fails.&lt;br&gt; The following date formats are valid: `YYYYMMDD`, `YYYY-MM-DD`, `YYYY-MM-DDTHH:mm:ssZ`, `UNIX`.|

#### Standard Parameters

|Parameter| Description|
| --- | --- |
|IP Address| IP address of the client.|
|Referer| Address of the page sending the data.|
| Site ID | ID of the site the data belongs to. This parameter overwrites the value defined in the **Configuration** tab if the value is not empty. |
|User Agent| User agent of the client. If this field is not mapped, it is auto-mapped to the User Agent attribute in Tealium EventStream API Hub and to the visitor’s last User Agent attribute in Tealium AudienceStream CDP.|
|Visitor ID| Unique identifier of the visitor. If this field is not mapped, it is auto-mapped to the Tealium Visitor ID.|

#### Common Contextual Properties

AT Internet Piano Analytics recommends additional properties to enhance analysis.

|Parameter| Description|
| --- | --- |
|Previous URL| The previous page URL. If this field is not mapped, it is auto-mapped to the Current URL attribute in EventStream and to the Entry URL attribute in AudienceStream.|
|Device Timestamp UTC| Device timestamp UTC in seconds. Date attributes are converted to UNIX timestamp.|
|Event Collection Platform| Collection platform used.|
|Event Collection Version| Version of the collection platform.|
|Device Manufacturer| Manufacturer of the device.|
|Device Model| Model of the device.|
|Device Display Height| Height of the viewport.|
|Device Display Width| Width of the viewport.|
|Device Screen Height| Height of the device screen.|
|Device Screen Width| Width of the device screen.|

#### Marketing Campaigns Properties

Map fields in this section to track marketing campaigns.

|Parameter| Description|
| --- | --- |
|Campaign Medium| Required property for tracking marketing campaigns.|
|Campaign Name| Required property for tracking marketing campaigns.|
|Campaign Creation| The campaign creation. For usage examples, see [AT Internet Piano: Analytics Connector Collection API](https://developers.atinternet-solutions.com/piano-analytics/data-collection/how-to-send-events/collection-api#marketing-campaigns).|
|Campaign Variant| The campaign variant.|
|Campaign Format| The campaign format.|
|Campaign Type| The campaign type.|

#### User Properties

|Parameter| Description|
| --- | --- |
|User ID| Map this field to track authenticated users.|
|User Category| Map this field to track authenticated users.|

#### Goals Properties

|Parameter| Description|
| --- | --- |
|Goal Type| Set Goal Type to track a conversion.|

#### Enhanced Marketing Source Detection

|Parameter| Description|
| --- | --- |
| Source Content | Captures content details from marketing campaigns (for example, ad copy or creative label). |
| Creative Format | Identifies the creative format used in campaigns. |
| Source ID | Unique identifier for tracking specific campaigns. |
| Marketing Tactic | Records the marketing tactic employed. |
| Source | Indicates the primary traffic source. |
| Source Platform | Specifies the platform where the source originated. |
| Source Term | Captures search terms or keywords. |
| Auto Event Collection | Tracks whether event collection was automatically triggered. |
| Country | (Alpha-`2`) Provides ISO 3166 Alpha-2 country codes for geo reporting. |