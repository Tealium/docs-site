---
title: Publish configuration
url: https://docs.tealium.com/iq-tag-management/save-publish/publish-configuration/
---
Use the following steps to configure your publish settings:

1. In the admin menu, click **Configure Publish Settings**. The **Publish Configuration** dialog appears.
1. Select the **General Publishing** or **Mobile Library Publishing** configuration tab.  
    ![](/images/iq-tag-management/whiteui-publishconfiguratin-select-publish-tab.png)
1. Adjust settings as needed.
1. Click **Save** to apply your changes.  
Some settings require you to perform a publish to enable their functionality. See the following section for more information on each of the publish settings.

## General publishing

The **General Publishing** configurations are grouped depending on which aspect of your implementation they affect. The following sections provide descriptions of what each publish configuration does.

### Version workflow

These configurations allow you to fine-tune how this profile&#39;s implementation is saved and published.

* **Publish Notify Email**  
If you want to receive emails whenever a version is published, enter the emails into the Publish Notify Email field. You can add multiple email addresses by separating each additional email with a comma.
* **Custom Version Naming**  
Allow users to enter a custom version name rather than the default timestamp ID. Default value is **ON**.
* **Workflow Management**  
This setting lets you set up workflow management, whereby users with Dev and QA publish permissions can request permission to publish to Prod. Enabling workflow management will require approval for all publishes to Prod. Default value is **OFF**.
* **Lock Profile**  
Prevents multiple users from modifying a profile at the same time. Default value is **OFF**.
* **Alert Notify Email (DEPRECATED)**  
To be alerted when errors occur on your website, contact your account manager to enable this feature and then add your email address to this field. if left blank, no alerts will be created. Add multiple email addresses as a comma-separated list.  
This setting is not longer supported. If this was enabled in your profile, you will no longer receive alerts emails.

### Performance optimization

These publish configurations affect the overall performance of the Universal Tag (`utag.js`) on your site.

* **Ready Wait Flag**  
Enabling the Ready Wait Flag will halt all `utag.js` operations until the DOM-Ready signal is received from the browser. Extensions scoped to Pre Loader continue to execute before DOM-Ready. Default value is **OFF**.
* **Bundled Tags**  
Displays the list of bundled tags that do NOT use the default **All Pages** load rule.  
Learn more about [bundling and page performance]().
* **Bundle Tags Loading on All Pages**  
Bundle tags using the **All Pages** load rule into `utag.js`. This reduces the number of network calls made by the browser, potentially improving performance and page load times. Default value is **OFF**.  
Tag loading order for bundled tags is determined by the order they appear on the tags screen, not their UIDs.   
Learn more about [bundling and page performance]().
* **Minify Tag Templates**  
Minifies the code for `utag.js` and all published tags. Default value is **ON**. Minification is the process of removing unnecessary characters from code, such as empty spaces and comments. The functionality of the code remains unchanged. This has the benefit of reducing the overall amount of code, making it easier and faster to transfer and download. However, the code becomes more difficult to understand.

### Implementation

These settings affect how you implement the Universal Tag (`utag.js`).

* **Generate distro.zip file**  
This will generate a distribution archive of all generated tag files. For more information, see [Self hosting]().
* **Cookies Domain**  
Enter the domain you want to set for the `utag_main` cookie. By default, Tealium automatically detects the domain of the page, so we recommend that you leave this field empty. By doing so, Tealium automatically detects the domain. However, you can set this value to the domain of your site. If you use multiple subdomains, you should set this to the root domain (for example, `tealium.com` instead of `www.tealium.com`)
* **Page Data Object**  
To use a data object other than Tealium&#39;s `utag_data`, enter your preferred data object name here.
* **Base Variables**  
Enter a comma-separated list of `utag_data` variables to send on every tracking call.  
Example: `page_name,site_language,site_currency,is_logged_in`
* **Visitor Session Timeout**  
Set this value, in milliseconds, to override the default session timeout of 30 minutes. (1800000 ms = 30 minutes).
* **Custom Publish Environments**  
Lets you create custom publish environments in addition to the defaults Dev, QA, and Prod. Default value is OFF.
* **Generate utag.sync.js File**  
Lets you generate and publish the utag.sync.js file when you turn it **ON**. Default value is **OFF**. The first time you enable this setting, you must re-publish all of the publish environments for this profile to generate the `utag.sync.js` file. Using a `utag.sync.js` file also requires that you code a separate file reference on your site, preferably in the head element of your page. If you code the file reference on your site, but fail to publish to all of your publish environments after enabling this setting, your site will fail to load as it is making a synchronous call to a file that does not yet exist.  

