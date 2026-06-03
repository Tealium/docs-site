---
title: Auth0 incoming webhook setup guide
description: This article describes how to use the Auth0 data source to create a webhook in your Auth0 account and send actionable events to Tealium.
url: https://docs.tealium.com/server-side/data-sources/webhooks/auth0/
---
## How it works

The Auth0 data source receives data from all Tealium actions available in the Auth0 marketplace after a user has been added to the database.

## Requirements

Auth0 incoming webhook requires the following:

* Tealium EventStream or Tealium AudienceStream
* Auth0 account

### Add an Auth0 data source

To add the Auth0 data source to your Tealium Customer Data Hub profile, see [Data Sources](). After adding and connecting the data source, save and publish your profile.
Adding the Auth0 data source to your Tealium Customer Data Hub profile generates a unique URL and a data source key to use in your webhook configuration. The format of the URL is as follows:

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

### Auth0 setup

After you connect Auth0 to your Tealium Customer Data Hub profile, configure the webhook using the following steps:

1. Log in to your Auth0 account.
1. From the left side menu, select **Actions &gt; Library**.
1. Click **Create Action &gt; Use a Marketplace Integration**.
1. Add **Tealium Action** to your library. 
1. Input the **Tealium Account Name**, **Tealium Profile Name** and **Data Source key** for the action.
1. From the left side menu, select **Actions &gt; Flow**.
1. Select the appropriate flow and add the action to the flow.

For more information, see [Auth0: Understand How Auth0 Actions Work](https://auth0.com/docs/customize/actions/actions-overview#what-can-you-do-with-actions-).

### Events and attributes

All incoming Auth0 event attributes are prefixed with `auth0_`. For example, for the `user_id` attribute, Auth0 will send the matching EventStream event attribute `auth0_user_id` (all lowercase). The Auth0 webhook API sends flattened JSON objects to Tealium.

|Key| Type| Example|
|---| ---| ---|
|`tealium_event`| String| `auth0_user_login`|
|`auth0_email_address`| String| `user@example.com`|
|`auth0_user_id`| Number| `8237572`|
|`auth0_phone_number`| Number| `0123456789`|
|`auth0_ip`| String| `255.255.255.255`|
|`auth0_city`| String| `San Diego`|
|`auth0_last_name`| String| `John`|
|`auth0_first_name`| String| `Doe`|

For more information, see [Actions Triggers: post-user-registration - Event Object](https://auth0.com/docs/customize/actions/flows-and-triggers/post-user-registration-flow/event-object).

## Vendor Documentation

* [Auth0: Introduction to Integrating with Auth0](https://auth0.com/docs/customize/integrations/marketplace-partners/introduction-to-integrating-with-auth0)
* [Auth0: Understand How Auth0 Actions Work](https://auth0.com/docs/customize/actions/actions-overview#what-can-you-do-with-actions-)