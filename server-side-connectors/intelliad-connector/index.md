---
title: intealliAd Connector Setup Guide for Customer Data Platform (CDP)
description: This article describes how to set up the intealliAd connector.
url: https://docs.tealium.com/server-side-connectors/intelliad-connector/
---
## Requirements

Client ID (provided to you by the intelliAd CSM team)

## Supported Actions

|**Action Name**| **Trigger on Audience**| **Trigger on Streams**|
|---| ---| ---|
|Add User To Segment| ✓| ✗|

## Configure Settings

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

To configure your vendor, follow these steps:

1. In the **Configure** tab, provide a title for the Connector instance.

1. Enter the **Client ID** that you received from intelliAd for your account.

1. Provide additional notes about your implementation.

## Action Settings - Parameters and Options

Click **Continue** to configure the connector actions. Enter a name for the action and select the action type from the list.

### Action - Add User to Segment

#### Parameters

1. **Client ID**: (Optional) Overrides the value provided in the **Configuration** tab.
1. **Add to Segment Config**: (Required) Map your Attribute(s) to the data fields for which you want to provide useful information. See options below.

|**Option**| **Description**|
|---| ---|
|Segment (seg)| Comma-separated segment id list. Segment-IDs will be provided from the intelliAd CSM team or the intelliAd frontend.|
|intelliAd User ID (`iauuid`)| intelliAd User-ID, passed to the Connector|
|Exclude (exclude)| Exclude given segments for current user. Only possible value is `1`.|
