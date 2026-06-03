---
title: Trace: Test with Trace
description: In this step, use Trace to validate that your configuration is working as expected.
url: https://docs.tealium.com/server-side/getting-started/eventstream-api-hub/test-trace/
---
## Requirements

If you are testing a web page with Trace, you need the following:

* [Tealium Tools browser extension]()

## Start a trace

Follow these steps to perform a test with Trace:

1. In the sidebar, select **Trace**.
1. Under **New Trace**, click **Start**. A dialog with a trace ID will appear.
1. Copy the trace ID and click **Continue**.
1. Activate the trace ID using one of the following methods:
    * **Tealium Tools**
      * Open a new browser window to your test page.
      * Click the Tealium Tools browser extension and click **AudienceStream Trace**. 
      * Enter the trace ID from step 2 and click **Start Trace**.   
      ![](/images/server-side/es-getting-started-trace-tealium-tool.jpg)
    * **Data layer attribute**
      * Add `tealium_trace_id` to the data layer of your code installation and set it to the value of the trace ID.
      * In the HTTP API, this means adding a query string parameter: `&amp;tealium_trace_id=012345`
      * In a Swift app, for example, it will look like this:  
      `tealium?.volatileData()?.add(data: [&#34;tealium_trace_id&#34;: &#34;012345&#34;])`

1. Proceed with your test case work flow. This might require refreshing the page, navigating through some pages, making a purchase, or viewing some screens in a native app.
1. Return to the **Trace** interface to inspect the log details.

## Trace Log

The Trace log updates automatically as it processes the traced event. It displays the event data details, the matched spec, any matched feeds, and any triggered connector actions. If there were any errors, those are provided as well with additional details of the issue.

The Trace image below reflects the validation of the previously configured components using the **Search with No Results** example.

![](/images/server-side/getting-started-eventstream-trace.png)

In this case:

![](/images/server-side/beast-thumbsup-whistle-small.png)

* ✓ The event spec for `search` is valid.
* ✓ The event feed matched.
* ✓ The Google Sheets connector triggered.

If you didn&#39;t see the expected trace log, check the following items:

* Did you use the correct trace ID in your test?
* Did you save and publish your account after adding the event spec, event feed, and connector action?
* Did you set `tealium_event` correctly?
* Does the value of `tealium_event` match the name of the spec?
* Does your test event match the conditions of the event feed?

You&#39;ve made it to the end of this simple getting started guide. The next step will quickly cover the save and publish process, followed by some helpful links for additional reading.