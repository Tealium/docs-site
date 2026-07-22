---
title: Sprinklr Universal Pixel Tag Setup Guide
description: This article describes how to set up the Sprinklr Universal Pixel Tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/sprinklr-universal-pixel-tag/
---
## Tag tips

* Use mappings to dynamically set the client ID.
* Supports these E-Commerce extension parameters:
    * Order Subtotal (`_csubtotal`)
    * Order Currency (`_ccurrency`)
    * List of Quantities (`_cquan`)
* Quantity is the total number of all items for a particular event. If no quantity value is provided through mapping, then the quantity is calculated from the list of product quantities array from the E-Commerce extension, if available.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [about-tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Client ID**: Your Sprinklr-provided client ID.
* **Generate Event ID**: Automatically generate an event ID for every Sprinklr tracking event.
<!--

### Leads API


<blockquote>
This feature requires an active [Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/).
</blockquote>


To support Sprinklr Leads API Connector, set **Generate Event ID** to `true`.  When **Generate Event ID** is enabled, this tag generates a unique event ID for each event tracked and sends it as an attribute to Tealium EventStream for use in the Sprinklr Leads API Connector and passes it to the Sprinklr Universal Pixel in the `event_id` parameter. This event ID attribute may be mapped in the connector to synchronize the web-based tag with server-side integration. 

The tag sends event IDs using generated event attributes using the following naming convention:

```nohl
sprinklr_event_id_{SPRINKLR_EVENT}_{TAG_UID}
```

For example, a purchase event from tag #32 would send the following attribute and value:

```json
{
  "sprinklr_event_id_Purchase_32": "028b2ade7478..."
}
```

A page view event from the same tag would send the following attribute and value:

```json
{
  "sprinklr_event_id_PageView_32": "084b1cda7461..."
}
```

#### Deduplication

To ensure proper event deduplication, the event ID from the Sprinklr Universal Pixel tag must be included in the payload sent by the Tealium Collect tag. To do this, use the following steps:

* From the **Tag Timing** drop-down, select **Prioritized**.
* Set the **Bundle Flag** toggle to `On`.
* Use the [Load Order Manager screen](https://docs.tealium.com/load-order-manager/) to fire the Sprinklr Universal Pixel tag before the Tealium Collect tag. We recommend that you fire the Tealium Collect tag last. -->

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Tag Configurations and Global Parameters

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `client_id` | String | Client ID. |
| `eventId` | String | Event ID. |
| `leadId` | String | Lead ID. |
| `custom.myvar` |  | Custom parameter. |
| `generate_event_id` | Boolean | Generate event ID. |

### E-Commerce

| Variable | Description |
|:---------|:------------|
| `value` | Value (Overrides `_csubtotal`). |
| `currency` | Currency (Overrides `_ccurrency`). |
| `product_quantity` |  List of product quantities (Overrides `_cquan`). |
| `quantity` | The total number of all items for the event. |

### User Data

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `userInfo.firstName` | String | The first name of the customer. |
| `userInfo.lastName` | String | The last name of the customer. |
| `userInfo.fullName` | String | The full name of the customer. |
| `userInfo.customerId` | String | The unique identifier for the customer. |
| `userInfo.anonymousId` | String | Automatically sends Tealium Visitor ID, map a variable to override. The unique identifier for a customer who is not registered as a user. |
| `userInfo.phoneNo` | String | The phone number of the customer. |
| `userInfo.email` | String | The email of the customer. |