---
title: Trace
description: Trace is the testing and validation tool for EventStream. Use Trace to validate that your configuration is working properly and that connector actions are triggered.
url: https://docs.tealium.com/server-side/getting-started/eventstream-api-hub/trace/
---
## How it works

Use Trace to isolate a specific test case and view a log of how it gets processed in EventStream. Trace generates a unique ID called a trace ID to use during your testing.

When you send events using the trace ID, the results are displayed in a detailed log in the Trace tool, including the following information:

* events received
* attributes enriched
* event specifications validated
* event feeds matched
* connector actions triggered

Here&#39;s how it works:

* **Start a trace**  
Starting a new trace generates a unique trace ID. You add this value to the data layer of your test application as the `tealium_trace_id` attribute or by copying it into the Tealium Tools Trace tool for testing directly from the browser.
* **Test your workflow**  
Once your trace ID is in place, step through the workflow you want to test. This can be a multi-step flow across different screens or pages.
* **View trace log**  
Return to Trace and watch a log as EventStream processes activity in real-time. You can inspect the events, the enriched attributes, and the outcome of triggered connector actions.

The next tutorial demonstrates how to use Trace to validate that the connector is working.