This setting is also required for Tealium&#39;s Flicker Free Adobe Test &amp;amp; Target solution.

* **Use UTF-8 Encoding**  
Turn this toggle on if you want the utag.js file to be encoded with UTF-8 instead of the default ISO 8859-1. Default value is **ON**.  
    For profiles created before Nov. 10, 2015, the default is **Off**.

* **Prevent Tag Load**  
Quickly disable all tags managed by Tealium iQ. You must republish the profile after turning this on. Default value is **OFF**.
* **Web Companion**  
Toggle on or off to enable or disable support for Web Companion Target Environment swtiching.  
Enabling this feature allows your website to set a cookie with any arbitrary value, which could expose your system to code injections. This feature is offered as a convenience for those who cannot use the Google Chrome browser. If you can use Chrome, we recommend using the [Tealium Tools Environment Switcher](/iq-tag-management/tealium-tools/environment-switcher/) as a best practice.

* **Data Layer Enrichment Profile**  
Specify the AudienceStream profile from which to retrieve visitor data. The on-page data layer will then be enriched with this visitor data.

### Publishing URLs

These configurations allow you to specify a publication location other than Tealium&#39;s default servers. If you want to publish your profiles to a non-standard location (if your prod environment is not specified as &#34;prod&#34;), then enter the URL in the appropriate field. You may do this for each of the three environments: Dev, QA, and Prod.

* **Publish Dev URL**  
Use this setting if you are self-hosting your Tealium JavaScript files or if you use first-party domains. For more information, see [Self-Hosting utag.js]() and [First-Party Domains]().
* **Publish QA URL**  
Use this setting if you are self-hosting your Tealium JavaScript files or if you use first-party domains. For more information, see [Self-Hosting utag.js]() and [First-Party Domains]().
* **Publish Prod URL**  
Use this setting if you are self-hosting your Tealium JavaScript files or if you use first-party domains. For more information, see [Self-Hosting utag.js]() and [First-Party Domains]().

To restrict the delivery of your `utag.js` files to the Europe geographic region, you must enter `//tags-eu.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT` into the URL fields. Restricting the delivery locations to Europe in this way means that you are only using servers physically located in the EU to deliver your `utag.js` file.

### Legacy settings

These configurations are deprecated, but remain to support legacy deployments and should not be used for newer implementations (`utag.js` versions 4.26 and later).

* **Profile Can Be Subloaded**  
This is required when another profile uses the Profile Loader tag to load this profile. This functionality is deprecated in favor of [Profile Libraries]().
* **Force Timeout**  
Set this value, in milliseconds, to cancel slowly loading tags. Only tags that take longer than this value to load are cancelled. This configuration only works for profiles using utag.js versions before version 4.26. This configuration will not affect profiles using more recent utag.js versions.  
Tealium removes from the load queue any tag libraries that have not loaded by the time the force timeout value expires. The countdown to a forced timeout starts when the initial `utag.js` call is made, not when the subsequent tag library calls (`utag.1.js`, `utag.2.js`, et cetera) are made. Be aware that if a visitor&#39;s browser is running slowly, the Force Timeout feature could cause a tag to be cancelled even though the `utag.js` or tag library requests themselves aren&#39;t slow. Enter a high **Force Timeout** value to prevent unnecessary timeouts.
* **Extensions Scoped To Footer**  
Toggle on or off to set this value if this profile uses a `utag.footer.js` file to load extensions.

## Mobile library publishing

In this tab, you can activate mobile library support by clicking **Activate Mobile Library**. Learn more about [Creating a Mobile Profile]().
