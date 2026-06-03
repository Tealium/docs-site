---
title: Batched actions
description: This article describes how batched actions work with Tealium connectors.
url: https://docs.tealium.com/server-side/connectors/batched-actions/
---
Many connectors support batch-based actions. When using batched actions, the system accumulates connector requests into a batch and then calls the vendor once for the entire batch. Using batched actions reduces the load on the vendor system and helps you remain within vendor API rate limits.

 Batching is ignored when using [Trace]().

Connectors that support batching contain batch-based parameter logic. Requests are queued until one of the following three thresholds is met:

* Number of requests
* Time since oldest request 
* Size of requests

When the maximum threshold value is reached, the connector sends the batch. These thresholds operate on an OR basis, meaning that any one of them will trigger a batch send.

When you publish a profile, the connector batch queues are processed regardless of whether the batch limits have been reached.

## Batch components

The above threshold values are not the only factors that affect how requests are batched to the vendor. Tealium components operate in parallel for scale with more than one component forming its own batch at the same time.

For this example, consider a connector action that is batched with the following thresholds (values for example purposes only):

* Maximum requests = 100
* Maximum time = 1 minute
* Maximum Size = 10 MB

### Single component

In this example, the Tealium connector has a single batching component. It receives a constant flow of incoming data at 150 requests per minute and the size of 150 requests is less than 10MB.

In this case, the **Maximum requests** parameter would be triggered regularly to send the batched data, because threshold is reached before either of the other two parameters are triggered.

![](/images/server-side/single-component-batching.png)

### Multiple components

In reality, Tealium connectors have multiple batching components. In this example, there are two batching components with the same incoming flow of data (150 requests per minute). The requests are equally distributed between the two components. Because each component monitors its batch independently, the flow of data into each component is now only 75 requests per minute. This data flow is not high enough to trigger the **Maximum requests** threshold. In this case, the data flow would first trigger the **Maximum time** threshold instead. We still see regular calls to the vendor API, but with each containing only 75 records.

![](/images/server-side/multiple-component-batching.png)

In real-world scenarios, there are more than one or two components in a Tealium connector. Tealium scales the number of batching components up and down to meet demand.

### Event order

Due to parallel data flows, events may not be triggered to downstream connectors in the same order as they were received. For example, if a visitor received event A and then event B, it is possible that event B could be sent to the vendor in the first batch of data and event A could be sent later an a separate batch. If the order of events is important to your use case, pass along a sequence number or event timestamp in the connector payload and reconstruct the original order in the vendor system.
