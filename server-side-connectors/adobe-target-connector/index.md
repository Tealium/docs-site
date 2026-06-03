---
title: Adobe Target Connector Setup Guide
description: This article describes how to set up the Adobe Target connector.
url: https://docs.tealium.com/server-side-connectors/adobe-target-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Adobe Profile API
* API Endpoint: `https://your-client-code.tt.omtrdc.net/m2/client/profile/update`, where `your-client-code` is your Adobe Target instance ID.
* Documentation: [Adobe: Profile API settings](https://experienceleague.adobe.com/en/docs/target-dev/developer/implementation/methods/profile-api-settings)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **Authentication Token**: (Optional) Provide your authentication token if **Require Authentication** is enabled in the Profile API settings. The token expiration date appears in the Profile API settings. For more information, see [Adobe Target: Profile API settings](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/methods/profile-api-settings.html).

 We recommend that you set the trigger to **In Audience at End of Visit** or use a [delayed action]() of one hour to allow Adobe Target enough time to create visitor profiles for new site visitors. 

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Single Profile Update | ✓ | ✗ |

Enter a name for the action and select the **Action Type**.

The following section describes how to set up parameters and options for each action.

### Single Profile Update

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Client|  &lt;ul&gt;&lt;li&gt;Your client code provided by Adobe. This value appears in the API endpoint like this:`https://your-client-code.tt.omtrdc.net/m2/client/profile/update`&lt;/li&gt;&lt;/ul&gt; |
|mboxpcID|  &lt;ul&gt;&lt;li&gt;Either mboxpcID or mbox3rdPartyId is required. For more information, see [Adobe Target: Updating profiles](https://experienceleague.adobe.com/en/docs/target-dev/developer/api/profile-apis/profile-single-api).&lt;/li&gt;&lt;/ul&gt; |
|mbox3rdPartyId|  &lt;ul&gt;&lt;li&gt;Either mboxpcID or mbox3rdPartyId is required. For more information, see [Adobe Target: Updating profiles](https://experienceleague.adobe.com/en/docs/target-dev/developer/api/profile-apis/profile-single-api).&lt;/li&gt;&lt;/ul&gt; |
|Attributes|  &lt;ul&gt;&lt;li&gt;Parameter format is `profile.paramName`.&lt;/li&gt;&lt;li&gt;Not all parameter values need to exist for all pcIds or mbox3rdPartyId.&lt;/li&gt;&lt;li&gt;Parameters and values are case sensitive.&lt;/li&gt;&lt;li&gt;The current size limit is 8 KB for GET.&lt;/li&gt;&lt;li&gt;The calls to the profile update API do not count toward your mbox charges.&lt;/li&gt;&lt;/ul&gt; |
