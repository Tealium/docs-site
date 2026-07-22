---
title: PulsePoint HCP365 incoming webhook setup guide
description: This article describes how to use the PulsePoint HCP365 data source to create a webhook in your PulsePoint account and send actionable events to Tealium.
url: https://docs.tealium.com/server-side/data-sources/webhooks/setup-guides/pulsepoint-hcp365/
---
The PulsePoint HCP365 pixel is used to resolve the identity of a Healthcare Provider (HCP) visiting a pharmaceutical website. The purpose of the PulsePoint HCP 365 data source is to bring in the resolved identity of the HCP along with other data elements related to the HCP.

## Prerequisites

* PulsePoint HCP365 account
* Tealium for Pharma

## How it works

PulsePoint HCP365 offers webhook functionality that can be configured to send outgoing requests to an endpoint that you specify. These requests inform Tealium about activity in your PulsePoint account. When you add the PulsePoint data source within Tealium, a unique endpoint will be generated that you can then use within PulsePoint HCP365 to configure the PulsePoint webhook.

## PulsePoint data source

To configure the PulsePoint data source, perform the following steps:

1. Navigate to **Connect > Data Sources**.
1. Click **+Add Data Source**.
1. On the **Select a Platform** screen, select **Pharma** under **Categories**, and then select **PulsePoint HCP365**.
1. In the **Name** field under **Summary**, enter a name and click **Continue**.
1. Click **Continue**.
1. Select the `pulsepoint_hcp_identity` event specification under the **Pharma** category and click **Continue**: ![](https://docs.tealium.com/images/server-side/data-sources/webhooks/pulsepoint1.png)
1. (Optional) To download installation instructions, including the data source key, base code, and event tracking code, click **Download as PDF**.
1. Click **Save & Continue**.
A summary of the data source appears.
1. Click **Close**.

For more information, see [Create a data source](https://docs.tealium.com/create-data-source/).

The PulsePoint data source generates a unique URL to use as the HTTP GET OR POST URL in your PulsePoint configuration. The generated URL uses the following format:

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

After you create the PulsePoint HCP365 data source, note the following values: **Tealium Account Name**, **Tealium Profile Name**, and the **Data Source Key**. You will need these when configuring the webhook within PulsePoint HCP365.

## PulsePoint setup

After you configure your data source endpoint, configure the webhook in your PulsePoint account.

1. Log in to your PulsePoint HCP365 Application.
1. Navigate to **Webhook Support**.
1. Select `GET` or `POST` as the **Request Method**.
1. In the **URL** field, enter the endpoint URL that was generated when creating the data source in Tealium.
1. In the **Body** field, the event parameters must be included in each request to connect to your Tealium instance and the specific data source. See the [Event attributes](#event-attributes) section for a list of event parameters..  

## Event attributes

The following parameters must be included in each connection request:

* `tealium_account` - Your **Tealium Account Name**.
* `tealium_profile` - Your **Tealium Profile Name**.
* `tealium_datasource` - Your **Data Source Key**.

The following attributes are specific to PulsePoint and can be sent through the webhook. Ensure that each attribute includes the `pulsepoint_` prefix as shown in the table below. Refer to your PulsePoint documentation or contact the PulsePoint Support Team if you need help with the HCP365 data elements.

|Event Attribute| Type| Definition | Example|
|---| ---| ---| ---|
| `pulsepoint_npi` | String |National Provider Identifier (NPI) of the individual. | `12345` |
| `pulsepoint_url` | String| Page URL where an event occurred.| `https://www.brandhcp.com/psoriatic-arthritis/3-year-data/` |
| `pulsepoint_channel` | String | Channel Indicator (`1` - Site, `2` - Search). | `1` |
| `pulsepoint_token` | String | Unique identifier for pixel and/or placement. | `J7CYWG18ZB3F`|
| `pulsepoint_param1` | String | Optional parameter that can be used to describe the event. | key action |
| `pulsepoint_param2` | String | Optional parameter that can be used to describe the event. | key action |
| `pulsepoint_param3` | String | Optional parameter that can be used to describe the event. | key action |
| `pulsepoint_param4` | String | Optional parameter that can be used to describe the event. | key action |
| `pulsepoint_param5` | String | Optional parameter that can be used to describe the event. | key action |

