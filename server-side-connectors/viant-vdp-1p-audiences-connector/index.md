---
title: Viant VDP 1P Audiences Connector Setup Guide
description: This article describes how to set up the Viant VDP 1P Audiences connector.
url: https://docs.tealium.com/server-side-connectors/viant-vdp-1p-audiences-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Viant API
* API Version: v1
* API Endpoint: `https://vdp-connect-api.viantinc.com`
* Documentation: [Viant API](https://docs.api.viantinc.com/reference/create-new-audience-segment)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1,000
* Max time since oldest request: 10 minutes
* Max size of requests: 10 MB

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Client ID**: (Required) Client ID for Viant VDP API authentication.
* **Client secret**: (Required) Client secret for Viant VDP API authentication.
* **Account ID**: (Required) Viant account ID.
* **Advertisers ID**: (Required) Viant advertisers ID.
* **Select audience**: Select an audience segment from the list, or click **Create New Segment** to create a new one. You can also enter a custom Viant segment ID directly.

## Actions

| Action name | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Add audience data | ✓ | ✓ |
| Expire individual audience IDs | ✓ | ✓ |

### Add audience data

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1,000
* Max time since oldest request: 10 minutes
* Max size of requests: 10 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Viant segment ID | The ID of the audience segment. This value overrides the audience segment value set in the connector configuration. |
| Country code | Two-letter country code, for example `US` or `CA`. |

#### User data

| Parameter | Description |
| --- | --- |
| Email (apply SHA256 hash) | Plain-text email address. The connector normalizes and hashes the value. |
| Phone number (apply SHA256 hash) | Plain-text phone number. The connector normalizes and hashes the value. |
| Address (already SHA256 hashed) | Pre-hashed address. Follow USPS formatting standards before hashing. |

### Expire individual audience IDs

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1,000
* Max time since oldest request: 10 minutes
* Max size of requests: 10 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Viant segment ID | The ID of the audience segment. This value overrides the audience segment value set in the connector configuration. |
| Data type | The identifier data type for the audience. Accepted values: `email_sha256`, `phonenumber_sha256`, `address_sha256`, `ip`, `cookie`, `mobile_id`. |

#### User data

| Parameter | Description |
| --- | --- |
| Email (apply SHA256 hash) | Plain-text email address. The connector normalizes and hashes the value. |
| Phone number (apply SHA256 hash) | Plain-text phone number. The connector normalizes and hashes the value. |
| Address (already SHA256 hashed) | Pre-hashed address. Follow USPS formatting standards before hashing. |

