---
title: Create a mobile profile
description: This document explains how to create a mobile profile.
url: https://docs.tealium.com/iq-tag-management/profiles/creating-a-mobile-profile/
---
A mobile profile is used with an installation of one of the following mobile application platforms:

* [Tealium for iOS](/platforms/ios-swift/install/)
* [Tealium for Android](/platforms/android-kotlin/install/)

## How it works

Profiles in your iQ Tag Management account are configured for use on a website by default. Any profile can be activated for use within a native mobile installation. You can activate an existing profile for mobile use or create a new profile. Using separate profiles for your mobile apps lets you manage settings and vendor tracking deployed to each of your mobile apps.

## Create a new profile for a mobile app

We recommend that you create a separate profile for each mobile application that you intend to install Tealium on. For example, the most common profile names for mobile apps are: `mobile-ios` and `mobile-android`.

Learn more about [managing profiles]().

## Activate a mobile profile

Use the following steps to activate a profile for use on mobile:

1. Log in and load the profile that you intend for use for your mobile application.
1. In the admin menu, click **Configure Publish Settings**. The **Publish Configuration** dialog appears.
1. Click the **Mobile Library Publishing** tab.  
    ![](/images/iq-tag-management/whiteui-tiq-creating-a-mobile-profile-activate-mobile-library.jpg)
1. Click **Activate Mobile Library** and then click **Activate** to confirm.
1. Click **Save**.
1. Save and publish your settings.  

This profile can now be referenced in your Tealium for Mobile application by referencing the account name, profile name, and publish environment.

Standard mobile variables are added to the profile and available to the data layer settings for use with tags and extensions.

## Configure mobile settings

Use your mobile profile to adjust the configuration settings that determine the behavior of your mobile installation.

Use the following steps to adjust your mobile configuration settings:

1. Log on to Tealium iQ using the profile that you intend for use for your mobile applications.
1. In the admin menu, click **Configure Publish Settings**. The **Publish Configuration** dialog appears.
1. Click the **Mobile Library Publishing** tab.  
Mobile publish settings are enabled by default. You can optionally scroll through the mobile publishing settings, as described in the following table, and adjust as needed.

| Configuration| Description|
|:------------ |:------------|
| Tag Management                        | &lt;ul&gt;&lt;li&gt;Enables mobile tag management in your application for client-side event tracking.&lt;/li&gt;&lt;li&gt;`utag.js` runs in a webview.&lt;/li&gt;&lt;/ul&gt;|
| Tealium Collect                       | &lt;ul&gt;&lt;li&gt;Enable native mobile tracking for server-side data management (HTTP calls directly to EventStream).&lt;/li&gt;&lt;li&gt;Set to **OFF** if you enabled Tag Management.&lt;/li&gt;&lt;/ul&gt;|
| Tealium S2S Legacy                    | &lt;ul&gt;&lt;li&gt;Set to **ON** for events and views to be sent through Tealium S2S legacy protocol.&lt;/li&gt;&lt;/ul&gt;|

### Batching

| Configuration| Description|
|:------------ |:------------|
| Send Batch Data after every (#) event | &lt;ul&gt;&lt;li&gt;Lets you set the number of events (size of batch) that must occur before data is sent back.&lt;/li&gt;&lt;li&gt;Entering a value of  or **1** essentially turns off batching.&lt;/li&gt;&lt;li&gt;The default value is set to **1**.&lt;/li&gt;&lt;/ul&gt;|
| WiFi Only Sending                     | &lt;ul&gt;&lt;li&gt;By enabling **ON**, events only send when the user&#39;s device is connected to WiFi.&lt;/li&gt;&lt;li&gt;The default value is **OFF**.&lt;/li&gt;&lt;/ul&gt;|
| Battery Saver                         | &lt;ul&gt;&lt;li&gt;By enabling **ON**, data is only sent when the device has adequate battery power and is not in power saving mode.  &lt;ul&gt;&lt;li&gt;iOS: 20% battery and not charging.&lt;/li&gt;&lt;li&gt;Android: 15% battery&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;The default value is **ON**.&lt;/li&gt;&lt;/ul&gt;|

### Data Retention

| Configuration| Description|
|:------------ |:------------|
| Dispatch Expiration in (#) days       | &lt;ul&gt;&lt;li&gt;Specify how long (in days) the data persists in the application if no data has been sent back.&lt;/li&gt;&lt;li&gt;A value of **-1** means there is no dispatch expiration.&lt;/li&gt;&lt;li&gt;The default value is set to **-1**.&lt;/li&gt;&lt;li&gt;Dispatch expiration is also applied to events queued due to WiFi only Sending or Battery Saver settings.&lt;/li&gt;&lt;/ul&gt;                                      |
| Minutes Between Synchronization       | &lt;ul&gt;&lt;li&gt;The number of minutes between configuration checks (checks occur at launches and wakes).&lt;/li&gt;&lt;li&gt;The default value is **15.0**.&lt;/li&gt;&lt;/ul&gt;|
| Queue Capacity                        | &lt;ul&gt;&lt;li&gt;The number of events and views to store on the device until ready to send.  &lt;ul&gt;&lt;li&gt;**0** = no offline dispatching&lt;/li&gt;&lt;li&gt;**-1** = no limit&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;The default value is **-1**.&lt;/li&gt;&lt;/ul&gt;|

### Debugging

| Configuration| Description|
|:------------ |:------------|
| Set Debugging Log Level               | &lt;ul&gt;&lt;li&gt;Lets you enable logging.&lt;/li&gt;&lt;li&gt;Select one of the following settings:  &lt;ul&gt;&lt;li&gt;**Default** – Sets the log level to match the Environment setting in your configuration.&lt;/li&gt;&lt;li&gt;**Dev** – Log activity, info, warnings, and errors&lt;/li&gt;&lt;li&gt;**QA** – Log info, warnings, and errors&lt;/li&gt;&lt;li&gt;**Prod** – Log errors&lt;/li&gt;&lt;li&gt;**Silent** – Do not log&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |

When you are ready, click **Save**, and save and publish your settings.  

The next time your mobile application is loaded, the new configuration is detected and applied.
