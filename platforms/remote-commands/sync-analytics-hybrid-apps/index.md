---
title: How to sync analytics sessions in hybrid apps
description: This document describes how to sync a session in a hybrid app.
url: https://docs.tealium.com/platforms/remote-commands/sync-analytics-hybrid-apps/
---
## Overview

A hybrid app combines components written in native code, such as Objective-C for iOS or Java for Android, and one or more webview components written in HTML and JavaScript. A common use case is a shopping app where a native code component is used for browsing products and a webview component is used for the checkout and payment processing.

### Problem

A common challenge for analytics vendors on hybrid apps is being able to track a session between the native component and the webview component. Even if the vendor is integrated into both components, a visitor will be assigned a separate session identifier in each and the vendor&#39;s reports will show inflated numbers for sessions.

To solve this problem, the native and webview components must share information. You can share information between these components by appending a query string parameter to the webview URL loaded by the native code. This parameter contains the shared session ID that is used in both the native and webview components.

The initiation and sharing of that session ID is accomplished with some configuration in Tealium iQ and with some custom code in your native app. The custom remote command tag facilitates the sharing of that session ID between the hidden webview and the native code, where it&#39;s  passed to your website that loads from a visible webview.

### Solution

This article demonstrates this solution using Google Analytics, but it applies to any vendor that supports session management. For the Google Analytics solution we retrieve a session ID (`clientId`) in the Tealium iQ SDK (generated in a hidden webview and passed to the native code through a remote command), pass it to the webview component of a hybrid app through a query string parameter, then use Tealium iQ to pass the session ID back to Google Analytics running on the website inside the webview. This example will focus mainly on Android, but the process for iOS is the same.

Here are the requirements for this solution:

1. Native code
    *  **Custom remote command**  
    A custom command defined in the native code to be called by the custom remote command tag. This allows the hidden webview to pass the session ID to the native code.
    *  **Webview Query String Parameter**  
    A query string parameter containing the session ID is appended to the URL that loads the webview component of your hybrid app.
1. iQ profile for mobile app  
The profile that manages your native app requires the following configuration:
    *   **Custom Remote Command tag** - A tag that facilitates communication between the hidden webview and the native app code.
    *   `session_id` - A UDO variable to store the vendor session ID that is passed by the custom remote command tag to the native code.
    *   **JavaScript Code extension** - JavaScript code to get the current session ID from the vendor and pass it to the custom remote command tag.
1. iQ profile for mobile web  
The following customizations are required in the iQ profile for the webview component of your hybrid app:
    *   **`session_id`** - A query string variable used in the URL of the webview to pass the session ID from the native code.
    *   **Custom JavaScript** - JavaScript code (extension or tag template) to pass the session ID to the vendor tag.


This article assumes that you are using Tealium for Android/iOS v5.0&#43; and requires that you redeploy your app.


Here is a summary of the solution for each component in the hybrid app:

