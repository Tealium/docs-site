---
title: Kochava Connector Setup Guide
description: This article describes how to set up the Kochava connector.
url: https://docs.tealium.com/server-side-connectors/kochava-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Install Event| ✗| ✓|
|Send Post-Install Event| ✗| ✓|

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Send Install Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Kochava App ID| This is the unique application ID used to represent the App.<br> Reference the following [API documentation](https://support.kochava.com/server-to-server-integration/install-notification-setup) for more info|
|App Version| A string representation of the application version number. |
|IP Address| The IP address of the device on install.|
|Device Version| A string representation of the device make, model and OS. The syntax is as follows: `device-os_name-os_version` where each value is separated by a hyphen.<br> Reference the following [API documentation](https://support.kochava.com/server-to-server-integration/install-notification-setup) for more info|
|Device User Agent| A string representation of the device user agent as provided by the client. Please ensure that this is URL-encoded. This string is useful when campaigns require fingerprint attribution.|
|IDFA| You must include one or more of the following device IDs in the appropriate fields: IDFA, IMEI, Android ID, MAC address or a custom variant.|
|IDFV| You must include one or more of the following device IDs in the appropriate fields: IDFA, IMEI, Android ID, MAC address or a custom variant.|
|IMEI| You must include one or more of the following device IDs in the appropriate fields: IDFA, IMEI, Android ID, MAC address or a custom variant.|
|ADID| You must include one or more of the following device IDs in the appropriate fields: IDFA, IMEI, Android ID, MAC address or a custom variant.|
|Android ID| You must include one or more of the following device IDs in the appropriate fields: IDFA, IMEI, Android ID, MAC address or a custom variant.|
|iAd Org Name|
|iAd Conversion Date|
|iAd LineItem Name|
|iAd Campaign ID|
|iAd Attribution|
|iAd AdGroup Name|
|iAd Click Date|
|iAd Campaign Name|
|iAd LineItem ID|
|iAd Keyword|
|iAd AdGroup ID|

### Action — Send Post-Install Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Kochava App ID| This is the unique application ID used to represent the App.<br> Reference the following [API documentation](https://support.kochava.com/server-to-server-integration/post-install-event-setup) for more info|
|App Version| A string representation of the application version number. |
|IP Address| The IP address of the device on install.|
|Event Name| Name of the event to track.|
|Event Data| Data points related to the event tracked.|
|Device Version| A string representation of the device make, model and OS. The syntax is as follows: `device-os_name-os_version` where each value is separated by a hyphen.<br> Reference the following [API documentation](https://support.kochava.com/server-to-server-integration/post-install-event-setup) for more info|
|Device User Agent| A string representation of the device user agent as provided by the client. Please ensure that this is URL-encoded. This string is useful when campaigns require fingerprint attribution.|
|IDFA| You must include one or more of the following device IDs in the appropriate fields: IDFA, IMEI, Android ID, MAC address or a custom variant.|
|IDFV| You must include one or more of the following device IDs in the appropriate fields: IDFA, IMEI, Android ID, MAC address or a custom variant.|
|IMEI| You must include one or more of the following device IDs in the appropriate fields: IDFA, IMEI, Android ID, MAC address or a custom variant.|
|ADID| You must include one or more of the following device IDs in the appropriate fields: IDFA, IMEI, Android ID, MAC address or a custom variant.|
|Android ID| You must include one or more of the following device IDs in the appropriate fields: IDFA, IMEI, Android ID, MAC address or a custom variant.|
