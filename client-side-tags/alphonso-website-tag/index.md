---
title: Alphonso Website Tag Setup Guide
description: This article describes how to set up the Alphonso Website Tag tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/alphonso-website-tag/
---## Tag tips

* The Use Default configuration options will cause the tag to act in the same manner as placing the snippet directly on your page.
* The Session ID, UTM Source, and UTM Medium populate automatically. To manage these options yourself, turn these options off.
* Add custom values by using the **+ Add Custom Destination** button.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

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

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

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
