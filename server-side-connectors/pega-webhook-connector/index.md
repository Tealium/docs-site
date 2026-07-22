---
title: Pega Webhook Connector Setup Guide
description: This article describes how to configure an advanced webhook to send custom request actions using template variables for Pega API.
url: https://docs.tealium.com/server-side-connectors/pega-webhook-connector/
---
## Prerequisites

* Set up [Pega Customer Decision Hub](https://docs.pega.com/pega-customer-decision-hub-implementation-guide/87/pega-customer-decision-hub-implementation-guide)
* Tealium EventStream API Hub or Tealium AudienceStream CDP

## How it works

The Pega outgoing webhook enables integrations with Pega's Customer Decision Hub, Next-Best-Actions designer, and Customer Profile designer. Using Tealium and Pega together can help you comply with security regulations, leverage real-time data collection to be more responsive, and identify and target individual customers with Next-Best-experience messages. Integrating with Pega allows Tealium data to trigger custom customer interactions, such as a newsletter promotion or promotional code offering through Pega, helping personalize the customer’s journey. To get started, submit an HTTP request to send first-party personalized data to Pega.

## Vendor Requirements

### Request URL

You can create a custom request URL in Pega using Pega's Designer Studio. Your request URL is based on your specific Pega implementation and the service packages in your Pega account. When you create your request URL, you will need to include specific path parameters. To set up your REST service, including specifying the variables and path parameters for your custom URL, see [Creating a Service REST rule](https://docs.pega.com/data-management-and-integration/87/creating-service-rest-rule) in the Pega documentation. After creating your Service REST rule, complete your REST rule configuration by [configuring the resources and processing details](https://docs.pega.com/data-management-and-integration/87/defining-resource-and-processing-details-service-rest-rule) for your rule.


<blockquote>
For more information about all of Pega's APIs, API best practices, and information about creating REST integrations, see [Pega APIs and services](https://docs.pega.com/data-management-and-integration/84/pega-apis-and-services) in the Pega documentation.
</blockquote>


### Method Field

For more information about available methods to use in your service REST rule, see [Service REST methods](https://docs.pega.com/data-management-and-integration/87/service-rest-methods) in the Pega documentation.

## Webhook Example

The request body is a JSON message with a customizable body template. Pega accepts either nested or flat JSON. The structure of the JSON request will depend on your Pega implementation and data points specified in the Designer Studio.

For more information about configuring a webhook connector, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).

In this example, the webhook sends a `PageView` request with parameters to identify the user.

* **Method**: `POST`
* **URL**: `https://<host>:<port>/prweb/PRRestService/<servicepackage>/<serviceclass>/<servicemethod>`
* **Body Content Type**: `application/json`
* **Body Data**: ``Map `{{data}}` To Body``
* **Template Variables:**
  * `Map "PageView" To Intent`
  * `Map customer_id to ID`
  * `Map tealium_firstparty_visitor_id To Cookieidvalue`
  * `Map Last event timestamp To time`

* **Templates**:
  * Name: `data`
  * Template:  
```json
{
  "Cookieidvalue": "{{Cookieidvalue}}",
  "ID": "{{ID}}",
  "Intent": "{{Intent}}",
  "Lastviewedproduct": "{{time}}"
}
```