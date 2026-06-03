---
title: About Trace
description: Trace is a testing and inspection tool for your server-side configuration that tracks your workflow to show how events and customer data are processed in real-time.
url: https://docs.tealium.com/server-side/trace/about/
---
## Required

The following items are required to use trace:

* Tealium EventStream or AudienceStream  
* [Tealium Tools Browser Extension](https://chrome.google.com/webstore/detail/tealium-tools/gidnphnamcemailggkemcgclnjeeokaa)  

Do not add trace IDs to bulk events.&lt;br&gt;Do not add trace IDs as a permanent parameter to monitor production data.

## How it works

Trace provides an inside view into the inner workings of EventStream and AudienceStream. The trace tool is critical for testing your configuration. Use trace to observe the details of a  workflow, ensure that attributes update correctly, rules are correctly applied, and that actions trigger as expected.

The trace interface supports the following actions:

* Start or stop a trace
* Join an active trace
* View predefined workflows and event log details in real time
* Establish rules and view results
* Get replay code to replay, pause, or resume an event
* View a scrolling summary of actions, events, and audiences
* View the details of an event or processing step
* View snapshots of visitor profiles

Invalid trace IDs are removed from the event data.

## Limits

* **Time limit**: A trace times out and is removed after 12 hours, regardless of activity.
* **Event limit**: A trace supports up to 250 events. If the limit is reached, the trace stops accepting new events.
* **Functions**: When testing functions with trace, function calls are limited to 15 per minute.
