---
title: FullStory Tag Setup Guide
description: This article describes how to set up the FullStory tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/fullstory-tag/
---## Tag tips

* In the Advanced Settings, set the Bundle Flag to **Yes** and the Wait Flag to **No** to make FullStory start recording as soon as possible.
* Use mapping to:
  * Send the User ID for identified users (`FS.identify`).
  * Send additional user parameters (`FS.identify` and `FS.setUserVars`).
  * Send an event with parameters (`FS.event`).
  * Override the Event Source (default is `tealium`).
  * Enable FullStory debugging.
  * Stop adding the FullStory Session ID to the data layer.
  * Stop sending the Tealium Session ID to the `FS.identify` and `FS.setUserVars` methods.
  * Stop sending the Tealium Visitor ID to the `FS.identify ` and `FS.setUserVars` methods.
* Events send when a value is present in the Event Name variable.
* If a Full Event Object is present, none of the Individual Custom Event parameters are sent.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Org ID**
  * Your FullStory Org ID
* **Namespace**
  * Your FullStory JavaScript namespace

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`fs_debug`|  <ul><li>String</li><li>Enable FullStory Debugging</li><li>Values are **true** or **false**.</li></ul> |
|`get_fs_session_id`|  <ul><li>String</li><li>Get FullStory Session ID</li><li>Values are **true** or **false**.</li></ul> |
|`get_tealium_session_id`|  <ul><li>String</li><li>Get Tealium Session ID</li><li>Values are **true** or **false**.</li></ul> |
|`get_tealium_visitor_id`|  <ul><li>String</li><li>Get Tealium Visitor ID</li><li>Values are **true** or **false**.</li></ul> |
|`fs_consent`|  <ul><li>String</li><li>User Tracking Consent</li><li>Values are **true** or **false**.</li></ul> |
|`fs_script`|  <ul><li>String</li><li>Script URL</li></ul> |

### User Parameters

|Variable| Description|
|---| ---|
|`uid`|  <ul><li>String</li><li>User ID</li></ul> |
|`uservars.displayName`|  <ul><li>String</li><li>User Display Name</li></ul> |
|`uservars.email`|  <ul><li>String</li><li>User Email</li></ul> |
|`uservars.custom`|  <ul><li>Custom User Var</li></ul> |

### Events

|Variable| Description|
|---| ---|
|`fs_event_name`|  <ul><li>String</li><li>Event Name</li></ul> |
|`fs_event_source`|  <ul><li>String</li><li>Event Source</li></ul> |
|`s_event.custom`|  <ul><li>Individual Custom Event Parameter</li></ul> |
|`fs_event_object`|  <ul><li>Object</li><li>Full Event Object</li></ul> |

### Page Events

|Variable| Description|
|---| ---|
|`fs_page.pageName`|  <ul><li>String</li><li>Page Name</li></ul> |
|`fs_page.category`|  <ul><li>String</li><li>Page Category</li></ul> |
|`fs_page.title`|  <ul><li>String</li><li>Page Title</li></ul> |
|`fs_page.url`|  <ul><li>String</li><li>Page URL</li></ul> |
|`fs_page.image_url`|  <ul><li>String</li><li>Page Image URL</li></ul> |
|`fs_page.custom`|  <ul><li>Individual Custom Page Parameter</li></ul> |
|`fs_page_object`|  <ul><li>Object</li><li>Full Page Object</li></ul> |
