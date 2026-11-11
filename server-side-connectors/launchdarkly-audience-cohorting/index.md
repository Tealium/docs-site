---
title: LaunchDarkly Audience Cohorting Connector Setup Guide
description: This article describes how to set up the LaunchDarkly Audience Cohorting connector.
url: https://docs.tealium.com/server-side-connectors/launchdarkly-audience-cohorting/
---
## API information

This connector uses the following vendor API:

* API Name: LaunchDarkly API
* API Version: 20240415
* API Endpoint: `https://app.launchdarkly.com`
* Documentation: [LaunchDarkly API](https://docs.launchdarkly.com/)

## Actions

| Action name | Visitor profile | Event data |
| --- | :---: | :---: |
| Add Member to Segment | ✓ | ✗ |
| Remove Member from Segment | ✓ | ✗ |

## Configuration

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Client-Side ID**  
(Required) The client-side ID for the metric events environment. You can find the client-side ID on the **Projects** tab in your [LaunchDarkly Account settings page](https://app.launchdarkly.com/settings/members) under **Environments**.
* **Access Token**  
(Required) The access token must have a role that allows the `importEventData` action. LaunchDarkly strongly recommends using a dedicated access token with this permission. For more information, see [Scoping personal API access tokens](https://docs.launchdarkly.com/home/account-security/api-access-tokens#scoping-personal-api-access-tokens) and [Environments](https://docs.launchdarkly.com/home/organize/environments?q=environment) in the LaunchDarkly documentation.
* **Segment Name**  
(Required) The segment name in LaunchDarkly that you want to send the data to.
* **Segment ID**  
(Required) The unique identifier for the segment in LaunchDarkly.
* **Segment Description**  
The segment description provided in LaunchDarkly.
* **URL Override**  

After you configure the connector, click **Done**.
(For testing purposes only) Lets you override the URL of the actions.

## Actions

The following section lists the supported parameters for each action.

### Add Member to Segment

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Member ID | The visitor’s LaunchDarkly ID. |
| HTTP Request Session ID | Select this option if you want to send the session ID. The session ID is not sent by default. |

#### Member Parameters

| **Parameter** | **Description** |
| --- | --- |
| Last Name | The visitor's last name. |
| First Name | The visitor’s first name. |
| Email | The visitor’s email address. |
| Phone Number | The visitor’s phone number. |

### Remove Member from Segment

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Member ID | The visitor’s LaunchDarkly ID.|
| HTTP Request Session ID | Select this option if you want to send the session ID. The session ID is not sent by default. |

