---
title: Viant Connector Setup Guide
description: This article describes how to set up the Viant connector.
url: https://docs.tealium.com/server-side-connectors/viant-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Viant API
* API Version: v1
* API Endpoint: `https://tealium.viantinc.com/`

## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following three thresholds is met:

* Max number of requests: 15,000
* Max time since oldest request: 10 minutes
* Max size of requests: 2 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Username**  
  * The username provided by Viant for use in the API.
* **Password**  
  * The password provided by Viant for use in the API.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Data (Batched) | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Data (Batched)

#### Data Parameters

| **Parameter** | **Description** |
| --- | --- |
| Segment Name | (Required) Name of the Segment. |
| Advertiser ID | (Required) Viant Advertiser `ID`. |
| TTL | (Required) The time in seconds before record expires. If you do not have a preference, use the maximum value of `32000000`. |
| Segment ID | (Required) A unique identifier for the segment. Can be a Viant ID (for example, taxonomy ID or userpool ID) or non-Viant identifier (for example, partner segment ID). |
| Segment ID Type | (Required) Defines the segment ID type. Allowed values are `userpool`, `taxonomy`, `third_party`. |
| Transaction ID | (Required) Transaction ID for purchase events. |
| Sales Amount | (Required) Sales amount for purchase events. |

#### Payload Parameters

| **Parameter** | **Description** |
| --- | --- |
| Hashed Email | Personal email, all lower case, no leading or trailing spaces prior to hashing. Can be hashed with `md5` or `sha256`. |
| Hashed Physical Address | Address in [United States Postal System format](https://faq.usps.com/s/article/What-is-the-Format-and-Sequence-of-Information-for-the-Recipient-s-Address#:~:text=LINE%201%3A%20NAME%20OF%20ADDRESSEE,AND%20POSTAL%20CODE%20(IF%20KNOWN)) prior to hashing. Can be hashed with md5 or sha256. |
| IP | Client side IPv4 address |
| Mobile ID | `AAID` or `IDFA` |
| Cookie | Viant Cookie |
| UID2 | Unified ID 2.0 |
| Ramp ID | Ramp ID |
| ID5 | ID5 ID |