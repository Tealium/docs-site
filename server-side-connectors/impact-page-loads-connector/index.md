---
title: Impact Page Loads Connector Setup Guide
description: This article describes how to set up the Impact Page Loads connector.
url: https://docs.tealium.com/server-side-connectors/impact-page-loads-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Landing Page Event| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

## Actions and Parameters

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Send Landing Page Event

| **Parameter** | **Description** |
| --- | --- |
| Campaign ID | (Required) Unique integer campaign identifier provided by Impact. |
| Page URL | (Required) Full landing page URL, for example: `https://www.example.com?utm_source=google&utm_medium=cpc`. |
| Custom Profile ID | (Required) Advertiser’s own user-specific value, for example: `cookie value`. |
| User Agent | (Required) String identifying the browser and operating system. |
| IP Address | (Required) String representing IP Address of the customer. |
| Referring URL | The URL of the page the click originated from. |
| Customer ID | Unique alphanumeric customer identifier your platform assigns to customer accounts. Do not use personally identifiable information. |
| Customer Email | SHA1 hash string of customer email address. |
| Event Date | Use a string value of `NOW` or dates in <a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a> or `dd-MMM-yyyy HH:mm:ss z` formats. `NOW` is used by default. |
| Customer Email Already Hashed | Check this box if the customer email is already hashed. |