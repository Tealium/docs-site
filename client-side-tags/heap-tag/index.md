---
title: Heap Tag Setup Guide
description: This article describes how to configure the Heap Tag.
url: https://docs.tealium.com/client-side-tags/heap-tag/
---
## Tag Configuration

First, go to the tag marketplace and add the Heap Tag to your profile (See [Add a tag](https://docs.tealium.com/manage-tags/#add-a-tag)). After adding the Tag, configure the below settings:

  1. **Title**: (Required) The default is `Heap`. You may replace it with a custom name of choice.
  1. **Application ID**: (Required) Enter the Application ID provided by Heap.
  1. **String Delimiter**: This is the default seperator (semicolon) for passing an array as delimited strings. You may replace it with another delimiter of choice.


<blockquote>
Override, or dynamically populate, the **Application ID** and **String Delimiter** using [Data Mappings](https://docs.tealium.com/heap-tag/).
</blockquote>


### Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this Tag on your site.

Recommended Load Rule: The default **All Pages** Rule.

### Data Mappings

Mapping is the process of sending data from a [Data Layer Variable](https://docs.tealium.com/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor Tag. For instructions on how to map a variable to a tag destination, see [Mapping Variables](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The destination variables for the Heap Tag are built into its Data Mapping toolbox under the following categories:

#### Standard

In the following destinations, replace `custom` with your specific value.

|Destination Name| Description|
|---| ---|
|Application ID| The app id value provided by Heap|
|User ID| Unique visitor identifier assigned by Heap|
|Track Event Properties (`track.custom`)| Attach event properties to the event being tracked. Mapping to this destination triggers the `heap.track()` function ([learn more](https://heapanalytics.com/docs/custom-api#track)).|
|Add Event Properties (`addEventProperties.custom`)| Attach new event properties to the visitor's subsequent events ([learn more](https://heapanalytics.com/docs/custom-api#addeventproperties)). |
|Add User Properties (`addUserProperties.custom`)| Attach new properties to a visitor profile ([learn more](https://heapanalytics.com/docs/custom-api#adduserproperties))|
|String Delimiter| The delimiter character for separating array values. 
<blockquote>
Mapping to this destination overrides the default semicolon delimiter.
</blockquote>
|

#### Event Triggers

The Heap Tag automatically triggers any events that are defined in your Heap interface. But when you want to trigger events on the fly, without defining them in Heap first, you must map them in the **Event Triggers** category.

Triggering an event requires two things:

* event name
* trigger string (ideally a Data Layer value from the page where you want the event to trigger).

To map an event trigger,

1. Under **Data Mappings**, select your event variable from the **Variables** dropdown.
1. Click on **Select Destination** and go to the **Event Triggers** category.
1. In the **Value** field, enter the value of the variable being mapped. This becomes the trigger string.
1. In the **Trigger** field, specify a name for the event.
1. Click **Add**.

Repeat if you want to add more triggers.

#### How it works

As the tag loads on a page, it scans the Data Layer to see what value is populated in the mapped Variable. If it's equal to the supplied trigger string, the tag fires the event.


<blockquote>
The Ecommerce Extension does not automatically map any e-commerce Variables for this Tag.
</blockquote>


## Vendor Documentation

* [Heap Overview Documentation](https://heapanalytics.com/docs/installation)
* [Heap Custom API Documentation](https://heapanalytics.com/docs/custom-api)
