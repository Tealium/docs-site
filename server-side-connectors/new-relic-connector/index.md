---
title: New Relic Connector Setup Guide
description: This article describes how to set up the New Relic connector.
url: https://docs.tealium.com/server-side-connectors/new-relic-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:
* **Api Key**
  * The New Relic license key. Browser, mobile, or user keys are not supported.
* **Account ID**
  * The New Relic account ID.
* **Region**
  * The region where your account belongs: **EU** or **US**.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Entire Event Data | ✗ | ✓ |
| Send Entire Event Data (Batch) | ✗ | ✓ |
| Send Custom Event Data | ✗ | ✓ |
| Send Custom Event Data (Batch) | ✗ | ✓ |
| Send Entire Visitor Data | ✓ | ✗ |
| Send Entire Visitor Data (Batch) | ✓ | ✗ |
| Send Custom Visitor Data | ✓ | ✗ |
| Send Custom Visitor Data (Batch) | ✓ | ✗ |
| Send Security Data Event | ✗ | ✓ |
| Send Log Event | ✗ | ✓ |
| Send Entire Log Event | ✗ | ✓ |

Enter a name for the action and select the **Action Type**.

The following section describes how to set up parameters and options for each action.

### Send Entire Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | The name of the event. |
| Timestamp | The time of the event in seconds or milliseconds since the Unix epoch. The default value is the submission time if not provided. |
| Pretty Print | By default, the attribute keys are used. To use the attribute names as keys instead, enable this checkbox. Note that if the attribute names are updated, the payload names reflect these changes. |

### Send Entire Event Data (Batch)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | The name of the event. |
| Timestamp | The time of the event in seconds or milliseconds since the Unix epoch. The default value is the submission time if not provided. |
| Pretty Print | By default, the attribute keys are used. To use the attribute names as keys instead, enable this checkbox. Note that if the attribute names are updated, the payload names will also reflect these changes. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. Default is `10` minutes. |

### Send Custom Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | The name of the event. |
| Timestamp | The time of the event in seconds or milliseconds since the Unix epoch. The default value is the submission time if not provided. |
| Attributes | Define custom mappings between event attributes and vendor parameters. |

### Send Custom Event Data (Batch)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | The name of the event. |
| Timestamp | The time of the event in seconds or milliseconds since the Unix epoch. The default value is the submission time if not provided. |
| Attributes | Define custom mappings between event attributes and vendor parameters. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. Default is `10` minutes. |

### Send Entire Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | The name of the event. |
| Timestamp | The time of the event in seconds or milliseconds since the Unix epoch. The default value is the submission time if not provided. |
| Pretty Print | By default, the attribute keys are used. To use the attribute names as keys instead, enable this checkbox. Note that if the attribute names are updated, the payload names reflect these changes. |
| Include Current Visit Data with Visitor Data | Include current visit data with visitor data. |
| Exclude Current Visit Event Data | Exclude event data from the current visit data. |

### Send Entire Visitor Data (Batch)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | The name of the event. |
| Timestamp | The time of the event in seconds or milliseconds since the Unix epoch. The default value is the submission time if not provided. |
| Pretty Print | By default, the attribute keys are used. To use the attribute names as keys instead, enable this checkbox. Note that if the attribute names are updated, the payload names reflect these changes. |
| Include Current Visit Data with Visitor Data | Include current visit data with visitor data. |
| Exclude Current Visit Event Data | Exclude event data from the current visit data. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. Default is `10` minutes. |

### Send Custom Visitor Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | The name of the event. |
| Timestamp | The time of the event in seconds or milliseconds since the Unix epoch. The default value is the submission time if not provided. |
| Attributes | Define custom mappings between event attributes and vendor parameters. |

### Send Custom Visitor Data (Batch)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | The name of the event. |
| Timestamp | The time of the event in seconds or milliseconds since the Unix epoch. The default value is the submission time if not provided. |
| Attributes | Define custom mappings between event attributes and vendor parameters. |
| Batch Time To Live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. Default is `10` minutes. |

### Send Security Data Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Repository | The repository URL for the app with your integration. |

#### Security Metadata

| **Parameter** | **Description** |
| --- | --- |
| `source` | The user-friendly name of the security tool that generated this event (for example, Snyk, Dependabot). |
| `title` | A short (50-100 character) summary of the issue. |
| `message` | Detailed description of the issue, including explanation and remediation guidance. May include markdown formatting. |

#### Issue Classification

| **Parameter** | **Description** |
| --- | --- |
| `issueType` | Supported issue types: `Library Vulnerability`, `Container Vulnerability`, `Host Vulnerability`. |
| `issueId` | Standard identifier for the issue (for example, `CVE`, `CWE`, `CIS` benchmark rule). |
| `severity` | Defined severity level: `CRITICAL`, `HIGH`, `MEDIUM`, `LOW`, `INFO`. |

#### Entity Association

| **Parameter** | **Description** |
| --- | --- |
| `entityType` | Used to correlate the reported issue to a known entity in New Relic (for example, Host, Repository, AWS). |
| `entityLookupValue` | Helps locate the appropriate entity of the given type. |
| `entityGuid` | Unique identifier for a specific entity in New Relic. |

#### CVSSv3

| **Parameter** | **Description** |
| --- | --- |
| `cvssScore` | CVSSv3 score assigned to the CVE. |
| `cvssVector` | CVSSv3 vector describing the CVE. |

#### Issue Tracking

| **Parameter** | **Description** |
| --- | --- |
| `issueInstanceKey` | Unique identifier for this specific occurrence of the issue. |
| `issueVendorID` | Vendor-specific identifier for the issue, if different from `issueId`. |
| `disclosureURL` | URL to additional details on the issue (for example, vendor website, public disclosure sources). |

#### Remediation Guidance

| **Parameter** | **Description** |
| --- | --- |
| `remediationExists` | Indicates whether a known fix exists for this issue (`true` or `false`). |
| `remediationRecommendation` | Short-form guidance on resolving the issue (for example, `Upgrade PACKAGE_NAME to X.Y.Z`). |
| Event Metadata | Timestamp (milliseconds since epoch) of when the issue was detected. Defaults to the moment the data is sent to New Relic. |
| Custom Fields | Map any additional custom fields to be included in the log. |

### Send Log Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | The name of the event. |
| Timestamp | The time of the event in seconds or milliseconds since the Unix epoch. The default value is the submission time if not provided. |
| Attributes | Define custom mappings between event attributes and vendor parameters. |

### Send Entire Log Event

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 10,000
* Max time since oldest request: 60 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Timestamp | Milliseconds or seconds since epoch (integer), or ISO 8601-formatted timestamp (string). Defaults to ingest time if not provided. |
| Logtype | Primary field for identifying logs and matching parsing rules. |
| Custom Fields | These become attributes of the log message. |