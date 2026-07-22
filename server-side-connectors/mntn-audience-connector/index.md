---
title: MNTN Audience Connector Setup Guide
description: This article describes how to set up the MNTN Audience connector.
url: https://docs.tealium.com/server-side-connectors/mntn-audience-connector/
---
The MNTN Audience connector lets you create and manage MNTN audience segments from Tealium. Use this connector to sync first-party identities in batches to add, update, or remove audience members for connected TV (CTV) targeting, retargeting, and suppression without manual file uploads or custom API code.



## API information

This connector uses the following vendor API:

* API Name: MNTN Audience API
* API Version: v2026.0.1
* API Endpoint: `https://integrations.ex.mountain.com`

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **MNTN Audience API Key**: (Required) Your MNTN Audience API key.

## Actions

| Action Name | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Batch Upsert Audience Members | ✓ | ✓ |
| Batch Remove Audience Members | ✓ | ✓ |

### Batch Upsert Audience Members

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10,000
* Max time since oldest request: 60 minutes
* Max size of requests: 2 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Segment ID | ID of the existing MNTN audience segment to insert or update identities in. |
| Identity ID | (Required) Unique ID for the audience member within the segment (for example, a Tealium Visitor ID or CRM ID). |

#### Identifiers

| Parameter | Description |
| --- | --- |
| Email (Apply SHA256) | Plain text email address. The connector normalizes (lowercase, trim) and applies SHA256 hashing. |
| Email (Already SHA256) | Pre-hashed email address. Ensure the value is lowercased and trimmed before hashing. |
| Phone (Apply SHA256) | Plain text phone number. The connector strips non-digits, prepends the country code, and applies SHA256 hashing. |
| Phone (Already SHA256) | Pre-hashed phone number. Remove non-digits and prepend `1` for 10-digit US numbers before hashing. |
| IPv4 | Raw IPv4 address. |
| IPv4 (Already SHA256) | Pre-hashed IPv4 address. |
| IPv6 | Raw IPv6 address. |
| IPv6 (Already SHA256) | Pre-hashed IPv6 address. |
| MAID | Raw mobile advertising ID in UUID format, used for CTV or mobile targeting (for example, `3f097372-f01e-4b64-984c-395ae5828ee6`). |


<blockquote>
IPv4 (Already SHA256), IPv6, IPv6 (Already SHA256), and MAID have selective support in MNTN campaign targeting. Contact your MNTN account team before relying on these identifiers for targeting.
</blockquote>


### Batch Remove Audience Members

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1,000
* Max time since oldest request: 60 minutes
* Max size of requests: 2 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Audience Segment | Select the MNTN audience segment to remove members from, or enter a segment ID manually. |
| Identity ID | (Required) The identity ID of the audience member to remove from the segment (for example, a Tealium Visitor ID or CRM ID). |

## Best practices

* Start with a small test segment before you scale to production volumes.
* Keep request payloads efficient. MNTN recommends targeting batches around 2 MB and staying below the 8 MB maximum request size.
* Use a consistent identity strategy to avoid duplicate or conflicting records.
* Confirm consent and privacy requirements before you send identifiers to MNTN.

For more information, see [MNTN Help Center: Connect Tealium](https://help.mountain.com/en/articles/14696352-connect-tealium).
