---
title: Clicktale Carmel Tag Setup Guide
description: This article describes how to set up the Clicktale Carmel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/clicktale-carmel-tag/
---## Tag tips

* Override the standard config values using mappings.
* To pass audiences and badges to Clicktale:
  * Contact your Clicktale representative to enable the receiving of this data.
  * When mapping a badge, enter the name as it should appear in Clicktale.
  * Set **Send All Audiences** to `True` to send all audiences to Clicktale in the following format:  
`window.ClicktaleEventHandler(["Tealium Audience: AUDIENCE NAME", ...]);`
* Set **Send Replay Link** to `True` to make your Clicktale replay link available as the server-side attribute `clicktale_replay_link`.
* Contact your Clicktale representative to enable the generation of the replay link.
* Server-side attributes will appear in the current account and profile.
* Use a mapping to override `tealium_profile` .

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Title**
  * (Required) Identifies the tag instance.
  * Clicktale Carmel is the default name.
  * When using multiple tags by the same vendor, assign a unique name
* **Partition**
  * The partition where data is sent.
  * Example: **www07**
* **Project GUID / PTC ID**
  * Clicktale Project GUID
  * Example: **11111111-1111-1111-1111-11111111111**
* **Send Replay Link**
  * Select **True** to make your Clicktale Replay Link available as a server-side attribute.
* **Send All Audiences**
  * Select **True** to send each audience to Clicktale in the format window.
  * Example: `ClicktaleEventHandler(["Tealium Audience: AUDIENCE NAME", ...]);.`
* **Send Events to ClickTale**
  * Select **True** to send Event Data to Clicktale.

## Applying load rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag. The 'Load on All Pages' rule is the default load rule. To load this tag on a specific page, create a new load rule with the relevant conditions.

* Load this Tag on the page where you want to track the visitor's mouse movements.
* We recommend that this tag loads after the page has rendered completely.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`partition`|  <ul><li>String</li><li>Partition.</li><li>The partition where data is sent.</li><li>Map to this variable to dynamically configure the server partition value.</li></ul> |
|`project_guid`|  <ul><li>String</li><li>Project GUID.</li><li>Map to this variable to set the project guide field.</li></ul> |
|`send_replay_link`|  <ul><li>String, Boolean</li><li>Send Clicktale Replay Link</li><li>Values are **true** or **false**.</li></ul> |
|`send_audiences`|  <ul><li>String, Boolean</li><li>Send all audiences.</li><li>Values are **true** or **false**.</li></ul> |
|`tealium_account`|  <ul><li>String</li><li>Tealium Account.</li></ul> |
|`tealium_profile`|  <ul><li>String</li><li>Tealium Profile.</li></ul> |
|`SendEventsToClicktale`|  <ul><li>String</li><li>Toggle on to Send Events to Clicktale</li></ul> |

## Vendor Documentation

* [How to request an integration](https://uxanalyser.zendesk.com/hc/en-gb/articles/4405613239186 "https://uxanalyser.zendesk.com/hc/en-gb/articles/4405613239186")
* [Live Signals Implementation](https://uxanalyser.zendesk.com/hc/en-gb/articles/4409749139346-Live-Signals "https://uxanalyser.zendesk.com/hc/en-gb/articles/4409749139346-Live-Signals")
* [Tealium Integration](http://wiki.clicktale.com/Article/Tealium_Integration)
* [Frequently Asked Questions](http://wiki.clicktale.com/Article/Frequently_asked_questions)
