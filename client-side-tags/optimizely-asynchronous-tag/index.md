---
title: Optimizely Asynchronous Tag Setup Guide
description: Tealium's best practice is to load all tags Asynchronously. This post will outline how to follow the Tealium best practices when implementing Optimizely.
url: https://docs.tealium.com/client-side-tags/optimizely-asynchronous-tag/
--- For options to implement Optimizely synchronously see this [POST](). 

There are two methods of implementing the Optimizely Asynchronous tag. The content of your site and your testing requirements will determine which approach to use. We recommend that you try the two methods in the order they appear in this post.

**NOTE:** Both methods assume the `utag.js` file is coded asynchronously on the page.

## Method 1 (RECOMMENDED): Bundle Optimizely Async Tag and load on all pages

We recommend this method because the tag will not block anything else from loading in the page.

### Step 1: Enable the Bundling feature for Tags that will load on all pages.

1. In the admin menu, click **Configure Publish Settings**. The **Publish Configuration** dialog appears.
1. Turn **ON** the **Bundle Tags Loading On All Pages** toggle. This will bundle the Tag with `utag.js`, thus reducing the number of network calls made by the browser.

### STEP 2: Add and set up the Optimizely Async Tag

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

Here are the steps to set it up:

1. Enter your Project ID. This is the number at the end of the script tag Optimizely sends you.  
 For example:  `&lt;script src=&#34;//cdn.optimizely.com/js/123456789.js&#34;&gt;&lt;/script&gt;`
1. Select **Wait Flag = No** from the **Advanced Settings** list.  
1. Proceed to the **Load Rules** tab and check the default **Load on All Pages** rule.  
1. Proceed to the **Data Mappings** tab and map the destinations you want to send data to. To learn more, see [Data Mappings]() to learn how to map a data source to a Tag destination.  

 If you plan to track E-Commerce data with the Async Tag, we recommend that you use the [E-Commerce Extension]() to automatically map that data. 

| Destination Name | Destination Variable | Description                                                   | E-Commerce Extension Mapping (RECOMMENDED)     |
|:-----------------|:---------------------|:--------------------------------------------------------------|:-----------------------------------------------|
| Project ID       | `projectId`          | Project identifier provided by Optimizely                     | N/A                                            |
| Order ID         | `orderId`            | Unique identifier assigned to the order                       | `_corder` variable maps to this destination    |
| Revenue in Cents | `revenue`            | Subtotal amount (in cents) of the order                       | `_csubtotal` variable maps to this destination |
| Event Name       | `eventName`          | Name/Type of conversion event&lt;br&gt; Default event is `purchase` | N/A                                            |

### STEP 3: Save/Publish your profile.

**IMPORTANT**: For the Async Tag to fire as soon as possible, make sure the `utag.js` file is coded as high in the page as possible. We recommend placing the utag.js at the top of the HTML &amp;lt;body&amp;gt; tag. Tealium will load the Optimizely JavaScript file and take care of the rest.

## Method 2: Run Optimizely as blocking Tag

Optimizely typically prefers to be synchronous on the page so it can run &#34;sooner&#34; and determine the test before other stuff (like your Analytics tool) runs. However, the only way to have Optimizely run soon enough and still be asynchronous is by serving its `.js` library from an alternate location. In doing so, the Optimizely Async Tag becomes a blocking Tag and any subsequent asynchronous scripts (for example, `utag.10.js`) will not load until the [blocking Tag]() is complete.

 Make sure to upgrade the `utag.js` version if you are not already using the latest. For more information, see [utag.js Release Notes](/release-notes/?filter=tealium-universal-tag). 

1. Repeat step #2 above to add and set up the Optimizely Async Tag.
1. Drop down the **Advanced Settings** and enter the location of the `.js` library in the **Custom Script Source** field.
1. **Save/Publish** your profile.

That&#39;s it! A few simple differences, but this will dramatically change the way the Optimizely file is loaded and how other tags are loaded after Optimizely.