&lt;table style=&#34;border: 1px solid rgb(237, 237, 237) !important&#34;&gt;&lt;thead&gt;&lt;tr&gt;&lt;td colspan=&#34;4&#34; style=&#34;text-align: center;&#34;&gt;&lt;strong&gt;Hybrid App&lt;/strong&gt;&lt;/td&gt;&lt;/tr&gt;&lt;/thead&gt;&lt;tbody&gt;&lt;tr &gt;&lt;th style=&#34;border: 1px solid rgb(237, 237, 237) !important;vertical-align: top; text-align: center;text-transform:uppercase;&#34; class=&#34;bg-secondary&#34; colspan=&#34;2&#34;&gt;Native Code&lt;br&gt;Component&lt;/th&gt;&lt;td rowspan=&#34;3&#34; style=&#34;vertical-align: top; text-align: center;border: 1px solid rgb(237, 237, 237) !important&#34;&gt;Native code loads webview at URL with:&lt;br&gt;&lt;code&gt;&amp;session_id=SESSION&lt;/code&gt;&lt;p&gt;&amp;nbsp;&lt;/p&gt;&lt;/td&gt;&lt;th style=&#34;vertical-align: top; text-align: center;text-transform:uppercase;&#34; class=&#34;bg-secondary&#34;&gt;Webview&lt;br&gt;Component&lt;/th&gt;&lt;/tr&gt;&lt;tr&gt;&lt;td style=&#34;vertical-align: top; text-align: center;&#34;&gt;iQ Mobile Profile&lt;br&gt;(run in hidden webview)&lt;/td&gt;&lt;td style=&#34;border: 1px solid rgb(237, 237, 237) !important;vertical-align: top; text-align: center;&#34;&gt;Native Code&lt;/td&gt;&lt;td style=&#34;vertical-align: top; text-align: center;&#34;&gt;iQ Profile for Website&lt;/td&gt;&lt;/tr&gt;&lt;tr&gt;&lt;td style=&#34;vertical-align: top;&#34;&gt;&lt;p&gt;Configure custom remote command &lt;code&gt;syncSessionId&lt;/code&gt; command&lt;/p&gt;&lt;p&gt;JavaScript Code Extension to get session ID from vendor&lt;/p&gt;&lt;p&gt;Call to &lt;code&gt;utag.link()&lt;/code&gt; to trigger custom remote command, passing session ID&lt;/p&gt;&lt;/td&gt;&lt;td style=&#34;vertical-align: top;border: 1px solid rgb(237, 237, 237) !important&#34;&gt;&lt;p&gt;Custom code to handle remote calls to syncSessionId&lt;/p&gt;&lt;p&gt;Custom code to pass session ID variable to the webview&lt;/p&gt;&lt;/td&gt;&lt;td style=&#34;vertical-align: top;&#34;&gt;&lt;p&gt;Query string variable &lt;code&gt;session_id&lt;/code&gt; from the webview URL&lt;/p&gt;&lt;p&gt;Vendor Tag with data mapping for &lt;code&gt;session_id&lt;/code&gt;&lt;/p&gt;&lt;/td&gt;&lt;/tr&gt;&lt;/tbody&gt;&lt;/table&gt;


## Implementation

### Add a remote command (native code)

Use the `addRemoteCommand` method to define a new command for the custom remote command tag to utilize. This allows the hidden Tealium webview to pass data to the Tealium library in the native code environment.

#### Android (Java code):

Although fully functional, this code is simply a sample to show how to accomplish this task. Use your own judgment, and always test before deploying code in your live app

1. Define a new remote command called `syncSessionId` that stores the passed session ID value into a native variable called `sessionId`. Place this code in the Tealium `init` block (often this will be in a helper file):  
    ```java
    // initialize Tealium
    Tealium.Config config = Tealium.Config.create(application, &#34;&#34;, &#34;&#34;, &#34;&#34;);
    // create a new Tealium instance with the above config object
    Tealium inst = Tealium.createInstance(TEALIUM\_INSTANCENAME, config);
    // register a new RemoteCommand with Tealium called &#34;syncGASession&#34;
    inst.addRemoteCommand(new RemoteCommand(&#34;syncSessionId&#34;, &#34;Syncs the Analytics Session ID&#34;) {
        // onInvoke will be called when Tealium iQ triggers the command
        @Override
        protected void onInvoke(Response response) throws Exception {
            // grab the response object
            JSONObject resp = response.getRequestPayload();
            // set the application-level &#34;gaSessionId&#34; String variable to the value of the key &#34;sessionId&#34; in the response
            // assumes you created this shared variable in your Application class. See sample app for details.
            DemoApplication.sessionId = resp.optString(&#34;sessionId&#34;, null);
        }
    });
    ```
1. Customize your webview to append the query string parameter `session_id` with the session value stored in the native code. Here&#39;s an example of a webview being created and the session ID being passed as a query string parameter:  
    ```java
    public class WebviewActivity extends AppCompatActivity {
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_webview);
            webview mywebview = (webview) findViewById(R.id.webview);
            mywebview.clearCache(true);
            mywebview.getSettings().setJavaScriptEnabled(true);
            mywebview.loadUrl(&#34;https://solutions.tealium.net/hosted/cpr/mobile_ga_demo.html?session_id=&#34; &#43; DemoApplication.sessionId);
        }
    }
    ```

#### iOS (Objective-C code)

Here&#39;s a fragment of the equivalent Objective-C code required to achieve the same thing on iOS. This code does not include the creation of the webview and is included as a starting point:

```objc
// replace with your instance name
Tealium *instanceHandle = [Tealium instanceForKey: @&#34;tealium&#34;]; 
[instanceHandle addRemoteCommandID:@&#34;syncSessionId&#34;
   description:@&#34;Syncs the Session ID&#34;
   targetQueue:dispatch_get_main_queue()
 // response is generated from the mappings set up in Tealium iQ
   responseBlock:^(TEALRemoteCommandResponse * _Nonnull response) {
 // grab the Session ID from the response object
       NSString *session_id = response.requestPayload[@&#34;sessionId&#34;];
 /* now that you have the session ID, store it somewhere you can 
 access it later on when you create your webview. See Android code
 for an example */
}\];
```

