---
title: Event logging
description: Learn how event logging works for client-side consent management.
url: https://docs.tealium.com/consent/client-side/consent-management/event-logging/
---

## Requirements

* Tealium EventStream or [Tealium DataAccess]() (EventStore or EventDB)

## How it works

The event logging feature logs every consent action taken by your visitors and works with all the [client-side consent management]() offerings. When client-side consent management is deployed to your site and event logging is enabled, consent actions are sent as an HTTP request to Tealium&#39;s server-side CDH, where they can be logged with EventStore or EventDB or streamed with EventStream as needed for auditing and record-keeping purposes.

The following consent actions are logged:

* Grant or revoke consent
* Changes to consent preferences
* Changes to the **Do Not Sell** option

For customers with access to the relevant products, these events can be stored in EventDB and EventStore or streamed with EventStream (consent-based blocking does not apply to these specific events).

For customers who prefer to use their own data collection endpoint, a custom URL can be specified.

## Event logging settings

The following settings are available:

* **Log Consent Changes** - set to **Yes** to enable event logging (applies to all consent management offerings).
* **Event Log URL** - the event collection endpoint used to log consent changes. Only edit this setting if you have your own data collection endpoint.  
Default:
    ```bash
    https://collect.tealiumiq.com/event
    ```

* **Event Log Profile** - the profile to which logged events should be sent. The value set here is passed to the event log URL as the parameter `tealium_profile=&#34;PROFILE&#34;`.

To customize the [consent event]() payloads, edit these two templates `fullConsentEventHandler` and `partialConsentEventHandler`. For more information about updating templates, see [Managing Templates]().
