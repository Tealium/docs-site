---
title: Bold360 (formerly BoldChat) Tag Setup Guide
description: This article describes how to set up the Bold360 (formerly BoldChat) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/bold360-formerly-boldchat-tag/
---
## Tag Tips

* Configuration values are found by going to Bold360 and clicking **Setup &gt; HTML &gt; Generate Visitor Monitor HTML.**
* The Conversion Tracking event is sent automatically when there is an Order ID (`_corder`) from the E-Commerce extension.
* Mapping a value to Conversion Ref also triggers Conversion Tracking.
* Use the mapping toolbox to send additional visitor information.

## Tag Configuration

First, go to Tealium's tag marketplace and add the Bold360 (formerly BoldChat) tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Account ID**
* **Website ID**
  * Optional
  * Only add if specified in Visitor Monitor HTML

* **Invitation Definition ID**
  * Leave blank for no proactive Invitation or set dynamic invitation IDs using mapping.

* **Conversion Code ID**
  * Conversion Code ID is found in Conversion Tracking HTML.
  * This value only sent for a conversion event.

* **Floating Chat Button Definition ID**

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`AccountID`|  <ul><li>Account ID</li></ul> |
|`WebsiteDefID`|  <ul><li>Website Definition ID</li></ul> |
|`InvitationDefID`|  <ul><li>Proactive Invitation Definition ID</li></ul> |
|`FloatingChatButtonDefID`|  <ul><li>Floating Chat Button Definition ID</li></ul> |
|`VisitName`|  <ul><li>Visitor Name</li></ul> |
|`VisitPhone`|  <ul><li>Visitor Phone</li></ul> |
|`VisitEmail`|  <ul><li>Visitor Email</li></ul> |
|`VisitRef`|  <ul><li>Visitor ID</li></ul> |
|`VisitInfo`|  <ul><li>Visitor Info</li></ul> |
|`CustomUrl`|  <ul><li>Custom URL</li></ul> |
|`WindowParameters`|  <ul><li>Window Parameters</li></ul> |
|`ConversionCodeID`|  <ul><li>Conversion Code ID</li></ul> |
|`ConversionRef`|  <ul><li>Conversion ID or Order ID</li></ul> |
|`ConversionAmount`|  <ul><li>Conversion Amount</li></ul> |
|`ConversionInfo`|  <ul><li>Conversion Info</li></ul> |
