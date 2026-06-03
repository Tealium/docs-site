---
title: Webtrends Tag Setup Guide
url: https://docs.tealium.com/client-side-tags/webtrends-tag/
---## Tag Specifications and Requirements

#### Specifications

* **Name**: Webtrends
* **Vendor**: Webtrends
* **Type**: Web Analytics

#### Required

Webtrends On Demand Account

Configurations:

* Web server time zone
* DCSID (Data Collection Server ID)
* Data Collection Server address
* Subdomain(s) of your site
* DCSID of the subdomain(s)

## Tag Configuration in Tealium iQ

#### Adding the Tag

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

#### Configuring the Tag

![](/images/client-side-tags/no-title-1024i83a5e04f7e903e54.png)

![](/images/client-side-tags/no-title-1025i528d8a79e781f8d3.png)

![](/images/client-side-tags/no-title-1026i376757c72484df88.png)

1. **Title**: (Required) Enter a descriptive title to identify the Tag instance.
1. **Code Version**: (Required) From the drop-down list, select the Tag version you want to set up.  
**Tip**: The Webtrends version number is provided in the commented section at the top of the JavaScript file.  
 E.g.: //WebTrends SmartSource Data Collector Tag v10.4.12//
1. **DCSID**: (Required) Enter the string value of the DCSID (Data Collection Server ID)—also called SmartSource Site ID—in the format &#34;dcsxxxxxxxxxxxxxxxxxxxxxx_xxxx&#34;.
1. **Collection Server**: (Required) By default, this field is pre-populated with the domain name (IP address) of the data collection server for Webtrends On Demand. Leave the default value as is.
1. **Timezone Offset**: (Optional) From the drop-down list, select the time zone of the visitor&#39;s (web client) browser. The default time zone is set to GMT&#43;00:00.
1. **Download Types**: (Required) Enter the comma-separated list of downloadable file types you want to track on your site. By default, this field is pre-populated with the following file types: xls,doc,pdf,txt,csv,zip,docx,xlsx.
1. **Paid Search Params**: (Required) Enter the comma-separated list of query string parameters that are used to signal a paid search engine. The default parameter is &#39;gclid&#39;.
1. **Track Events**: (Required) Enable/disable click event tracking for the Tag. By default, this field is set to &#34;true&#34;.
    * To turn OFF event tracking, select &#39;false&#39; from the drop-down list.

1. **Trim Offsite Params**: (Required) Choose whether or not you want to remove any query parameters from the off-site links to limit the number of unique URLs. By default, this field is set to &#34;true&#34;.
    * To include the query parameters in the URL, select &#39;false&#39; from the drop-down list.

1. **Enabled**: (Required) Enable/disable the Tag to collect and send data. By default, this field is set to &#34;true&#34;.
    * To disable data collection, select &#39;false&#39; from the drop-down list.

1. **i18n**: (Required) Enable/disable Internationalized Support for handling search phrases and query parameters in Asian languages. By default, this field is set to &#34;false&#34;.
    * To enable Internationalized support, select &#39;true&#39; from the drop-down list.

1. **FPC** **(Cookie)**: (Required) Enter the name of the first-party cookie. The default value is WT_FPC.
1. **Split Value**: (Optional) Enter the alphanumeric value of the WT.sp parameter to split a Parent Child profile into sub-profiles.  
**Note**: Webtrends recommends you use a short, alphanumeric value (a-z, A-Z, 0-9 only). Do not include symbols.
1. **Preserve**: (Required) Choose whether or not you want to preserve the base parameters collected during initial track calls. By default, this field is set to &#34;true&#34;.
    * To allow modification of the base parameters by multitrack calls, select &#39;false&#39; from the drop-down list.

1. **Testing Domains**: (Required) Enter the comma-separated list of onsite domains that are identified by the same DCSID.  
 E.g.: testing.example.com, dev.example.com
1. **Testing DCSID**: (Required) Enter the DCSID value of the testing domain(s).
1. **Heat Map Plugin**: (Optional) Enable/disable the Heatmap plugin which records the location of mouse clicks on a page. By default, this plugin is turned &#34;Off&#34;.
    * To enable the plugin, set it to &#34;On&#34;.

1. **YouTube Plugin**: (Optional) Enable/disable the YouTube plugin which tracks visitors&#39; interaction with YouTube videos on a webpage. By default, this plugin is turned &#34;Off&#34;.
    * To enable the plugin, set it to &#34;On&#34;.

1. **Facebook Plugin**: (Optional) Enable/disable the Facebook plugin which tracks Like(s), Share(s) and other Facebook events. By default, this plugin is turned &#34;Off&#34;.
    * To enable the plugin, set it to &#34;On&#34;.

1. **Ads Plugin**: (Optional) Enable/disable the Ads plugin which detects the presence of the Ads Click parameter in the query string. By default, this plugin is turned &#34;Off&#34;.
    * To enable the plugin, set it to &#34;On&#34;.

1. **Replicate Plugin**: (Optional) Enable/disable the Replicate plugin which sends data to specific collection servers. By default, this plugin is turned &#34;Off&#34;.
    * To enable the plugin, set it to &#34;On&#34;.

**Tip**: Place this Tag at the bottom of the list in the Tags tab; Webtrends recommends you load this Tag after the page has finished loading.

#### Applying Load Rules

[Load Rules]() determine when and where to load an instance of this Tag. The &#39;Load on All Pages&#39; rule is the default Load Rule. To load this Tag on a specific page, create a new load rule with the relevant conditions.

**Note**: We recommend that you load the Tag on every page for accurate collection of visitor data. Leave the default &#39;Load on All Pages&#39; selection as is.

#### Setting up Mappings

[Mapping](/iq-tag-management/data-mappings/manage/) is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor Tag. The destination variables for this Tag are available in the Mapping toolkit. For ease of use, the variables are grouped into different categories.

#### Vendor Documentation

* [Webtrends JavaScript Tag configuration](http://help.webtrends.com/en/jstag/)
* [Webtrends Query Parameter Reference](http://help.webtrends.com/en/QueryParameters/index.html)
* [Documentation Center: User Guides and Release Notes](https://product.webtrends.com/wrc/ondemand/documentationcenter/)