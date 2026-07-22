---
title: Adition Tagging Connector Setup Guide
description: This article describes how to set up the Adition Tagging connector.
url: https://docs.tealium.com/server-side-connectors/adition-tagging-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Tag visitor| ✓| ✗|

## Configure Settings

Go to the **Connector Marketplace** and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Tag Visitor

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Endpoint URL|  <ul><li>(Optional) Default endpoint is <https://ad13.adfarm1.adition.com/tagging></li><li>Provide your assigned endpoint URL.</li><li>When provided, it will override the default endpoint</li><li>For example: <ul><li><https://adfarm1.adition.com/tagging></li><li><https://ad1.adfarm1.adition.com/tagging></li><li><https://ad2.adfarm1.adition.com/tagging></li><li><https://ad3.adfarm1.adition.com/tagging></li><li><https://ad11.adfarm1.adition.com/tagging></li><li><https://ad13.adfarm1.adition.com/tagging></li></ul> </li></ul> |
|Client ID|  <ul><li>Provide your Adition client ID.</li><li>Example: `3133`</li></ul> |
|Tag|  <ul><li>Map custom values to the keys and subkeys as configured in Adition.</li><li>Example: Map string `current` to `tag[tealium.abc_de]`.</li><li>You can add multiple mappings</li></ul> |
|Adition Cookie|  <ul><li>Map the string variable which contains the value from the Adition cookie sync to the cookie name: `UserID1` .</li></ul> |
