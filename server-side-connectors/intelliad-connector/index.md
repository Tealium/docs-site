---
title: intealliAd Connector Setup Guide for AudienceStream
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

Go to the Connector Marketplace and add a new intealliAd Connector. Read the [Connector Overview]() article for general instructions on how to add a Connector.

To configure your vendor, follow these steps:

1. In the **Configure** tab, provide a title for the Connector instance.

1. Enter the **Client ID** that you received from intelliAd for your account.

1. Provide additional notes about your implementation.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. It&#39;s where you&#39;ll set up actions and trigger them.

This section describes how to set up parameters and options for the action.

### Action - Add User to Segment

#### Parameters

1. **Client ID**: (Optional) Overrides the value provided in the **Configuration** tab.
1. **Add to Segment Config**: (Required) Map your Attribute(s) to the data fields for which you want to provide useful information. See options below.

|**Option**| **Description**|
|---| ---|
|Segment (seg)| Comma-separated segment id list. Segment-IDs will be provided from the intelliAd CSM team or the intelliAd frontend.|
|intelliAd User ID (`iauuid`)| intelliAd User-ID, passed to the Connector|
|Exclude (exclude)| Exclude given segments for current user. Only possible value is `1`.|
