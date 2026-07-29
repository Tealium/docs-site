---
title: RTB House Audiences Connector Setup Guide
description: Use the RTB House Audiences connector to deliver audience membership changes to an RTB House-managed Google Cloud Storage bucket in JSONL format.
url: https://docs.tealium.com/server-side-connectors/rtb-house-audiences-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Google Cloud Storage API
* API Version: v1
* API Endpoint: `https://storage.googleapis.com/`

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).


<blockquote>
This connector uses a Tealium-managed Google Cloud service account for authentication. RTB House grants this account access to the destination bucket, so no authentication setup is required here.
</blockquote>


## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add user to RTB House segment | ✓ | ✗ |
| Remove user from RTB House segment | ✓ | ✗ |

### Add user to RTB House segment

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 100 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Segment ID | Enter the RTB House `segment_id`. No spaces or special characters are allowed. |

#### User identifiers

At least one of the following user identifiers must be mapped and populated when the action is triggered.

| Parameter | Description |
| --- | --- |
| AAID | Android device advertising ID. |
| IDFA | iOS device advertising ID. |
| UID | RTB House synced user ID from the site pixel. |
| AID | Alternative user ID, such as a hashed email or internal ID. |

### Remove user from RTB House segment

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 100 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Segment ID | Enter the RTB House `segment_id`. No spaces or special characters are allowed. |

#### User identifiers

At least one of the following user identifiers must be mapped and populated when the action is triggered.


<blockquote>
This action completes successfully even if the user is not currently in the segment. The connector writes the removal record without checking current segment membership.
</blockquote>


| Parameter | Description |
| --- | --- |
| AAID | Android device advertising ID. |
| IDFA | iOS device advertising ID. |
| UID | RTB House synced user ID from the site pixel. |
| AID | Alternative user ID, such as a hashed email or internal ID. |
