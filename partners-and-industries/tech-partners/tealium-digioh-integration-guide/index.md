---
title: Tealium + Digioh Integration Guide
description: This article describes how to create a data source for Digioh to send form submission events to your Tealium account.
url: https://docs.tealium.com/partners-and-industries/tech-partners/tealium-digioh-integration-guide/
---
## Prerequisites

* [Digioh Account](https://digioh.com/login)
* Tealium EventStream API Hub or Tealium AudienceStream CDP account

## How it works

Digioh offers an integration that sends Digioh form submission data as events into your Tealium account. Integrations are assigned to one or more Boxes and can send additional metadata fields. In Digioh, you set the name of these events (sent as `tealium_event` ) and map Tealium attribute names to Digioh form field names.

In Tealium, you create an HTTP API data source and an event specification for the expected event.

## Tealium setup

There are two parts to setting up your account to receive events from Digioh: a data source an an event specification. Before you add the Tealium integration in Digioh, create an instance of the HTTP API data source in Tealium. This generates a data source key you use in the Digioh configuration.

### Data source

To add a data source for use with your Digioh integration, add an instance of the **HTTP API** data source. When you finish, copy the data source key generated for that data source to use in a static field mapping in your Digioh configuration.

Learn more about [connecting to a data source](https://docs.tealium.com/about-data-sources/).

### Event specification

Create an event specification to define the Digioh event name and its required and optional attributes. Use the event specification name in the **Event** parameter in your Digioh configuration.

For more information, see [About event specifications](https://docs.tealium.com/about-event-specifications/).

## Digioh setup

Follow these steps to add the Tealium integration to your Digioh account:

1. Log in to Digioh, go to **Integrations**, and click **New Integration**.
1. In the **Integration** list, under the CDP category, select **Tealium (Event)**.
1. Enter values for the following fields:
    * **Account** - your Tealium account name
    * **Profile** - your Tealium profile name
    * **Event** - the name of the event specification you created in Tealium (the value of `tealium_event`)

1. Click **Create Integration**

### Field Mapping

Next, create **Field Mappings** to select the fields to send in the event to Tealium.

To add the data source key as a field:

1. In **Field Name**, enter `tealium_datasource`.
1. For **Field Value**, select **Static** and enter the data source key you created in Tealium.
1. Click **Save Field Mapping**.

Digioh allows for additional form fields to include in the event. Use the **Map Fields** configuration to select Digioh fields and the matching Tealium attribute name. For example, you might map ` [PHONE]` to `customer_phone`.


<blockquote>
The Digioh field `[EMAIL]` is mapped to the Tealium attribute `email` automatically, but you can edit this mapping.
</blockquote>


Here is a list of standard fields:

* `[EMAIL]`
* `[NAME]`
* `[FIRST_NAME]`
* `[LAST_NAME]`
* `[FULL_NAME]`
* `[PHONE]`
* `[OPT_IN]`
* `[CUSTOM_1]`
* `[CUSTOM_2]`
* `[CUSTOM_3]`
* `[CUSTOM_4]`
* `[CUSTOM_5]...[CUSTOM_50]`

For a full list of Digioh fields that can be mapped, see [What are all the data and analytics fields Digioh can push through Integrations?](https://help.digioh.com/knowledgebase/what-are-all-the-fields-digioh-can-push/)

## Vendor documentation

* [Digioh: How to Integrate with Tealium](https://help.digioh.com/knowledgebase/how-to-integrate-with-tealium/)
* [Digioh Integration Basics](https://help.digioh.com/knowledgebase/digioh-integration-basics/)
* [Digioh: Mapping Data Fields](https://help.digioh.com/knowledgebase/what-are-all-the-fields-digioh-can-push/)
