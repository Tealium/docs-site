---
title: Zapier incoming webhook setup guide
description: This article describes how to use the Zapier data source to create a webhook in your Zapier account and send actionable events to Tealium.
url: https://docs.tealium.com/server-side/data-sources/webhooks/setup-guides/zapier/
---
## Prerequisites

* Zapier account
* Tealium AudienceStream account

## How it works

Zapier lets you send webhooks from Zaps to an endpoint that you specify. These requests notify Tealium AudienceStream about activity in your Zapier account. When you add the Zapier data source, a unique endpoint is generated that you use to configure the Zapier webhook.

## Zapier data source

The Zapier data source generates a unique URL to use in your Zapier Webhook configuration. The data source also generates query string parameters for the Zapier webhook.

The webhook URL is:

```
https://collect.tealiumiq.com/event
```

The following query string parameters are required in the Zapier configuration:

```
tealium_acount=ACCOUNT
tealium_profile=PROFILE
tealium_datasource=DATA_SOURCE_KEY
tealium_event=EVENT_NAME
```

To add the Zapier data source to your Tealium profile, see [Data Sources](https://docs.tealium.com/about-data-sources/). After you add and connect the data source, save and publish your profile.

## Zapier setup

After you have your data source endpoint, go to your Zapier account to create the webhook. When creating the Zapier webhook, use the URL and query string parameters for the data source, followed by any additional event attributes that you need. If your Zapier events are intended to enrich visitor profiles within AudienceStream, be sure to include a user ID.

![](https://docs.tealium.com/images/server-side/zapierwebhooksetup-png.png)

For information on setting up Zapier Webhooks, see [Send Webhooks in Zaps](https://help.zapier.com/hc/en-us/articles/8496326446989-Send-webhooks-in-Zaps).
