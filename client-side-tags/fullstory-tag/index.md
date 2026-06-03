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

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Org ID**
  * Your FullStory Org ID
* **Namespace**
  * Your FullStory JavaScript namespace

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`fs_debug`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Enable FullStory Debugging&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`get_fs_session_id`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Get FullStory Session ID&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`get_tealium_session_id`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Get Tealium Session ID&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`get_tealium_visitor_id`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Get Tealium Visitor ID&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`fs_consent`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User Tracking Consent&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`fs_script`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Script URL&lt;/li&gt;&lt;/ul&gt; |

### User Parameters

|Variable| Description|
|---| ---|
|`uid`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User ID&lt;/li&gt;&lt;/ul&gt; |
|`uservars.displayName`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User Display Name&lt;/li&gt;&lt;/ul&gt; |
|`uservars.email`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;User Email&lt;/li&gt;&lt;/ul&gt; |
|`uservars.custom`|  &lt;ul&gt;&lt;li&gt;Custom User Var&lt;/li&gt;&lt;/ul&gt; |

### Events

|Variable| Description|
|---| ---|
|`fs_event_name`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Event Name&lt;/li&gt;&lt;/ul&gt; |
|`fs_event_source`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Event Source&lt;/li&gt;&lt;/ul&gt; |
|`s_event.custom`|  &lt;ul&gt;&lt;li&gt;Individual Custom Event Parameter&lt;/li&gt;&lt;/ul&gt; |
|`fs_event_object`|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;Full Event Object&lt;/li&gt;&lt;/ul&gt; |

### Page Events

|Variable| Description|
|---| ---|
|`fs_page.pageName`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Page Name&lt;/li&gt;&lt;/ul&gt; |
|`fs_page.category`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Page Category&lt;/li&gt;&lt;/ul&gt; |
|`fs_page.title`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Page Title&lt;/li&gt;&lt;/ul&gt; |
|`fs_page.url`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Page URL&lt;/li&gt;&lt;/ul&gt; |
|`fs_page.image_url`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Page Image URL&lt;/li&gt;&lt;/ul&gt; |
|`fs_page.custom`|  &lt;ul&gt;&lt;li&gt;Individual Custom Page Parameter&lt;/li&gt;&lt;/ul&gt; |
|`fs_page_object`|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;Full Page Object&lt;/li&gt;&lt;/ul&gt; |
