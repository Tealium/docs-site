---
title: Kevel Connector Setup Guide
description: Set up the Kevel connector to send Tealium visitor and event data to Kevel Ad Server UserDB and Kevel Audience for ad targeting.
url: https://docs.tealium.com/server-side-connectors/kevel-connector/
---
Kevel (formerly Adzerk) is a retail media and ad serving platform. The Kevel connector sends Tealium visitor and event data to two Kevel products for ad targeting with first-party data:

* **Kevel Ad Server UserDB:** The user database that Kevel Ad Server uses for targeting when it selects an ad. The connector sets custom properties, interests, segment memberships, opt-out status, and GDPR consent on user records, and deletes user records on request.
* **Kevel Audience:** The Kevel audience management product. The connector adds users to and removes users from Kevel Audience segments.

The connector also includes admin tasks to create, update, and delete Ad Server segments and to create Kevel Audience segments.

## API information

This connector uses the following vendor APIs:

* Kevel Ad Server user data
  * **API Name**: Kevel UserDB API
  * **API Version**: v1
  * **API Endpoint**: `https://e-{network_id}.adzerk.net/udb/{network_id}`
  * **Documentation**: [Kevel: UserDB](https://dev.kevel.com/reference/userdb) and [Kevel: User Segments](https://dev.kevel.com/reference/segments)
* Kevel Ad Server segments and advertisers
  * **API Name**: Kevel Management API
  * **API Version**: v1
  * **API Endpoint**: `https://api.kevel.co/v1`
  * **Documentation**: [Kevel: Management API Overview](https://dev.kevel.com/reference/campaign-api-overview)
* Kevel Audience segment memberships
  * **API Name**: Kevel Audience Segment Manager API
  * **API Version**: 1.0
  * **API Endpoint**: `https://segments.cdp.{your-company}.audience.kevel.com` (the Segment Manager URL for your Kevel Audience account)
  * **Documentation**: [Kevel Audience: Segment Manager](https://docs.audience.kevel.com/api/http/segment-manager)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Network ID**
  * (Required) Your Kevel network ID. The network ID is the number in the URL of the Kevel UI: `app.kevel.co/#!/{networkId}/`. For example, if the URL is `https://app.kevel.co/#!/12345/`, the network ID is `12345`.
  * Enter a whole number, such as `12345`.
* **Ad Server API Key**
  * (Required for Ad Server actions) Your Kevel Ad Server API key.
  * To get an API key, open the Kevel UI, go to **Settings**, and generate or copy an API key.
* **Kevel Audience API Token**
  * (Required for Kevel Audience actions) Your Kevel Audience API token.
* **Kevel Audience Segment Manager URL**
  * (Required for Kevel Audience actions) The URL of the Kevel Audience Segment Manager API for your account, in the form `https://segments.cdp.{your-company}.audience.kevel.com`.
  * The URL must start with `https://` and its hostname must end in `.audience.kevel.com`. The connector rejects other hostnames, ports other than 443, query strings, and fragments.
* **Kevel Audience Region**
  * (Required for Kevel Audience actions) The region of your Kevel Audience account: `us-east-1`, `us-west-2`, `eu-central-1`, `eu-west-1`, `ap-southeast-1`, `ap-southeast-2`, `ap-northeast-2`, or `ap-south-1`.

The settings that you need depend on the actions and admin tasks that you use:

| Kevel product | Actions and admin tasks | Required settings |
| --- | --- | --- |
| Kevel Ad Server | All Ad Server actions, the Ad Server segment admin tasks, and the segment and advertiser drop-down lists | **Network ID** and **Ad Server API Key** |
| Kevel Audience | All Kevel Audience actions, the Create Kevel Audience Segment admin task, and the Kevel Audience segment drop-down lists | **Network ID**, **Kevel Audience API Token**, **Kevel Audience Segment Manager URL**, and **Kevel Audience Region** |

Kevel provides the API token, Segment Manager URL, and region for your Kevel Audience account. To get these values, contact your Kevel account team.

### Native Segments destination

The Kevel Audience actions work with segments attached to the **Kevel - Native Segments** destination of your network. The Create Kevel Audience Segment admin task attaches new segments to this destination automatically. If your network has no Kevel - Native Segments destination in the region of the **Kevel Audience Region** setting, Kevel returns an error. To set up the destination, contact your Kevel account team.

### Test the connection

To check your credentials, click **Test Connection**. The test checks each API whose credentials you entered:

* **Ad Server API key:** The test reads the segment list from the Kevel Management API and reads a test user record from Kevel UserDB. This test checks the API key and the network ID.
* **Kevel Audience API token:** The test lists the Kevel Audience segments for your network ID and region. The test requires the Segment Manager URL and region.

Enter at least one set of credentials. The test fails if you enter neither an Ad Server API key nor any Kevel Audience field, if you fill in only some of the Kevel Audience fields, or if any check fails.

After you configure the connector, click **Done**.

## Manage segments

The connector includes the following admin tasks for managing Kevel segments. After you create a segment, select it in the segment drop-down lists of the actions. The drop-down lists show the newest segments first. They load up to 10,000 Ad Server segments or advertisers and up to 2,000 Kevel Audience segments. If your network has more, enter the segment or advertiser ID instead.

### Create an Ad Server segment

To create a segment in Kevel Ad Server, click **Create Ad Server Segment** and enter the following values. This task requires the **Ad Server API Key**.

| **Parameter** | **Description** |
| --- | --- |
| Segment Name | (Required) The name of the segment, from 1 to 200 characters. |
| Segment Category | (Optional) The category of the segment in Kevel. |
| Segment Description | (Optional) A description of the segment. |

Kevel allows more than one segment with the same name. Before you create a segment, check the segment drop-down list for an existing segment with that name.

### Update an Ad Server segment

To change the name, category, or description of an Ad Server segment, click **Update Ad Server Segment** and enter the following values. This task requires the **Ad Server API Key**.

| **Parameter** | **Description** |
| --- | --- |
| Segment | (Required) Select the segment to update. |
| Segment Name | (Required) The new name of the segment, from 1 to 200 characters. |
| Segment Category | (Optional) The new category of the segment. Leave blank to keep the current category. This task can't clear a category. |
| Segment Description | (Optional) The new description of the segment. Leave blank to keep the current description. This task can't clear a description. |

### Delete an Ad Server segment

To delete an Ad Server segment from your Kevel network, click **Delete Ad Server Segment** and select the segment. This task requires the **Ad Server API Key**. The deletion is permanent. Kevel reports success even for a segment ID that doesn't exist, so a success message doesn't confirm which segment was deleted.

| **Parameter** | **Description** |
| --- | --- |
| Segment | (Required) Select the segment to delete. |


<blockquote>
Kevel accepts segment IDs that don't exist without returning an error. Actions that still reference a deleted segment continue to succeed but have no effect. After you delete a segment, update the actions that use it.
</blockquote>


### Create a Kevel Audience segment

To create a segment in Kevel Audience, click **Create Kevel Audience Segment** and enter the following values. This task requires the **Network ID** and the Kevel Audience settings.

| **Parameter** | **Description** |
| --- | --- |
| Segment Name | (Required) The name of the segment. If a segment with the same name exists, Kevel returns an error. |
| Segment Category | (Optional) The category of the segment in Kevel Audience. |
| Segment Description | (Optional) A description of the segment. |
| Static Segment | (Optional) Select this checkbox to mark the segment as static. A static segment has stable membership over time. Only static segments are available in Kevel Forecast. |

Kevel Audience creates the segment in the region of the **Kevel Audience Region** setting and attaches it to the **Kevel - Native Segments** destination for your network.

## Actions

Click **Continue** to configure the connector actions. Enter a name for the action and select the action type from the list.

| Action Name | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Set User Custom Properties | ✓ | ✓ |
| Add User Interest | ✓ | ✓ |
| Add User to Ad Server Segments | ✓ | ✓ |
| Remove User from Ad Server Segments | ✓ | ✗ |
| Add User to Retargeting Segment (Legacy) | ✓ | ✗ |
| Opt Out User | ✓ | ✗ |
| Set GDPR Consent | ✓ | ✗ |
| Forget User | ✓ | ✗ |
| Add Users to Kevel Audience Segment (Batched) | ✓ | ✓ |
| Remove Users from Kevel Audience Segment (Batched) | ✓ | ✗ |

The first nine actions in the table are Ad Server actions that write to Kevel UserDB. The last three are Kevel Audience actions. For the settings that each group requires, see [Configuration](#configuration).

The Ad Server actions identify the user by a user key, up to 1,024 characters. The connector removes leading and trailing spaces from the user key. The user key must match the user key that your site or app sends in Kevel ad decision requests. Otherwise, Kevel can't use the stored data when it selects an ad for the user.


<blockquote>
Kevel UserDB returns the same success response for every Ad Server write. Tealium can't detect a value that Kevel accepts but that is logically wrong, such as a segment ID that doesn't exist. Test each action with a known user key and confirm the result in Kevel.
</blockquote>


### Set User Custom Properties

Sets custom properties on the user record in Kevel UserDB.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User Key | (Required) The key of the user record in Kevel UserDB, up to 1,024 characters. |
| Custom Properties | (Required) Map Tealium attributes to custom property names. Map at least one property. The connector sends numbers, booleans, and strings with their original data types. The custom properties of one request can't exceed 8 KB (8,192 bytes). |


<blockquote>
Each request replaces all the custom properties of the user. Kevel doesn't merge the new properties with the stored properties. Kevel removes any stored property that the request doesn't include, including a mapped property whose attribute has no value for the visitor or event. If no mapped property has a value, the connector doesn't send a request and Kevel keeps the stored properties. If two actions set different properties for the same user, each action removes the properties of the other. Map all the properties that you want to keep in one action.
</blockquote>


### Add User Interest

Adds one interest to the user record in Kevel UserDB.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User Key | (Required) The key of the user record in Kevel UserDB, up to 1,024 characters. |
| Interest | (Required) One interest to add to the user record, for example `sports`. Kevel stores the value exactly as sent and doesn't split it on commas. For example, Kevel stores `news,tech` as one interest named `news,tech`. To add more than one interest, configure one action for each interest. |

### Add User to Ad Server Segments

Adds the user to one or more Ad Server segments. The existing segment memberships of the user stay in place.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User Key | (Required) The key of the user record in Kevel UserDB, up to 1,024 characters. |
| Segments | (Required) Select the segments to add the user to, or enter segment IDs. Each ID is a whole number without leading zeros. Enter from 1 to 1,000 segments. The connector removes duplicate segment IDs. |

Kevel accepts any segment ID without checking that the segment exists. To avoid IDs that don't match a segment, select segments from the drop-down list.

### Remove User from Ad Server Segments

Removes the user from one or more Ad Server segments. Kevel removes only the listed segment IDs. Other segment memberships of the user stay in place. Removing a segment that the user isn't a member of has no effect.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User Key | (Required) The key of the user record in Kevel UserDB, up to 1,024 characters. |
| Segments | (Required) Select the segments to remove the user from, or enter segment IDs. Each ID is a whole number without leading zeros. Enter from 1 to 1,000 segments. The connector removes duplicate segment IDs. |

Kevel accepts any segment ID without checking that the segment exists. To avoid IDs that don't match a segment, select segments from the drop-down list.

### Add User to Retargeting Segment (Legacy)

Adds the user to an advertiser retargeting segment through the legacy Kevel retargeting endpoint. Kevel no longer documents this endpoint. For new configurations, use the Ad Server segment actions instead.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User Key | (Required) The key of the user record in Kevel UserDB, up to 1,024 characters. |
| Advertiser | (Required) Select the Kevel advertiser that owns the retargeting segment. The value must be an advertiser ID, which is a whole number without leading zeros. |
| Segment | (Required) Select the Ad Server segment to use as the retargeting segment. The value must be a segment ID, which is a whole number without leading zeros. |

Kevel returns the same success response for every write, so Tealium can't detect an advertiser or segment ID that doesn't exist. Select both values from the drop-down lists.

### Opt Out User

Sets the opt-out status on the user record in Kevel UserDB.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User Key | (Required) The key of the user record in Kevel UserDB, up to 1,024 characters. |


<blockquote>
You can't undo an opt-out through this connector.
</blockquote>


### Set GDPR Consent

Sets the GDPR consent status on the user record in Kevel UserDB. For more information about managing consent in Tealium, see [Server-side consent management](https://docs.tealium.com/server-side-consent-management/).

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User Key | (Required) The key of the user record in Kevel UserDB, up to 1,024 characters. |
| GDPR Consent | (Required) The GDPR consent status of the user: `true` if the user gave consent or `false` if the user didn't. Values aren't case-sensitive. The connector sends the value to Kevel as a boolean and rejects any other value. |

### Forget User

Permanently deletes the user record and all its data from Kevel UserDB.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User Key | (Required) The key of the user record to delete, up to 1,024 characters. |


<blockquote>
You can't undo the deletion. The action deletes the user record every time it runs, so trigger it only for users who requested deletion.
</blockquote>


### Add Users to Kevel Audience Segment (Batched)

Adds users to a Kevel Audience segment. If a user doesn't exist in Kevel Audience, Kevel creates the user.

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50
* Max time since oldest request: 15 minutes
* Max size of requests: 1 MB

The connector sends each batch to Kevel as one request, because Kevel Audience accepts at most 50 memberships per request.


<blockquote>
This action and the Remove Users from Kevel Audience Segment (Batched) action use separate batches. If you add and remove the same user and segment within a short time, Kevel can apply the two changes in either order.
</blockquote>


#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User ID Type | (Required) The type of user ID. For the list of types, see [User ID types](#user-id-types). |
| User ID | (Required) The user ID. The connector formats or hashes the value according to the user ID type. |
| Segment | (Required) Select the Kevel Audience segment to add users to, or enter a segment ID, for example `es_02f28ebe`. Segment IDs contain 1 to 128 letters, numbers, hyphens, or underscores. |


<blockquote>
If you delete a Kevel Audience segment in Kevel, Kevel still reports success for the batched actions that target it and keeps the memberships. Remove or update those actions when you delete their segment.
</blockquote>


#### User ID types

| User ID Type | Kevel user ID type | Value to map |
| --- | --- | --- |
| Email (apply SHA-256) | `email_sha256` | A plain-text email address. The connector trims and lowercases the address, checks that it's a valid email address, and hashes it with SHA-256. |
| Email SHA-256 (pre-hashed) | `email_sha256` | An email address, trimmed and lowercased before hashing with SHA-256, as a 64-character hexadecimal string. |
| Email MD5 (pre-hashed) | `email_md5` | An email address, trimmed and lowercased before hashing with MD5, as a 32-character hexadecimal string. |
| Email SHA-256 Base64 (pre-hashed) | `email_sha256b64` | An email address, trimmed and lowercased before hashing with SHA-256, with the hash encoded as URL-safe Base64. |
| Phone E.164 (apply SHA-256) | `phone_e164_sha256` | A phone number that includes the country code, for example `+14155552671` or `0044 20 7946 0958`. The connector removes spaces, dots, dashes, and parentheses, replaces a leading `00` with `+`, adds a missing `+`, and hashes the result with SHA-256. The connector can't add a missing country code, so a national number such as `4155552671` is hashed as a different number. |
| Phone E.164 SHA-256 (pre-hashed) | `phone_e164_sha256` | A phone number in E.164 format, including the leading `+`, hashed with SHA-256, as a 64-character hexadecimal string. |
| CRM ID | `crm` | Your CRM ID for the user. The connector removes leading and trailing spaces and sends the value otherwise unchanged. |
| Kevel Audience first-party cookie | `1pCookie` | The Kevel Audience first-party cookie ID. The connector removes leading and trailing spaces and sends the value otherwise unchanged. |
| Android Advertising ID | `gaid` | The Google advertising ID of an Android-powered device. The connector removes leading and trailing spaces and sends the value otherwise unchanged. |
| iOS IDFA | `idfa` | The Identifier for Advertisers (IDFA) of an iOS device. The connector removes leading and trailing spaces and sends the value otherwise unchanged. |

For pre-hashed user ID types, the connector converts hexadecimal values to lowercase. The connector rejects values that don't have the length or format listed for the user ID type.

The connector rejects empty user IDs and the values `null`, `undefined`, and `none`. This check isn't case-sensitive.

### Remove Users from Kevel Audience Segment (Batched)

Removes users from a Kevel Audience segment. Removing a user who isn't a member of the segment has no effect.

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50
* Max time since oldest request: 15 minutes
* Max size of requests: 1 MB

The connector sends each batch to Kevel as one request, because Kevel Audience accepts at most 50 memberships per request.


<blockquote>
This action and the Add Users to Kevel Audience Segment (Batched) action use separate batches. If you add and remove the same user and segment within a short time, Kevel can apply the two changes in either order.
</blockquote>


#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| User ID Type | (Required) The type of user ID. For the list of types, see [User ID types](#user-id-types). |
| User ID | (Required) The user ID. The connector formats or hashes the value according to the user ID type. |
| Segment | (Required) Select the Kevel Audience segment to remove users from, or enter a segment ID, for example `es_02f28ebe`. Segment IDs contain 1 to 128 letters, numbers, hyphens, or underscores. |

The user ID types, user ID rules, and segment requirements for this action match [Add Users to Kevel Audience Segment (Batched)](#add-users-to-kevel-audience-segment-batched).

## Rate limits

Kevel applies the following rate limits:

* **Kevel Ad Server (UserDB and Management API):** 10 requests per second per network. The limit applies to all requests for the network, including requests from the admin tasks, the drop-down lists, and other tools.
* **Kevel Audience:** 250 requests per second for all endpoints.

Except for the two batched actions, each action sends one request every time it runs. Requests that exceed a rate limit can fail. Before you trigger these actions from high-volume events or audiences, compare your expected request rate with these limits.
