---
title: Consent management
description: Learn to implement consent management in remote commands.
url: https://docs.tealium.com/platforms/remote-commands/consent-management/
---
When you enable [consent management](https://docs.tealium.com/platforms/getting-started-mobile/consent-management/) in a Tealium mobile library a user must consent to tracking before any tracking data is sent from the device. The user's consent must also be enforced in remote commands and the third-party vendor SDKs that are integrated into your app. The following scenarios describe how to handle consent in remote commands.

## Consent Scenarios

When you prompt a user for consent in your app there are three possible scenarios that determine what tracking data is sent from the device:

* A user declines all tracking
* A user consents to all tracking
* A user consent to partial tracking

### User declines all tracking

If a user declines consent to all tracking, the Tealium mobile library prevents all standard tracking requests from leaving the device or from being sent to any remote commands. However, if the **Remote API** option is enabled, it generates an additional call with a special event type `remote_api`. This call ignores all offline queueing and consent restrictions. 

The `remote_api` call does not any send data to JavaScript tags loaded by Tealium iQ, or to Tealium server-side products, such as AudienceStream or EventStream. Instead, it is used to trigger the following remote commands: 

* Functional remote commands (such as those that support necessary functionality in the app).
* Remote commands from third-party SDKs with built-in consent and/or offline queueing support, that expect an unfiltered stream of app events.

### User consents to all tracking

If a user consents to all tracking, then any remote command can be triggered. Upon consent, the Tealium library initializes the remote command and any mapped events and data are sent to the vendor SDK.

Some vendor SDKs require you to call an opt-in command before remote commands are triggered. Refer to each [vendor integration](https://docs.tealium.com/platforms/remote-commands/integrations/) for the specific command.


### User consents to partial tracking

If a user grants partial consent to specific categories, then the following applies:

* The `grant_partial_consent` event is sent with the `consent_categories` attribute.
* All JSON remote commands are triggered. 
* Remote command tags are only triggered if they are assigned to one of the categories that the user has consented to, or if the tag has been omitted from consent.

Learn more about [consent categories](https://docs.tealium.com/iq-tag-management/consent-management/consent-preferences-dialog/manage/) and the [consent event specifications](https://docs.tealium.com/consent-change-event-specifications/).

## Remote API Call

How the **Remote API** option affects a remote command depends on whether the remote command is implemented using a JSON configuration file or by Tealium iQ.

### JSON Remote Commands

A `remote_api` call triggers all remote commands that are configured using a JSON file. All the mapping logic is applied and the commands are executed. To enforce consent in a vendor SDK using a JSON configuration file, map the Tealium consent events to the supported vendor method.

In this example with Braze, the Tealium consent events are mapped to the vendor consent methods for Android:

```json
{
  "commands": {
    "grant_full_consent": "enableSDK",
    "decline_consent": "disableSDK,wipeData"
  }
}
```

Learn more about [JSON configuration mappings](https://docs.tealium.com/platforms/remote-commands/vendor-integrations/#mappings).

### Remote Command Tags

To send consent events to remote command tags, you must configure the tag to expect `remote_api` events. By default, tags are only configured to expect `view` and `link` calls.

To update a tag to expect `remote_api` calls, change the list of events to the following:
```javascript
u.ev = { remote_api: 1 }; // remove "view" and "link" to avoid double-counting when remote_api is enabled
```

The following example shows how to disable tracking in the Braze Mobile Remote Command tag. Map the `tealium_event` variable to the Braze command `Disable Data Collection (disableSDK)`. 
Learn more about [consent event specifications](https://docs.tealium.com/consent-change-event-specifications/).

![](https://docs.tealium.com/images/platforms/remote-commands/remote-command-tag-mapping-consent.png)

For more information on how to check which events a tag is set to listen to, see [How to Check if a Tag will Fire on 'View' or 'Link' Calls](https://support.tealiumiq.com/en/support/solutions/articles/36000363410-how-to-check-if-a-tag-will-fire-on-view-or-link-calls).

## Vendor-Specific Consent Configuration

Each vendor SDK manages consent differently. For more information on configuring consent options for each vendor SDK, refer to the vendor-specific remote commands documentation in [remote command integrations](https://docs.tealium.com/platforms/remote-commands/integrations/).