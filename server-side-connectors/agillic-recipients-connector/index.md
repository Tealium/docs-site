---
title: Agillic Recipients Connector Setup Guide
description: This article describes how to set up the Agillic Recipients connector.
url: https://docs.tealium.com/server-side-connectors/agillic-recipients-connector/
---
## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add or Update Recipient| ✓| ✓|
|Add or Update Recipient (Batched)| ✓| ✓|
|Update Recipient Table Records| ✓| ✓|
|Achieve Event| ✓| ✓|

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **Client ID**
  * (Required) Provide your web application client ID.
  * For more information, see [Getting Started with APIs: Authentication](https://developers.agillic.com/apis/getting-started#authentication).

* **Client Secret**
  * (Required) Provide your web application client secret.

* **Date Format**
  * Set the date format for the connector.
  * If not specified, the default format `dd.MM.yyyy` is used.
  * The date and timestamp format is unique to each Agillic account instance.
  * Formats are defined in the Agillic Administration interface.
  * For more information, see [Getting Started with APIs: Dates and Time](https://developers.agillic.com/apis/getting-started#dates-and-time).

* **Timestamp Format**
  * Set the timestamp format for the connector.
  * If not specified, the default format `dd.MM.yyyy` is used.

## Actions

Click **Next** or go to the **Actions** tab. Enter a name for the action and select the action type from the drop-down menu.

This section describes how to set up parameters and options for each action.

### Add or Update Recipient

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Recipient ID|  <ul><li>(Required) Map any unique Person Data, such as EMAIL or MOBILE.</li><li>Use Recipient ID for general purpose.</li><li>For more information, see [APIs: Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation).</li></ul> |
|Recipient Data|  <ul><li>(Required) Map values to the Person Data fields.</li></ul> |

### Add or Update Recipient (Batched)

### Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 5 MB

### Parameters

|**Parameter**| **Description**|
|---| ---|
|Recipient ID|  <ul><li>(Required) Map any unique Person Data, such as EMAIL or MOBILE.</li><li>Use Recipient ID for general purpose.</li><li>For more information, see [APIs: Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation).</li></ul> |
|Recipient Data|  <ul><li>(Required) Map values to the Person Data fields.</li></ul> |
| Recipient ID Attribute Name |<ul><li>(Optional) Overwrites which Person Data value is used to match with existing recipients.</li><li>Map any unique Person Data, such as EMAIL or MOBILE.</li><li>For more information, see [APIs: Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation).</li></ul> |

### Update Recipient Table Records

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Recipient ID|  <ul><li>(Required) Map any unique Person Data, such as EMAIL or MOBILE.</li><li>Use Recipient ID for general purpose.</li><li>For more information, see [APIs: Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation).</li></ul> |
|Table|  <ul><li>(Required) Table ID of the records that will be batch updated.</li></ul> |
|Table Record|  <ul><li>(Required) Map one or more values to each table record field.</li><li>ID or Primary Key must be specified.</li></ul> |

### Achieve Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Recipient ID|  <ul><li>(Required) Map any unique Person Data, such as EMAIL or MOBILE.</li><li>Use Recipient ID for general purpose.</li><li>For more information, see [APIs: Recipient API](https://developers.agillic.com/apis/recipients-api#api-documentation).</li></ul> |
|Event ID|  <ul><li>(Required) Event ID to be achieved.</li></ul> |