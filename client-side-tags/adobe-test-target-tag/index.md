---
title: Adobe Test & Target Tag Setup Guide
description: Adobe Test & Target gives marketers the necessary capabilities to continually make their online content and offers more relevant to their customers -- yielding greater conversion.
url: https://docs.tealium.com/client-side-tags/adobe-test-target-tag/
---
## Tag Specifications

**Name**: Test &amp; Target

**Vendor**: Adobe

**Type**: Personalization

## Requirements

**Services**: Adobe Marketing Cloud Account

**Configurations**:

* Client Code
* Timeout
* Global mbox Name (synchronous version)

## Tag Configuration in Tealium iQ Tag Management

### Step 1. Add the Tag

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

Tealium supports both asynchronous and synchronous versions of the Test &amp; Target Tag. Each version is a separate tag in the tag marketplace. However, we recommend that you use the asynchronous version. If you have concerns about flicker, check out our [Flicker-Free Test &amp; Target]() solution, which allows you load the Test &amp; Target Tag asynchronously and avoid the appearance of flicker.

You must add and configure the [Test &amp; Target Content Modification extension]() along with the asynchronous tag. The synchronous version does not use the extension.

### Step 2. Configure the Tag

#### Asynchronous

As a best practice we recommend using the asynchronous version of Test &amp; Target. There are a few differences in the configurations, depending on which version you use. For the asynchronous version, set the following configurations:

![](/images/client-side-tags/basic-configuration-1.png)

1. **Title**: (Required) Enter a descriptive title to identify the tag instance.
1. **Client Code**: (Required) Enter the client ID assigned to you by Adobe.
1. **Timeout**: (Required) Enter the amount of time, in milliseconds, you want the tag to wait for a response from Adobe before assuming the Test &amp; Target server is not responding. If there is no response from the server, the tag call is halted. We recommend setting this to 5000 milliseconds or greater.
1. **Visitor Tracking ID**: (Optional) This field lets you track visitors across Test and Target and SiteCatalyst. You can find this configuration in the `mbox.js` file as `var imsOrgId = &#39;XXXXXXXXXXXXXXXXXXXXXXXX@AdobeOrg&#39;`

You&#39;ve finished configuring the Test &amp; Target Tag.

#### Synchronous

The synchronous version of Test &amp; Target has a slight difference in configurations and requires a change to the **Advanced Settings** of the tag. If you plan to load this tag synchronously, then you must load the `utag.js` file synchronously as well. For information about how to acquire the synchronous `utag.js` code, see [How utag.sync.js works]().

![](/images/client-side-tags/basic-configuration-2.png)

1. **Title**: (Required) Enter a descriptive title to identify the tag instance.
1. **Client Code**: (Required) Enter the client ID assigned to you by Adobe.
1. **Global mbox Name**: (Required) Enter the name of the globally hidden mbox. Adobe typically uses `global` here. The tag automatically calls `mboxCreate` to create the mbox.
1. **Visitor Tracking ID**: (Optional) This field lets you track visitors across Test and Target and SiteCatalyst. You can find this configuration in the `mbox.js` file as `var imsOrgId = &#39;XXXXXXXXXXXXXXXXXXXXXXXX@AdobeOrg&#39;`
1. **Advanced Settings**: (Required) Change the following Advanced Settings:
  * Set **Wait Flag** to `No`.
  * Set **Synchronous Load** to `Yes`.
![](/images/client-side-tags/basic-configuration-3.png)

Any further configuration of the test content is handled through Test &amp; Target&#39;s user interface.

### Step 3. Apply Load Rules

[Load Rules]() determine when and where to load an instance of this tag. The **Load on All Pages** rule is the default Load Rule. To load this tag on a specific page, create a new load rule with the relevant conditions.

**Best Practice**: We recommend that you load this tag on all pages by leaving the default **Load on All Pages** selected. For the asynchronous version, you can control the conditions under which your tests load through the Test &amp; Target Extension.

### Step 4. Set up Mappings

[Mapping]() is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor tag.

* For the asynchronous version of Test &amp; Target, mappings are handled through the Test &amp; Target Content Modification extension in the **Static Params** field.
* Mapping is not supported for the synchronous version of Test &amp; Target.