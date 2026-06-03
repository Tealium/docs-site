---
title: CMP Plugins
description: Learn how to integrate your Consent Management Platform (CMP) with Tealium iQ Tag Management to enforce privacy settings for managed tags.
url: https://docs.tealium.com/partners-and-industries/partner-with-us/cmp-plugins/
---


CMP plugins are vendor-specific solutions in the Tealium extension marketplace that make it easy to integrate a CMP installation with a Tealium iQ installation. 

A CMP plugin offers the following benefits:

- A simple import tool to reduce the time to integrate the two solutions.
- Robust enforcement of firing tags based on consent status from the CMP.
- Server-side distribution of consent data from the CMP.

## How it Works

A CMP plugin creates a mapping between the data processing services configured in the CMP and the tags configured in Tealium iQ. The plugin provides a helper tool, usually a bookmarklet, that makes it easy to import the CMP settings into Tealium iQ and map each service name to one or more tags.

Once the mappings are set up and deployed to your site, your managed tags will fire based on the user&#39;s interaction with the CMP.

A CMP integration has the following parts:

* **Service Mapping**   
A service mapping associates CMP service names with managed tags. The linked tags will only fire after the associated CMP service name is consented to.
* **Data Layer Integration**  
Consent status variables from the CMP are added to the [data layer object](/platforms/javascript/data-layer-object/) of each tracking call. The variable names are in the format `&lt;cmp name&gt;_&lt;variable name&gt;`. For example, an array of consented service names from Usercentrics would be `usercentrics_services_with_consent`.
    * `&lt;cmp name&gt;_services_with_consent` - an array of consented service names.
    * `&lt;cmp name&gt;_consent_type` - `explicit` or `implicit` consent type.


## Requirements

To integrate with Tealium iQ Tag Management, the following consent status information must be available for each data processing service configured in the CMP. These are usually accessed as global JavaScript variables or methods in the page:

* **Service Name** - A unique name for the service that consent was applied to.
* **Consent Status** - The status of the consent for the service, where `true` indicates that consent has been granted and `false` indicates that consent has not been granted.
* **Consent Method Type** - The method by which consent was obtained (`implicit` or `explicit`).


## Sending Consent Data to Tealium

In addition to collecting and enforcing consent on the client-side, a CMP integration can also distribute consent status to other vendors using server-side connectors.

If your CMP supports webhook callbacks, then you can extend your integration with Tealium by sending updates to the [HTTP API endpoint](/platforms/http-api/endpoint/). These events will be processed server-side and can be activated across other vendors using Tealium EventStream, AudienceStream, and DataAccess.

If your CMP does not support webhooks, contact Tealium to work with your product and engineering teams to formalize an integration.

## Become a Partner

[Contact us](https://tealium.com/tealium-partner-network/) to integrate your technology.