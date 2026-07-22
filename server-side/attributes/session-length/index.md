---
title: Session length
description: This article explains visit session length in AudienceStream.
url: https://docs.tealium.com/server-side/attributes/session-length/
---
## How it works

Session length determines when AudienceStream ends a visit. When a visit reaches the session length without a new event, the visit ends and AudienceStream performs end-of-visit processing. The next event from the visitor starts a new visit. AudienceStream has a maximum visit length of 24 hours, regardless of event activity.

## Session lengths

In AudienceStream, the default session length is set based on the platform that sends the events:

* **Web**: 30 minutes for multiple events, 10 minutes for a single event without a follow-up event.
* **Mobile App**: 2 minutes.
* **Omnichannel**: 1 minute.
* **File Import**: 1 minute.
* **Collect API**: 30 minutes.
* **All Others**: 30 minutes.

The platform is based on the reserved attribute named `platform` according to the following values:

* **Mobile**: `platform` is set to one of the following: `android`,`ios`,`win`,`bb10`, or `native_mobile`.
* **Web**: `platform` is set to `web` or not set.

## Customize session length

To customize the session length, set the data layer variable `_dc_ttl_` to a value in milliseconds on the first event of a session. The minimum value of `_dc_ttl_` is `5000` (5 seconds) and the maximum value of is `1800000` (30 minutes). For example, to set the session length to five minutes, add the following to the event: `"_dc_ttl_": 300000`. The session length cannot be changed after it has been set.


<blockquote>
To set a custom session length, do not set the `platform` variable. If you set a custom value for `platform`, the session length defaults to 30 minutes.
</blockquote>
