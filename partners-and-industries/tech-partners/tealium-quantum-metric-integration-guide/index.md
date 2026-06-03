---
title: Tealium + Quantum Metric Integration Guide
description: This article describes how to get the most out of Tealium and Quantum Metric by setting up the Quantum Metric tag in Tealium iQ Tag Management and enabling the Quantum Metric Tag to send Session Replay URLs to Tealium AudienceStream.
url: https://docs.tealium.com/partners-and-industries/tech-partners/tealium-quantum-metric-integration-guide/
---The bi-directional integration between Tealium and Quantum Metric gives you deeper insights into how your key customer segments experience your digital products.

 When using this tag with `utag` version 4.50 or later, you must set the `utag.js` [`always_set_v_id` setting]() to `true`. This setting ensures that the visitor ID is available for cookie synchronization. For more information, see the [utag 4.50 release notes]() and [Considerations for tealium_visitor_id when upgrading to utag 4.50&#43;](https://support.tealiumiq.com/en/support/solutions/articles/36000535887-considerations-for-tealium-visitor-id-when-upgrading-to-utag-4-50-).

## Prerequisites

* **Tealium**
    * iQ Tag Management (Required)
    * AudienceStream (Recommended)  
To achieve the most value out of the bi-directional integration.
* **Quantum Metric**
    * Platform for Native or Web (Required)

## How it works

Quantum Metric is the Digital Experience Intelligence platform, driving unparalleled visibility into every customer interaction across all devices and delivering faster data-driven decisions. Built to automatically prioritize both technical and behavioral insights, the platform promotes enterprise digital transformation by empowering organizational Customer Experience (CX) alignment. Performance and security are the foundation of Quantum Metric, enabling customers to gain real-time user insights securely and at scale.

See the [Tealium and Quantum Metric Partnership Overview](https://tealium.com/technology-partner/quantum-metric/) for more information.

## Tag configuration

Before you enable Tealium AudienceStream to receive Quantum Metric Replay URLs, you must first add and configure the Quantum Metric tag.

For more information, see [Quantum Metric tag]().  

### Enable AudienceStream

Before enabling Quantum Metric Replay URLs to be sent to AudienceStream, consult with your Quantum Metric Client Service Manager to determine the target behaviors and experiences you want to send from Quantum Metric to Tealium.

Enable AudienceStream to receive data from Quantum Metric:

1. Go to your Quantum Metric tag in iQ Tag Management.
1. Expand the details and click **Edit**.
1. Set the Send Replay URL field to **True**.  
      ![](/images/tech-partners/quantum-metric-tag-configuration.jpg)
1. Define the following fields:
      * Time Stamp
      * Tealium Account
      * Tealium Profile
1. Click **Apply**.
1. Save and publish your changes to the environments you want.

### View in Live Events

After the Quantum Metric tag is configured and sending Replay URLs to AudienceStream is enabled, you can view activity in the Live Events feed.

Use the following steps to view in Live Events:

1. In the Customer Data Hub left sidebar, click **Event Stream &amp;gt; Live Events**.
1. Scroll down to find the events from Quantum Metric by filtering for events containing the event attribute `quantum_metric_replay_url` or `quantum_metric_user_id`.  
    ![](/images/tech-partners/quantummetric-live-events.png)
1. Use these event attributes to enrich the profile with other [AudienceStream attributes]().
