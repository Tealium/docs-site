---
title: ChatGPT Ads Custom Audiences Connector Setup Guide
description: Add visitors to or remove visitors from an OpenAI Custom Audience, and target that audience in ChatGPT Ads campaigns.
url: https://docs.tealium.com/server-side-connectors/chatgpt-ads-custom-audiences-connector/
---
The ChatGPT Ads Custom Audiences connector adds visitors to, or removes them from, an OpenAI Custom Audience. Target that audience in ChatGPT Ads campaigns for inclusion, exclusion, or bid adjustments.

The connector validates and SHA-256 hashes identifiers before transmission. Supported identifier types are email address, phone number, and Google Advertising ID (GAID).

## Requirements

This connector requires the following:

* An OpenAI Ads Manager account.
* An Ads API key, created in OpenAI Ads Manager under **Settings**. A key can access only the Custom Audiences in its own ad account.
* A Custom Audience. Create one in OpenAI Ads Manager, or create one from the connector using the **Create Custom Audience** admin task.

## API information

This connector uses the following vendor API:

* **API Name**: OpenAI Ads API.
* **API Version**: v1.
* **API Endpoint**: `https://api.ads.openai.com`.
* **Documentation**: [OpenAI Ads: Custom audiences](https://developers.openai.com/ads/custom-audiences) and [OpenAI Ads API OpenAPI spec](https://developers.openai.com/ads/openapi.json).

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 2000
* Max time since oldest request: 60 minutes
* Max size of requests: 4 MB

## Configuration

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following setting:

* **Ads API Key**: (Required) An Ads API key from OpenAI Ads Manager, under **Settings**. A key can access only the Custom Audiences in its own ad account.

After you configure the connector, click **Done**.

## Create a Custom Audience

Use the **Create Custom Audience** admin task to create an empty Custom Audience in OpenAI directly from the connector. The connector creates the audience with the connector's **Ads API Key**, in the ad account that key belongs to.

To create a Custom Audience:

1. In the connector, click **Create Custom Audience**.
1. Set the following fields:

    | Field | Description |
    | --- | --- |
    | **Audience Name** | (Required) A name for the new Custom Audience, 3 to 1,000 characters. |
    | **Description** | (Optional) A description of the audience, stored in OpenAI. Do not include personal data. |

1. Click **Create Custom Audience**.

The audience starts empty. The **Add to Custom Audience** action adds members.


<blockquote>
Each click creates a separate audience. If OpenAI returns no response, refresh the **Custom Audience** list before you try again, because the audience may already exist.
</blockquote>


If your ad account does not allow small or empty audiences, OpenAI rejects the request. Create the audience in OpenAI Ads Manager instead.

To rename or archive a Custom Audience, use OpenAI Ads Manager.

## Actions

| Action name | Visitor profile | Event data |
| --- | :---: | :---: |
| Add to Custom Audience | ✓ | ✓ |
| Remove from Custom Audience | ✓ | ✓ |

Click **Continue** to configure the connector actions. Enter a name for the action and select the action type from the list.

### Add to Custom Audience

Add visitors to an OpenAI Custom Audience. Adding a visitor who is already a member has no effect.

#### Parameters

| Parameter | Description |
| --- | --- |
| **API Key Override** | <ul><li>(Optional) An Ads API key to use for this action instead of the connector's **Ads API Key**. Map an attribute that holds the key, or enter the key as a custom value.</li><li>A custom value is stored in the action and shown in plain text. To keep the key out of the action, map it from an attribute.</li><li>The **Custom Audience** list always uses the connector's key. If this key belongs to a different ad account, enter the Custom Audience ID instead of selecting it.</li></ul> |
| **Custom Audience** | <ul><li>(Required) Select a Custom Audience, or enter its ID, for example `caud_123`.</li><li>To make a new audience, click **Create Custom Audience**, or create it in OpenAI Ads Manager.</li><li>The list leaves out archived audiences and shows up to 5,000 audiences. If your audience is not listed, enter its ID.</li><li>OpenAI needs about 25,000 matched users before you can use an audience for inclusion or bid adjustments. Exclusion audiences have no minimum. Expect fewer matched users than identifiers sent.</li></ul> |

#### Identifiers

Map at least one attribute. A visitor with no valid identifier is not sent, and the action reports a validation error.

| Identifier | Description |
| --- | --- |
| **Email Address (apply SHA256 hash)** | Map a plain-text email address. The connector trims and lowercases the value, keeps dots and plus tags, and hashes it. Values without exactly one `@`, or with spaces, are skipped. |
| **Email Address (already SHA256 hashed)** | Map a 64-character hexadecimal SHA-256 hash of the email address, trimmed and lowercased before hashing. |
| **Phone Number (apply SHA256 hash)** | Map a phone number that includes its country code, for example `+1 (415) 555-2671`. The connector removes spaces, dashes, parentheses, and periods, then hashes the E.164 number, for example `+14155552671`. Numbers without a leading `+` and country code are skipped. |
| **Phone Number (already SHA256 hashed)** | Map a 64-character hexadecimal SHA-256 hash of the E.164 phone number, for example of `+14155552671`. |
| **Google Advertising ID (GAID)** | Map a hyphenated GAID. Do not hash it. The connector sends it in lowercase and OpenAI hashes it. All-zero IDs are skipped. |

Mapping rules:

* Invalid values are skipped, and the visitor's other identifiers are still sent.
* Map each option once. If you map both Email Address options, or both Phone Number options, the already-hashed value is sent, and the plain-text value is hashed and sent only when the visitor has no valid hashed value.
* To send several values of one type, map a list attribute.

### Remove from Custom Audience

Remove visitors from an OpenAI Custom Audience. Removing a visitor who is not a member has no effect. OpenAI can reject a removal that would leave a campaign using this audience below its minimum size.

This action uses the same parameters as **Add to Custom Audience**. For more information, see [Add to Custom Audience](#add-to-custom-audience).

## Known limitations

* OpenAI needs about 25,000 matched users before you can use an audience for inclusion or bid adjustments. OpenAI recommends 100,000. Exclusion audiences have no minimum.
* Matched-user counts are shown in OpenAI Ads Manager as ranges, not exact values.
* OpenAI applies audience changes in the background. A successful send is not immediate membership. Processing typically takes 20 to 30 minutes.
* **Add to Custom Audience** and **Remove from Custom Audience** for the same visitor are not guaranteed to apply in order. A quick join-then-leave can briefly land in the wrong state.
* Custom Audiences cannot target users in the EEA or Switzerland. 
