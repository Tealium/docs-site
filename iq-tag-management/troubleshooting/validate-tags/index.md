---
title: Validate and troubleshoot tags
description: This guide explains how to validate client-side tags that have been implemented in Tealium iQ. It will cover several methods to ensure that tags are loading and that data is being sent.
url: https://docs.tealium.com/iq-tag-management/troubleshooting/validate-tags/
---
## Getting started

The validation methods covered here are performed using Google Chrome as the browser and vendor specific plugins.

### Vendor plugins

We recommend downloading the following plugins for Google Chrome:

* [Google Tag Assistant](https://chrome.google.com/webstore/detail/tag-assistant-by-google/kejbdjndbnbjgmefkgdddjlbokphdefk?hl=en)
* [Google Analytics Debugger](https://chrome.google.com/webstore/detail/google-analytics-debugger/jnkmfdileelhofjcijamephohjechhna?hl=en)
* [Facebook Pixel Helper](https://chrome.google.com/webstore/detail/facebook-pixel-helper/fdgfkebogiimcoedlicjlajpkdmockpc?hl=en)
* [Adobe Analytics Debugger](https://chrome.google.com/webstore/detail/debugger-for-adobe-analyt/bdingoflfadhnjohjaplginnpjeclmof?hl=en)
* [Tealium Tools]()

### Chrome Developer Tools

We recommend taking a tutorial on Chrome Dev Tools to familiarize yourself with the interface:

* [Chrome Dev Tools Tutorial](https://www.codeschool.com/courses/discover-devtools)
* [Chrome Dev Tools Documentation](https://developers.google.com/web/tools/chrome-devtools/)

## Validate with Google Tag Assistant

The following list provides links that describe parameters for popular Google tags:

* [Google Analytics Parameters Cheat Sheet](https://www.cheatography.com/dmpg-tom/cheat-sheets/google-universal-analytics-url-collect-parameters/)
* [Google Analytics Enhanced Ecommerce Parameters Cheat Sheet](https://www.cheatography.com/nikalytics/cheat-sheets/enhanced-ecommerce-universal-analytics/)
* [Google Adwords Remarketing Parameters](https://developers.google.com/adwords-remarketing-tag/parameters)
* [Google Adwords Remarketing Verification](https://developers.google.com/adwords-remarketing-tag/verification)
* [More About Google Tag Assistant](https://support.google.com/analytics/answer/6277313?hl=en)

Use the following steps to validate with the Google Tag Assistant:

1. After you download the plugin, open your site to where the Tealium tags are installed and click the plugin icon in the upper-right corner of your Chrome window.  
    ![](/images/iq-tag-management/tag-assistant.png)

1. Select **Validate All Pages** then click **Done**.  
    ![](/images/iq-tag-management/image-2017-12-28-09-41-08.png)

1. Click **Allow** to allow the plugin to check if other plugins are blocking any Google tags and then click on any Google tags appearing in the plugin interface for more details.  
    ![](/images/iq-tag-management/image-2017-12-28-09-44-50.png)

1. For Google Analytics, click either **Pageview Requests** or **Events**.
The following example shows the results that display when you click **Pageview Requests**.
    ![](/images/iq-tag-management/image-2017-12-28-10-00-07.png)

1. When you click either of those, you will see the parameters sent to Google.
Clicking the **URLs** tab provides a more detailed view.
    ![](/images/iq-tag-management/image-2017-12-28-10-02-02.png)|

1. The default view shows the unformatted URL request. Change to the formatted view by clicking the table button.
This will allow you to see each parameter sent to Google. However, you should be fine viewing the initial **Metadata** tab.
  
    ![](/images/iq-tag-management/image-2017-12-28-10-03-53.png)

1. You can validate any other Google tags using this plugin as well.
Some examples are: Floodlight, Google Ads, Google Publisher, DFP, Google Trusted Stores.

## Validate with Google Debugger

The following list provides links that describe parameters for the Google Analytics tag:

* [Google Analytics Parameters Cheat Sheet](https://www.cheatography.com/dmpg-tom/cheat-sheets/google-universal-analytics-url-collect-parameters/)
* [Google Analytics Enhanced Ecommerce Parameters Cheat Sheet](https://www.cheatography.com/nikalytics/cheat-sheets/enhanced-ecommerce-universal-analytics/)

Use the following steps to validate with Google Debugger:

1. After you download the plugin, open your site where the Tealium tags are installed and click the plugin icon in the upper-right corner of your Chrome window.  
    ![](/images/iq-tag-management/section-page-2017-12-28-10-27-20.png)
    The live output in the [Chrome Developer Tools Console](https://developers.google.com/web/tools/chrome-devtools/console/) appears.
1. Start triggering events and page views and you will see the Google Analytics output in the console.  
The output displays what is getting sent to Google Analytics.  
    ![](/images/iq-tag-management/section-page-2017-12-28-10-28-48.png)|

## Validate with Facebook Pixel Helper

There are a number of events that will be displayed in this window depending on the type of interaction. Go to [Facebook Events](https://developers.facebook.com/docs/ads-for-websites/pixel-events/v2.11#events) to learn about these events and the parameters that can be sent with each.

Use the following steps to validate with the Facebook Pixel Helper:

1. After you download the plugin, open your site where the Tealium tags are installed and click the plugin icon in the upper-right corner of your Chrome window.  
    ![](/images/iq-tag-management/image-2017-12-28-11-13-34.png)
1. After you expand an event within the plugin, the parameters appear as follows:  
    ![](/images/iq-tag-management/image-2017-12-28-11-20-25.png)
1. Each pixel type detected can be expanded to display the details.  
In this example, the `AddToCart` pixel event is shown:  
The data that appears is the data sent to Facebook.  
    ![](/images/iq-tag-management/image-2017-12-28-11-21-53.png)

## Validate with Adobe Analytics Debugger

There are a number of parameters that will be displayed in the Adobe Analytics debugger. Go to [Adobe Query Parameters](https://marketing.adobe.com/resources/help/en_US/sc/implement/query_parameters.html) to learn more about the parameters for the Adobe Analytics (AppMeasurement) tag.

Use the following steps to validate using the Adobe Analytics Debugger:

1. After you download the plugin, open your site where the Tealium tags are installed and click the plugin icon in the upper-right corner of your Chrome window.
The screen displays the live output in the [Chrome Developer Tools Console](https://developers.google.com/web/tools/chrome-devtools/console/).  
    ![](/images/iq-tag-management/drapey-tie-neck-top-gap-2017-12-28-11-28-20.png)

1. Start triggering events and pageviews and the Adobe Analytics output will display in the console.  
This console output represents all the data that is sent to Adobe in each server call.  
    ![](/images/iq-tag-management/drapey-tie-neck-top-gap-2017-12-28-11-29-46.png)

## Validate with Chrome Developer Tools

Not all vendors have their own plugins. In this case, we recommend using the Chrome Developer Tools&#39; **Network** tab to validate that requests are successfully sent by the tags from the browser.

For more information, see the [Chrome DevTools Network Analysis](https://developers.google.com/web/tools/chrome-devtools/network-performance/reference) and search the document for **View query string parameters** to learn more about the parameters available.

Use the following steps to validate using Chrome Developer tools:

1. Open your site where Tealium is installed.
1. To display the Developer Tools, right-click the page and select **Inspect**.  
    ![](/images/iq-tag-management/chrome-inspect.png)

1. Click the **Network** tab.  
This example uses Google Analytics, but you can use any tag.  
    ![](/images/iq-tag-management/section-page-2017-12-28-13-12-38.png)

1. In Tealium iQ, find the **Tracking ID** in the configuration portion of the tag and copy the ID number.  
    ![](/images/iq-tag-management/tiq---services-christina-2017-12-28-13-13-14.png)

1. Navigate back to your site where the Network tab is still open and paste the ID number in the **Filter** box.  
    ![](/images/iq-tag-management/section-page-2017-12-28-13-13-56.png)

1. Click the **Preserve Log** checkbox and start executing page views and/or events.  
The network requests being sent by the tag appear.  
    ![](/images/iq-tag-management/section-page-2017-12-28-13-15-15.png)

1. Click an entry to view the details of the request.  
You will see several sections of information here, such as` Request URL`, `Response Headers`, `Cookies`, and `Query Parameters`.  
We are most interested in `Request URL` and `Query Parameters` but you will find more information on the others here: **Chrome Network Tab**
![](/images/iq-tag-management/section-page-2017-12-28-13-15-55.png)
The **Request URL** is the entire URL that was either sent as a POST or GET to the vendor&#39;s server. This URL includes the server URL and the query string parameters (the data) that the vendor will receive.  
![](/images/iq-tag-management/section-page-2017-12-28-13-18-25.png)
The **Query String Parameters** are a list of the parameters (not including the server url) that the vendor is receiving. This is most likely how data is passed from the page to the vendor.  
![](/images/iq-tag-management/section-page-2017-12-28-13-20-01.png)
The following example shows the Query String Parameters from an Adobe AppMeasurement server call:   
![](/images/iq-tag-management/drapey-tie-neck-top-gap-2017-12-28-13-22-40.png)

## Troubleshooting

There may be an instance where you find something missing in the Query Parameters or one of the plugins. If you would like to try and troubleshoot this yourself, there are some things you can try:

* First, use Web Companion or the Universal Tag Monitor to verify the data layer variables used in your page and event tracking calls. [Learn more](/platforms/javascript/install/#validate-installation).
* If your data layer is incomplete, it may require additional development work to include the variables you need.
* If your data layer looks good and your tracking calls are working as expected, but your vendor tags are not receiving the data you expect, the next step is to verify the data mappings for your tag. Data mappings tell Tealium which data layer variables to send to the corresponding vendor parameters. [Learn more]().
