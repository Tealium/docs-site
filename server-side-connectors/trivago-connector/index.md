---
title: Trivago Connector Setup Guide
description: This article describes how to set up the Trivago connector.
url: https://docs.tealium.com/server-side-connectors/trivago-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Trivago API
* API Endpoint: `https://secde.trivago.com/`
* Documentation: [Trivago API](https://developer.trivago.com/conversiontracking/conversion-api.html)

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:
* **X-Trv-Ana-Key**  
  *   Universally unique identifier. Contact your Trivago Technical Account Manager for more information.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Booking Confirmation | ✗ | ✓ |
| Update Booking Confirmation | ✗ | ✓ |
| Delete Booking Confirmation | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Booking Confirmation

#### Parameters

Required Parameters:

| **Parameter** | **Description** |
| --- | --- |
| TRV Reference | Unique tracking parameter as provided at the end of the URL. |
| Advertiser ID | The advertiser&#39;s unique ID, communicated to advertisers by Trivago. This value is always the same for one advertiser. |
| Hotel | The advertiser&#39;s unique hotel ID for the booked hotel. Must be identical to the IDs used in the inventory feed. |
| Arrival | Arrival date (UNIX timestamp). |
| Departure | Departure date (UNIX timestamp). |
| Booking Date | Booking submit date (UNIX timestamp). |
| Volume | Total gross booking price per stay (including all rooms, all nights). Gross price is the net rate plus the booking fee, plus VAT. |
| Currency | Currency in `ISO 4217` code. |
| Booking ID | The advertiser&#39;s booking reference. |
| Locale | Contains the Trivago `POS` the user clicked from, before being redirected to the advertiser&#39;s site. For more information, see [Trivago &gt; Supported locales and languages](https://developer.trivago.com/fastconnect/supported-locales.html). If you need to append the identifier to the URLs, contact your Technical Account Manager. |
| Number of Rooms | The total number of rooms booked with the same **Booking ID**. |
| Date Format | Required when the arrival and departure cannot be given in UNIX timestamp format. For example: `20181025` in YYYYMMDD format. The recommended format is YYYYMMDD but the separator can be adjusted as needed, according to the [accepted formats](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat). The date should be shared in UTC format when possible. Otherwise, the UTC-based timestamp needs to be included in both **Booking Date** and **Booking Date Format** parameters. For example: `booking_date_format`:&#34;YmdHisP&#34;, `booking_date`:&#34;`20200929123015&#43;07:00`&#34;. |
| Booking Date Format | Required when **Booking Date** cannot be given in UNIX timestamp format. The time of the booking in seconds is also required. For example: `20201025173002`. The recommended format is YmdHis but the separator can be adjusted as needed according to the [accepted formats](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat). The date should be shared in UTC format when possible. Otherwise, the UTC-based timestamp needs to be included in both **Booking Date** and **Booking Date Format**. For example, `booking_date_format`:&#34;YmdHisP&#34;, `booking_date`:&#34;`20200929123015&#43;07:00`&#34;. |
| Margin | Percentage of booking amount received as commission for the booking. For example: `15.8`. |
| Margin Absolute | If the margin cannot be provided in percentage, it can be provided alternatively as absolute value (for example: `60.30 USD`). The currency of **Margin Absolute** should match the currency provided for the volume. |

### Update Booking Confirmation

#### Parameters

Required Parameters:

| **Parameter** | **Description** |
| --- | --- |
| TRV Reference | Unique tracking parameter as provided at the end of the URL. |
| Advertiser ID | Trivago Advertiser ID, communicated to advertisers by Trivago. This value is always the same for one advertiser. |
| Hotel | The advertiser&#39;s unique hotel ID for the booked hotel. Must be identical to the IDs used in the inventory feed. |
| Arrival | Arrival date (UNIX timestamp). |
| Departure | Departure date (UNIX timestamp). |
| Booking Date | Booking submit date (UNIX timestamp). |
| Volume | Total gross booking price per stay (including all rooms, all nights). Gross price is the net rate plus the booking fee, plus VAT. |
| Currency | Currency in ISO 4217 code. |
| Booking ID | The advertiser&#39;s booking reference. |
| Locale | Contains the Trivago `POS` the user clicked from, before being redirected to the advertiser&#39;s site. For more information, see [Trivago &gt; Supported locales and languages](https://developer.trivago.com/fastconnect/supported-locales.html). If you need to append the identifier to the URL, contact your Technical Account Manager. |
| Number of Rooms | The total number of rooms booked with the same **Booking ID**. |
| Date Format | Required when arrival and departure cannot be given in UNIX timestamp format, These dates can be given in a different format. For example: `20181025` in YYYMMDD format. The recommended format is YYMMDD, but the separator can be adjusted as needed, according to the [accepted formats](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat). The date should be shared in UTC format, when possible. Otherwise, the UTC-based timestamp needs to be included in both **Booking Date** and **Booking Date Format**. For example: `booking_date_format`:&#34;YmdHisP&#34;, `booking_date`:&#34;`20200929123015&#43;07:00`&#34;. |
| Booking Date Format | Required when **Booking Date** cannot be given in UNIX timestamp format. The time of the booking in seconds is also required. For example: `20201025173002`. The recommended format is YmdHis but the separator can be adjusted as needed according to the [accepted formats](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat). The date should be shared in UTC format, when possible. Otherwise, the UTC-based timestamp needs to be included in both **Booking Date** and **Booking Date Format**. For example: `booking_date_format`:&#34;YmdHisP&#34;, `booking_date`:&#34;`20200929123015&#43;07:00`&#34;). |
| Margin | Percentage of booking amount received as commission for the booking. For example: `15.8`). |
| Margin Absolute | If the margin cannot be provided in percentage, it can be provided alternatively as absolute value. For example: `60.30 USD`. The currency of **Margin Absolute** should match the currency provided for the volume. |
| Update Date | Booking update date. |
| Update Date Format | Required when **Update Date** cannot be given in UNIX timestamp format. The time of the cancellation in seconds (for example: `20201025173002`) is also required. The recommended format is YmdHis but the separator can be adjusted as needed according to the [accepted formats](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat). The date should be shared in UTC format when possible. The UTC-based timestamp needs to be included in both **Update Date** and **Update Date Format** (for example: `update_date_format`:&#34;YmdHisP&#34;, `update_date`:&#34;`20200929123015&#43;07:00`&#34;). |
| Update Origin | Describes whether a PUT call is based on a user&#39;s or an advertiser&#39;s update to the given booking confirmation data. The possible values are either `advertiser` or `user`. |

### Delete Booking Confirmation

#### Parameters
Required Parameters:

| **Parameter** | **Description** |
| --- | --- |
| TRV Reference | Unique tracking parameter as provided at the end of the URL. |
| Advertiser ID | Trivago Advertiser ID, as defined and communicated to advertisers by Trivago. This value is always the same for one advertiser. |
| Hotel | The advertiser&#39;s unique hotel ID for the booked hotel. Must be identical to the IDs used in the inventory feed. |
| Arrival | Arrival date (UNIX timestamp). |
| Departure | Departure date (UNIX timestamp). |
| Booking Date | Booking submit date (UNIX timestamp). |
| Volume | Total gross booking price per stay (including all rooms, all nights). Gross price is the net rate plus the booking fee, plus VAT. |
| Currency | Currency in ISO 4217 code. |
| Booking ID | The advertiser&#39;s booking reference. |
| Locale | Contains the Trivago `POS` the user clicked from, before being redirected to the advertiser&#39;s site. For more information, see [Trivago &gt; Supported locales and languages](https://developer.trivago.com/fastconnect/supported-locales.html). If you need to append the identifier to the URL, contact your Technical Account Manager. |
| Number of Rooms | The total number of rooms booked with the same **Booking ID**. |
| Date Format | Required when arrival and departure dates cannot be given in UNIX timestamp format. For example: `20181025` in YYYYMMDD format. The recommended format is YYYYMMDD but the separator can be adjusted as needed, according to the [accepted formats](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat). The date should be shared in UTC format, when possible. Otherwise, the UTC-based timestamp needs to be included in both **Booking Date** and **Booking Date Format**. For example: `booking_date_format`:&#34;YmdHisP&#34;, `booking_date`:&#34;`20200929123015&#43;07:00`&#34;. |
| Booking Date Format | Required when **Booking Date** cannot be given in UNIX timestamp format. The time of the booking in seconds (for example: `20201025173002`) is also required. The recommended format is YmdHis but the separator can be adjusted as needed according to the [accepted formats](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat). The date should be shared in UTC format when possible. Otherwise, the UTC-based timestamp needs to be included in both **Booking Date**  and **Booking Date Format**. For example: `booking_date_format`:&#34;YmdHisP&#34;, `booking_date`:&#34;`20200929123015`&#43;07:`00`&#34;. |
| Margin | Percentage of booking amount received as commission for the booking. For example: `15.8`. |
| Margin Absolute | If the margin cannot be provided in percentage, it can be provided alternatively as absolute value. For example: `60.30 USD`. The currency of **Margin Absolute** should match the currency provided for the volume. |
| Refund Amount | Total refunded amount per stay (including all rooms, all nights, all fees). The parameter is required for `DELETE` calls even if **Refund Ratio** is provided. |
| Refund Ratio | Specifies how much of a given volume is going to be refunded. It needs to be shared with 4 decimal places. For example: 1.0000 = 100%, 0.0000 = 0.00%, 0.5052 = 50.52%. |
| Cancellation Date | Cancellation submit date. |
| Cancellation Date Format | Required when **Cancellation Date** cannot be given in UNIX timestamp format. The time of the cancellation in seconds (for example: `20201025173002`) is also required. The recommended format is YmdHis but the separator can be adjusted as needed according to the [accepted formats](https://developer.trivago.com/conversiontracking/conversion-api.html#dateformat). The date should be shared in UTC. If not possible, the UTC-based timestamp needs to be included in both **Cancellation Date** and **Cancellation Date Format**. For example: `cancellation_date_format`:&#34;YmdHisP&#34;, `cancellation_date`:&#34;`20200929123015&#43;07:00`&#34;. |