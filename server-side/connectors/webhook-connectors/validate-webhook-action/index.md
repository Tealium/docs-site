---
title: Validate webhook action
description: This article describes how to validate webhook actions.
url: https://docs.tealium.com/server-side/connectors/webhook-connectors/validate-webhook-action/
---
Use one of the following methods to verify and troubleshoot the new actions:

* **Vendor User Interface**  
If the vendor provides a web user interface that lets you monitor changes, submit an action to the target vendor endpoint and verify it on the target endpoint.
* **PutsReq Bucket**  
Send a test request to a sample PutsReq bucket URL. After configuring the Action fields, go to the following URL to examine the request received using the PutsReq user interface.  
`https://putsreq.com/&gt;YOURBUCKETNAME/inspect`
* **Trace**  
[Run the Trace tool]() and examine the action data. If you are using the template feature of this action, check the Template Variables JSON and Rendered Template: &amp;lt;template name&amp;gt;.  
When individual data items are added to a batch, trace displays batched actions first and then again after the batch is sent to the third party.  
Individual data items added to a batch are not batched in Trace.
 Multiple batching actions often correspond to a singe send-off action. There may be a considerable delay between the two

## Sample Action Configuration

1. Go to [https://putsreq.com/](http://putsreq.com/) and click **Create a PutsReq** to create an endpoint for testing.
      ![](/images/server-side/putsreq-yourputsrequrl.jpg)
1. Copy the **PutsReq URL**.
1. Go to the Actions settings for your Webhook connector.
1. Scroll down to Method and click to expand.
1. Select **POST** from the drop-down list.
1. Scroll down to URL, click to expand, and paste the **PutsReq URL** into the URL parameter field.  
      ![](/images/server-side/putsreq-webhookconnectorsettings-method-and-url.jpg)
1. Click **Save**.
1. Save and Publish your changes.
1. [Run a Trace]() to verify that the action triggered as expected.