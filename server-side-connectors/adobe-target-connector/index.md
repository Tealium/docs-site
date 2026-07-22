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

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **Authentication Token**: (Optional) Provide your authentication token if **Require Authentication** is enabled in the Profile API settings. The token expiration date appears in the Profile API settings. For more information, see [Adobe Target: Profile API settings](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/methods/profile-api-settings.html).


<blockquote>
We recommend that you set the trigger to **In Audience at End of Visit** or use a [delayed action](https://docs.tealium.com/about-delayed-actions/) of one hour to allow Adobe Target enough time to create visitor profiles for new site visitors.
</blockquote>


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
|Client|  <ul><li>Your client code provided by Adobe. This value appears in the API endpoint like this:`https://your-client-code.tt.omtrdc.net/m2/client/profile/update`</li></ul> |
|mboxpcID|  <ul><li>Either mboxpcID or mbox3rdPartyId is required. For more information, see [Adobe Target: Updating profiles](https://experienceleague.adobe.com/en/docs/target-dev/developer/api/profile-apis/profile-single-api).</li></ul> |
|mbox3rdPartyId|  <ul><li>Either mboxpcID or mbox3rdPartyId is required. For more information, see [Adobe Target: Updating profiles](https://experienceleague.adobe.com/en/docs/target-dev/developer/api/profile-apis/profile-single-api).</li></ul> |
|Attributes|  <ul><li>Parameter format is `profile.paramName`.</li><li>Not all parameter values need to exist for all pcIds or mbox3rdPartyId.</li><li>Parameters and values are case sensitive.</li><li>The current size limit is 8 KB for GET.</li><li>The calls to the profile update API do not count toward your mbox charges.</li></ul> |
