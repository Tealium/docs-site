---
title: About templates
description: This document introduces basic concepts about iQ Tag Management templates.
url: https://docs.tealium.com/iq-tag-management/templates/about/
---
## How it works

Templates are JavaScript code that provide the core logic for a feature, tag, or functional component of iQ Tag Management. Templates are used to assemble your configuration from Tealium iQ into the JavaScript files that run on your site or app. For a list of templates by component, see [Template Types](#template-types).

Users can run the [Template Status Checker](https://docs.tealium.com/template-status-checker/) to ensure that their templates are up-to-date. Advanced users will find directly editing templates useful for the following cases:

* Adding [Custom Container tags](https://docs.tealium.com/tealium-custom-container-tag/) or [custom consent integrations](https://docs.tealium.com/custom-cmp-integrations/) to build their own functionality for an unsupported vendor or self-built solution.
* Temporarily fixing a bug in a tag until an official fix is released.
* Changing the core logic of any templated component to meet their specific needs.


<blockquote>
Some customizations and fixes can be made by using extensions rather than editing templates. Consider using extensions first because they are easier to maintain over time.
</blockquote>


For more information on editing and updating templates, see [Manage Templates](https://docs.tealium.com/manage-templates/).

## Template types

Templates are used for system tags, vendor tags, and the consent manager. When you view a list of templates, each type can be identified by the following names:

### System tags

* **uTag Loader** (`utag.js`)  
The template for the Universal Tag. The Universal Tag is the JavaScript code that contains all of the generated code necessary to load third-party tags onto your site. For more information, see [JavaScript (`utag.js`) install](https://docs.tealium.com/platforms/javascript/install/#universal-tag-utagjs).
* **uTag Sync** (`utag.sync.js`)  
This file allows your pages to support A/B and multivariate testing tags, such as Adobe Target or Optimizely. Place the script in the `<head>` section of your page code and it loads synchronously to comply with the most common vendor requirements. For more information, see [How `utag.sync.js` works](https://docs.tealium.com/utag-sync/).
* **Mobile webview** (`mobile.html`)  
The template for mobile installations, which is loaded as a hidden webview for your mobile app to load vendor tags. For more information, see [Client-side](https://docs.tealium.com/platforms/getting-started-mobile/client-side/#mobile).

### Consent management

These templates are used in the consent management features. For more information, see [About consent management](https://docs.tealium.com/about-consent-management/).

* Dom Ready (`cmDomready`)
* General (`cmGeneral`)
* Show Explicit (`cmShowexplicit`)
* Show Preferences (`cmShowpreferences`)
* Do Not Sell Banner (`cmShowDNSBanner`)
* Do Not Sell Preferences (`cmDoNotSell`)
* Do Not Sell Prompt (`cmShowDNSPrompt`)
* Consent Logging - Accept/Decline Consent (`fullConsentEventHandler`)
* Consent Logging - Grant Partial Consent (`partialConsentEventHandler`)

### Consent integrations

These templates are used in the consent integrations. For more information, see [About consent integrations](https://docs.tealium.com/about-consent-integrations/).

* Framework (`utcm_framework`): The consent enforcement framework for Tealium iQ.
* Integration templates : All integration templates are identified by the integration name (as it appears in the consent integrations dashboard), the template name (such as OneTrust, Usercentrics, Custom, etc.), and the internal Tealium ID for your instance of that template. For example: `Consent Integrations - Test Integration (onetrust) UID:utcm_e9582a8f-40fd-49ae-9819-fb2721f5547e`
  * Didomi
  * OneTrust
  * OptOut Cookie + GPC
  * Usercentrics
  * Custom

### Marketplace Tags

All marketplace templates are identified by their vendor name (as it appears in the marketplace), tag name (as entered in the tag configuration), and the tag UID. 

Example: `Twitter Conversions: Twitter Conversions (Retargeting): Tag UID: 2042
`

## Template Status Checker

The **Template Status Checker** tool compares each of your templates to the latest system version available. For more information, see [about the template status checker](https://docs.tealium.com/template-status-checker/).

## Access templates

The following methods are available for accessing templates:

* **Admin Menu**  
In the admin menu, click **Manage Templates**.  
This method lets you browse all templates in the profile and quickly access them from a drop-down list.
* **Tag Configuration**  
From the tag configuration screen, expand the **Advanced Settings** area and click **Edit Templates**. This method takes you directly to the template for that tag.
* **Template Status Checker**  
In the admin menu, click **Template Status Checker** then click a template in the report.  
This method displays a status report of your templates. The report contains links to each template.  
For more information, see [about the template status checker](https://docs.tealium.com/template-status-checker/).

## Template merge behavior

Tag templates do not follow standard merge behavior. When merging one version into another, the tag templates in the active version take priority. Any tag template changes from the merged version will be discarded. If you want to merge in tag templates from another version, switch to that version and then merge the tag templates into your original version.

For more information about merging versions, see [merging-versions](https://docs.tealium.com/merging-versions/).