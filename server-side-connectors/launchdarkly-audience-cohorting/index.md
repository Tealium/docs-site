---
title: LaunchDarkly Audience Cohorting Connector Setup Guide
description: This article describes how to set up the LaunchDarkly Audience Cohorting connector.
url: https://docs.tealium.com/server-side-connectors/launchdarkly-audience-cohorting/
---
## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add Member to Segment | ✓ | ✗ |
| Remove Member from Segment | ✓ | ✗ |

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

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

