---
title: Nine Audience Match Connector Setup Guide
description: This article describes how to set up the Nine Audience Match connector.
url: https://docs.tealium.com/server-side-connectors/nine-audience-match-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Nine API
* API Version: v1
* API Endpoint: `https://pubsub.googleapis.com/`
* Documentation: [Nine API](https://cloud.google.com/pubsub/docs/overview)

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add User to Segment | ✓ | ✗ |
| Remove User from Segment | ✓ | ✗ |
| Remove User from All Segments | ✓ | ✗ |

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Private Key**  
 
Please enter your private key for the Google Pub/Sub connection.

## Actions - parameters and options

The following section lists the supported parameters for each action.

### Action - Add User to Segment

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Segment Name | (Required) Enter the name of your audience segment. |
| Client Name | (Required) Nine account ID. |
| Email (already SHA256 hashed) | Provide an email address that has already been SHA256 hashed. |
| Email (apply SHA256 hash) |Provide a plain text email address and the connector will whitespace trim, lowercase, and hash this value using the SHA256 hash. |

### Action - Remove User from Segment

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Segment Name | (Required) Enter the name of your audience segment. |
| Client Name | (Required) Nine account ID. |
| Email (already SHA256 hashed) | Provide an email address that has already been SHA256 hashed. |
| Email (apply SHA256 hash) |Provide a plain text email address and the connector will whitespace trim, lowercase, and hash this value using the SHA256 hash. |

### Remove User from All Segments

#### Action - Parameters

| **Parameter** | **Description** |
| --- | --- |
| Segment Name | (Required) Enter the name of your audience segment. |
| Client Name | (Required) Nine account ID. |
| Email (already SHA256 hashed) | Provide an email address that has already been SHA256 hashed. |
| Email (apply SHA256 hash) |Provide a plain text email address and the connector will whitespace trim, lowercase, and hash this value using the SHA256 hash. |

