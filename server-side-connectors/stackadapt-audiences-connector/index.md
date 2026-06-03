---
title: StackAdapt Audiences Connector Setup Guide
description: This article describes how to set up the StackAdapt Audiences connector.
url: https://docs.tealium.com/server-side-connectors/stackadapt-audiences-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: StackAdapt API
* API Endpoint: `https://api.stackadapt.com/graphql`
* Documentation: [StackAdapt GraphQL API](https://docs.stackadapt.com/graphql)

## Configuration

Go to the connector marketplace and add a new connector. For general instructions on how to add a connector, see [About connectors]().

After adding the connector, configure the following settings:
* **API Key**: Provide your StackAdapt API Key. If you do not have an API key, contact your StackAdapt team.
* **Environment**: Select the StackAdapt environment.
* **Advertiser ID**: The default advertiser ID. Override this value in the connector action mappings to set it dynamically.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Upsert a profile (Batch) | ✓ | ✗ |
| Add profile to profile list | ✓ | ✗ |
| Add profile to profile list (Batch) | ✓ | ✗ |
| Remove profile from profile list | ✓ | ✗ |
| Remove profile from profile list (Batch) | ✓ | ✗ |

The following section describes how to set up parameters and options for each action.

### Upsert a profile (Batch)

Create or update a profile in StackAdapt and add it to an existing profile list.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Raw email | Customer&#39;s email address. |
| Advertiser ID | Override the default advertiser ID set in the configuration. |
| Is Opted In | Whether the profiles have opted into email marketing. |
| Profile list ID | The ID of the profile list associated with the uploaded profile(s). |

#### Schema

| **Parameter** | **Description** |
| --- | --- |
| Is PII | Add parameters that represent personally identifiable information (PII). |
| Profile | Map the schema attributes to Tealium attributes. Ensure that you use the same parameters defined in the schema section. |
| Batch time to live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Add profile to profile list

Add a user to a profile list in StackAdapt.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Raw email | Customer&#39;s email address. |
| Advertiser ID | Override the advertiser ID set in the configuration. |
| List IDs | Profile list IDs to add the customer to. |

### Add profile to profile list (Batch)

Add a user to a profile list in StackAdapt.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Raw email | Customer&#39;s email address. |
| Advertiser ID | Override the advertiser ID set in the configuration. |
| List IDs | Profile list IDs to add the customer to. |
| Batch time to live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |

### Remove profile from profile list

Remove a user from a profile list in StackAdapt.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Raw email | Customer&#39;s email address. |
| Advertiser ID | Override the advertiser ID set in the configuration. |
| List IDs | Profile list IDs to add the customer to. |

### Remove profile from profile list (Batch)

Remove a user from a profile list in StackAdapt.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Raw email | Customer&#39;s email address. |
| Advertiser ID | Override the advertiser ID set in the configuration. |
| List IDs | Profile list IDs to add the customer to. |
| Batch time to live | Set the time to live (TTL) to specify how often batch actions are sent. Enter a value between `1` and `60` minutes. The default value is `10` minutes. |