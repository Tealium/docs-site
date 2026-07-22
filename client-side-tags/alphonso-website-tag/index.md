---
title: Alphonso Website Tag Setup Guide
description: This article describes how to set up the Alphonso Website Tag tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/alphonso-website-tag/
---## Tag tips

* The Use Default configuration options will cause the tag to act in the same manner as placing the snippet directly on your page.
* The Session ID, UTM Source, and UTM Medium populate automatically. To manage these options yourself, turn these options off.
* Add custom values by using the **+ Add Custom Destination** button.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Customer ID**
  * A value provided by Alphonso.
* **Use Default Session Management**
  * Use the Alphonso session management included with the code snippet.
  * If set to **no**, you will need to map Session ID.
* **Use Default UTM Parsing**
  * Use the Alphonso UTM parameter parsing included with the code snippet.
  * If set to **no**, you will need to map Campaign Source and Campaign Medium

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Description| Description|
|---| ---|
|`cust`|  <ul><li>Customer ID</li></ul> |
|`ord`|  <ul><li>Cache Buster</li></ul> |
|`utm_src`|  <ul><li>Campaign Source</li></ul> |
|`utm_mdm`|  <ul><li>Campaign Medium</li></ul> |
|`url`|  <ul><li>Page URL</li></ul> |
|`title`|  <ul><li>Page Title</li></ul> |
|`session_id`|  <ul><li>Session ID</li></ul> |
|`sess_status`|  <ul><li>Session Status</li></ul> |
|`ref`|  <ul><li>Referrer URL</li></ul> |
|`event_type`|  <ul><li>Event Name</li></ul> |
|`event_value`|  <ul><li>Event Value</li></ul> |
|`useDefaultSession`|  <ul><li>Use Default Session Management</li></ul> |
|`useDefaultUtm`|  <ul><li>Use Default UTM Parsing</li></ul> |
|`useOnBeforeUnload`|  <ul><li>Use OnBeforeUnload Pixel</li></ul> |
