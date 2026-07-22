---
title: InvocaJS Web Integration Tag Setup Guide
description: This article describes how to set up the InvocaJS Web Integration tag in your Tealium account.
url: https://docs.tealium.com/client-side-tags/invocajs-web-integration-tag/
---## Tag tips

* The Invoca Network ID and Tag ID are strictly numerical values.
* Use mapping to persist custom marketing data.
* After you map variables to the tag, add a corresponding Marketing data field in the Invoca user interface:
  * Contact your Invoca representative for help adding Marketing data fields.
  * Marketing data field names do not need to match the data mappings.
  * Data Source Type should be: **JavaScript Data Layer**
  * Data Source Name should be: `localStorage.getItem("inv_TEALIUM_MAPPING")`  

<blockquote>
`TEALIUM_MAPPING` must match the name of your custom data mapping.
</blockquote>


## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Invoca Network ID**
  * The Invoca Network ID is the unique ID assigned to your Invoca network (account).
* **Invoca Tag ID**
  * The Invoca Tag ID is the unique ID assigned to each tag you create within your Invoca Network.
* **Data center**: The data center region determines which Invoca content delivery network (CDN) serves the tag.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).
