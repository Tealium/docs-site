---
title: Yahoo Conversions Connector Setup Guide
description: This article describes how to set up the Yahoo Conversions connector.
url: https://docs.tealium.com/server-side-connectors/yahoo-conversions-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Conversion| ✓| ✓|

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](/server-side/connectors/manage/) article.

Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Send Conversion

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Click ID (`vmcid`)| (Required) Value of pixel context macro collected from the click or third party ad server.|
|Yahoo Client ID &lt;br&gt; (`dp`)| (Required) The client ID sent as the `dp` parameter prepended with `tealium_`. For example, `tealium_123456789`.|
|Event ID (`id`)| Unique event ID provided by Tealium. Yahoo uses this parameter to prevent duplication in reporting. If not mapped, Tealium will generate a UUID for this value.|
|Event Time (`et`)| Business time of the event (epoch UTC milliseconds). If not mapped, it will be initialized with the current timestamp.|
|Conversion Value (`gv`)| The numerical value of any given conversion. By default, the value is assumed to be United States Dollars (USD). The value is reported as dynamic conversion value in DSP and calculate ROAS in Native. For example, `12.25` (no currency symbol).|
|Conversion Currency (`gc`)| Event value currency.|
|Event Category (`ec`)| Event category.|
|Event Action (`ea`)| Event action.|
|Pixel ID (.`yp`)| Pixel ID.|
