---
title: Tag basics
description: Learn the basics of the tag in iQ Tag Management.
url: https://docs.tealium.com/iq-tag-management/getting-started/tag-basics/
---A tag loaded through Tealium runs identically to that same tag hard-code in your pages. A tag has the following components:

![](/images/iq-tag-management/getting-started-tags.jpg)

*   **Tag configuration**  
The settings for the tag, such as account ID.
*   **Load rule**  
The condition that determines when to load the tag on your site.
*   **Data mappings**  
The configuration that sends data to the tag using values from the data layer.

## How It Works

Before you add your first tag, let&#39;s review how it works:

* **No coding necessary**  
Setting up a tag does not require any coding. A tag in TiQ offers a user-friendly interface to configure and deploy a vendor&#39;s tag to your site. 
* **Deploy tags directly**  
Once the Tealium Universal Tag (`utag.js`) is added to your site, tags added in your account are loaded directly to your site by _publishing_ your changes.
* **Multi-functional tags**  
A single instance of a vendor tag typically provides all of the tagging functionality required by that vendor for your entire site. While the vendor might require different tag code for different types of pages (for example, Product Detail Page, Shopping Cart Page, and Order Confirmation Page), these are all provided in one instance of the tag in Tealium iQ.