### Add the custom remote command tag (iQ profile for mobile web)

In your iQ mobile profile, use the custom remote command tag to trigger the remote command you defined in your native code. When you add data mappings to this tag, the remote command will receive that data.

Follow these steps in your iQ profile for mobile web:

1.  Add the following UDO variable to your data layer: `session_id`
2.  Add the **Custom Remote Command** tag:  
![](/images/platforms/remote-commands/sync-analytics1.jpg)
3.  Set the **Command ID** to `syncSessionId` (the name of the remote command defined in the native code):  
![](/images/platforms/remote-commands/sync-analytics2.jpg)
4.  Add a data mapping for `session_id` to `sessionId`.  
![](/images/platforms/remote-commands/sync-analytics3.jpg)

### Add the vendor tag (iQ profile for mobile app)

In your iQ profile for the mobile app, you will use a vendor tag (Google Analytics in this example) to initiate a session and pass the session ID value to the custom remote command tag using a call to `utag.link()`. Most likely you will already have this tag added to your mobile profile for the purpose of native app tracking (as many popular analytics tag are mobile enabled).

Follow these steps to add and configure the vendor tag:

1.  Add your vendor tag (if you haven&#39;t already).
2.  Add a JavaScript Code extension scoped to the vendor tag (Google Analytics) with the following contents. Replace `UID` with the UID of the custom remote command tag.  
    ```js
    window.setTimeout(function() {
         // Vendor Specific: Retrieve a session ID from Google Analytics
         var tracker = window.ga.getByName(&#39;tealium_0&#39;); // assumes you only have one GA tracker on the page
         var clientId = tracker.get(&#39;clientId&#39;);
         // A tracking call picked up custom remote command
         utag.link({session_id : clientId}, null, [&#39;UID&#39;])
    }, 1000);
    ```
    
This extension waits for 1 second to give the tag enough time to load, and then gets the session ID from the vendor. Then it calls `utag.link()` to trigger the custom remote command tag, passing `session_id` as a parameter. Then the custom remote command tag passes that data to the remote command `syncSessionId` where the native code stores it for later use.

### Add the vendor tag (iQ profile for mobile web)

In your iQ Web Profile (the profile used for the website that is loaded in the webview component of your hybrid app) you will define a new data layer variable to detect the query string parameter used for the session ID and map that variable into the vendor tag.

Follow these steps to configure your vendor tag to sync the session ID:

1.  Add your vendor tag, if you haven&#39;t already.
2.  Add a new data layer variable named `session_id` of type query string parameter.
3.  In the vendor tag, add a data mapping for `session_id` to `clientId` (specific to Google Analytics in this example).

You&#39;re now finished. Assuming you&#39;ve followed all the steps above, the webviews in your app will receive the same session identifier as the native app, and your users will now be using a single session (as far as Google Analytics is concerned).

### Validate the results

After deploying the code above, you can use a local proxy, such as Charles Proxy or Fiddler, to view the output from the app. If you inspect the outgoing hits to `www.google-analytics.com`, you can verify that the `cid` parameter is the same in the hit coming from your native app as well as from the webview component.

To learn more, see [Troubleshooting a mobile installation](/platforms/getting-started-mobile/troubleshooting/).

Shared session ID from the native app:

![](/images/platforms/remote-commands/sync-analytics4.png)

Shared session ID from from the in-app webview:

![](/images/platforms/remote-commands/sync-analytics5.png)

Download the sample app as an Android Studio project: [GAwebviewDemo.zip](/images/platforms/remote-commands/GAWebViewDemo.zip).

## Additional solutions

This guide describes how to sync the session IDs for Google Analytics, but the same steps can easily be adapted for use with other vendors, such as Webtrends, Webtrekk, and Adobe Analytics. Depending on the vendor, you might need to read cookie values if there is no API that provides the session ID.

The solution documented in this article could also be used to pass other information to your app, outside of the scope of your analytics tools. It is possible to pass more than one parameter at a time by adding more mappings in the custom remote command tag, but you will need to adapt the native remote command code to handle additional parameters in the response object.