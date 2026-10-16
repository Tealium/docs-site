---
title: Create a mobile profile
description: Learn how to create a mobile profile.
url: https://docs.tealium.com/iq-tag-management/profiles/create-mobile-profile/
---
Use mobile profiles to manage settings and vendor tracking for your mobile app separately from your website.

## For Tealium Prism

A mobile profile is used with an installation of one of the following mobile application platforms:

* [Tealium Prism](https://docs.tealium.com/platforms/prism-mobile//)

### Create a mobile profile for Tealium Prism

For [Tealium Prism](https://docs.tealium.com/platforms/prism-mobile//), you configure a mobile profile when you create it. No additional activation steps are required.

1. In Tag Management, go to **Admin Menu > Manage Profiles**.
1. In the side panel, under **Profiles**, click **+ Add**.
1. Enter a profile name.
1. Select **Mobile Profile**.  
   ![](https://docs.tealium.com/images/platforms/prism/create-mobile-prism-profile.png)
1. Click **Create Profile**.

For more information on configuring a Tealium Prism mobile profile, see:
* [Prism: Modules](https://docs.tealium.com/platforms/prism-mobile/modules/)
* [Prism: Rules](https://docs.tealium.com/platforms/prism-mobile/rules/)
* [Prism: Barriers](https://docs.tealium.com/platforms/prism-mobile/barriers/)
* [Prism: Transformations](https://docs.tealium.com/platforms/prism-mobile/transformations/)

## For Tealium for iOS (Swift) 2.x and Tealium for Kotlin

These section is for installations of the following libraries:

* [Tealium for iOS](https://docs.tealium.com/platforms/ios-swift/install/)
* [Tealium for Android](https://docs.tealium.com/platforms/android-kotlin/install/)

For these SDK versions, first you create a profile, then you convert it to a mobile profile. We recommend that you create a separate profile for each mobile application that you intend to install Tealium on. For example, the most common profile names for mobile apps are: `mobile-ios` and `mobile-android`.

### Create and activate a mobile profile for iOS and Android


<blockquote>
For new mobile installations, we recommend using [Tealium Prism](#for-tealium-prism).
</blockquote>


To create and activate a profile for use with the Tealium for iOS or Android SDK:

1. Log in to Tealium Tag Management.
1. Go to **Admin Menu > Manage Profiles**.
1. Enter a profile name and click **Create Profile**.  
    
<blockquote>
Do not select **Mobile Profile** unless you are using the Tealium Prism SDK. For Swift 2.x and Kotlin SDKs leave this checkbox unselected.
</blockquote>

1. In the profile switcher, select the profile you just created.
1. In the admin menu, click **Configure Publish Settings**. The **Publish Configuration** dialog appears.
1. Click the **Mobile Library Publishing** tab.  
    ![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-creating-a-mobile-profile-activate-mobile-library.jpg)
1. Click **Activate Mobile Library** and then click **Activate** to confirm.
1. Click **Save**.
1. Save and publish your settings.  


<blockquote>
Standard mobile variables are added to the profile and available to the data layer settings for use with tags and extensions.
</blockquote>


This profile can now be referenced in your mobile application by referencing the account name, profile name, and publish environment. For setup instructions, see:

* [Tealium for iOS](https://docs.tealium.com/platforms/ios-swift/install/)
* [Tealium for Android](https://docs.tealium.com/platforms/android-kotlin/install/)

### Configure mobile settings

Use the following steps to adjust your mobile configuration settings:

1. Log on to Tealium Tag Management and select the account and profile for mobile application.
1. In the admin menu, click **Configure Publish Settings**. The **Publish Configuration** dialog appears.
1. Click the **Mobile Library Publishing** tab.  
Mobile publish settings are enabled by default. You can optionally scroll through the mobile publishing settings, as described in the following table, and adjust as needed.

| Configuration| Description|
|:------------ |:------------|
| Tag Management| <ul><li>Enables mobile tag management in your application for client-side event tracking.</li><li>`utag.js` runs in a webview.</li></ul>|
| Tealium Collect| <ul><li>Enable native mobile tracking for server-side data management (HTTP calls directly to EventStream).</li><li>Set to **OFF** if you enabled Tag Management.</li></ul>|
| Tealium S2S Legacy| <ul><li>Set to **ON** for events and views to be sent through Tealium S2S legacy protocol.</li></ul>|

#### Batching

| Configuration| Description|
|:------------ |:------------|
| Send Batch Data after every (#) event | <ul><li>Lets you set the number of events (size of batch) that must occur before data is sent back.</li><li>Entering a value of  or **1** essentially turns off batching.</li><li>The default value is set to **1**.</li></ul>|
| WiFi Only Sending                     | <ul><li>By enabling **ON**, events only send when the user's device is connected to WiFi.</li><li>The default value is **OFF**.</li></ul>|
| Battery Saver                         | <ul><li>By enabling **ON**, data is only sent when the device has adequate battery power and is not in power saving mode.  <ul><li>iOS: 20% battery and not charging.</li><li>Android: 15% battery</li></ul> </li><li>The default value is **ON**.</li></ul>|

#### Data Retention

| Configuration| Description|
|:------------ |:------------|
| Dispatch Expiration in (#) days       | <ul><li>Specify how long (in days) the data persists in the application if no data has been sent back.</li><li>A value of **-1** means there is no dispatch expiration.</li><li>The default value is set to **-1**.</li><li>Dispatch expiration is also applied to events queued due to WiFi only Sending or Battery Saver settings.</li></ul>                                      |
| Minutes Between Synchronization       | <ul><li>The number of minutes between configuration checks (checks occur at launches and wakes).</li><li>The default value is **15.0**.</li></ul>|
| Queue Capacity                        | <ul><li>The number of events and views to store on the device until ready to send.  <ul><li>**0** = no offline dispatching</li><li>**-1** = no limit</li></ul> </li><li>The default value is **-1**.</li></ul>|

#### Debugging

| Configuration| Description|
|:------------ |:------------|
| Set Debugging Log Level               | <ul><li>Lets you enable logging.</li><li>Select one of the following settings:  <ul><li>**Default** – Sets the log level to match the Environment setting in your configuration.</li><li>**Dev** – Log activity, info, warnings, and errors</li><li>**QA** – Log info, warnings, and errors</li><li>**Prod** – Log errors</li><li>**Silent** – Do not log</li></ul> </li></ul> |

When you are ready, click **Save**, and save and publish your settings.  

The next time your mobile application is loaded, the new configuration is detected and applied.
