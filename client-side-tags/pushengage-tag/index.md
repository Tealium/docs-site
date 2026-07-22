---
title: PushEngage Tag Setup Guide
description: This article describes how to set up the PushEngage tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/pushengage-tag/
---
PushEngage is a browser push notification platform that helps content website managers engage visitors by automatically segmenting and sending web push messages. The cloud-based tool offers features for setting up notification triggers, customer segmentation, automatic responses, A/B testing, and more

## Tag Configuration

First, go to the tag marketplace and add the PushEngage tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **API Key**: Your PushEngage API Key. API key lets you access PushEngage service.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|API key (`apiKey`)| [String]|
|Segment Name (`segmentName`)| [String/Array]|
|Profile ID (`profileId`)| [String]|
|Days (`days`)| [Number/Array]|

### Events

|Variable| Description|
|---| ---|
|Add a Segment to a Subscriber at the time of subscription| `init`|
|Add a Segment to a Subscriber on page load of your site| `add-to-segment`|
|Add a Dynamic Segment to a Subscriber| `add-to-dynamic-segment`|
|Remove a Subscriber from a Segment| `remove-to-segment`|
|Add Profile Id to a Subscribers| `add-to-profile`|
