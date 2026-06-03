---
title: Trace
description: Trace is the testing and validation tool for AudienceStream.
url: https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/trace/
---
Use Trace to validate that your configuration is working properly and that connector actions are being triggered.

## How it works

![](/images/server-side/getting-started-audiencestream-trace-icon.png)

Trace lets you isolate a specific test case and view a log of how it gets processed in AudienceStream. Trace generates a unique ID called a trace ID to use during your testing. When you trigger events using the trace ID, the results are displayed in a detailed log in the Trace tool, including information about: the received event, the enriched visitor attributes, the affected audience activity and the triggered connector actions.

Here&#39;s how it works:

* **Start a Trace**  
Starting a new trace generates a unique trace ID. You add this value to the data layer of your test application as the `tealium_trace_id` attribute or by copying it into the AudienceStream Trace Tealium Tool for testing directly from the browser.
* **Test Your Workflow**  
Once your trace ID is in place, you step through the work flow you want to test. This can be a multi-step flow that spans different screens or pages and Trace will capture all of them.
* **View Trace Log**  
Return to Trace and watch as the log of activity is processed in real-time. You can inspect the active visitor profile, the enriched attributes, and the outcome of triggered connector actions.

Click **Next** to see how to use Trace and validate that the connector is working.
