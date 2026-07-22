---
title: Create a mobile profile
description: This document explains how to create a mobile profile.
url: https://docs.tealium.com/iq-tag-management/profiles/creating-a-mobile-profile/
---
A mobile profile is used with an installation of one of the following mobile application platforms:

* [Tealium for iOS](https://docs.tealium.com/platforms/ios-swift/install/)
* [Tealium for Android](https://docs.tealium.com/platforms/android-kotlin/install/)

## How it works

Profiles in your iQ Tag Management account are configured for use on a website by default. Any profile can be activated for use within a native mobile installation. You can activate an existing profile for mobile use or create a new profile. Using separate profiles for your mobile apps lets you manage settings and vendor tracking deployed to each of your mobile apps.

## Create a new profile for a mobile app

We recommend that you create a separate profile for each mobile application that you intend to install Tealium on. For example, the most common profile names for mobile apps are: `mobile-ios` and `mobile-android`.

Learn more about [managing profiles](https://docs.tealium.com/manage-profiles/).

## Activate a mobile profile

Use the following steps to activate a profile for use on mobile:

1. Log in and load the profile that you intend for use for your mobile application.
1. In the admin menu, click **Configure Publish Settings**. The **Publish Configuration** dialog appears.
1. Click the **Mobile Library Publishing** tab.  
    ![](https://docs.tealium.com/images/iq-tag-management/whiteui-tiq-creating-a-mobile-profile-activate-mobile-library.jpg)
1. Click **Activate Mobile Library** and then click **Activate** to confirm.
1. Click **Save**.
1. Save and publish your settings.  

This profile can now be referenced in your Tealium for Mobile application by referencing the account name, profile name, and publish environment.


<blockquote>
Standard mobile variables are added to the profile and available to the data layer settings for use with tags and extensions.
</blockquote>


## Configure mobile settings

Use your mobile profile to adjust the configuration settings that determine the behavior of your mobile installation.

Use the following steps to adjust your mobile configuration settings:

1. Log on to Tealium iQ using the profile that you intend for use for your mobile applications.
1. In the admin menu, click **Configure Publish Settings**. The **Publish Configuration** dialog appears.
1. Click the **Mobile Library Publishing** tab.  
Mobile publish settings are enabled by default. You can optionally scroll through the mobile publishing settings, as described in the following table, and adjust as needed.

| Configuration| Description|
|:------------ |:------------|
| Tag Management                        | <ul><li>Enables mobile tag management in your application for client-side event tracking.</li><li>`utag.js` runs in a webview.</li></ul>|
| Tealium Collect                       | <ul><li>Enable native mobile tracking for server-side data management (HTTP calls directly to EventStream).</li><li>Set to **OFF** if you enabled Tag Management.</li></ul>|
| Tealium S2S Legacy                    | <ul><li>Set to **ON** for events and views to be sent through Tealium S2S legacy protocol.</li></ul>|

### Batching

| Configuration| Description|
|:------------ |:------------|
| Send Batch Data after every (#) event | <ul><li>Lets you set the number of events (size of batch) that must occur before data is sent back.</li><li>Entering a value of  or **1** essentially turns off batching.</li><li>The default value is set to **1**.</li></ul>|
| WiFi Only Sending                     | <ul><li>By enabling **ON**, events only send when the user's device is connected to WiFi.</li><li>The default value is **OFF**.</li></ul>|
| Battery Saver                         | <ul><li>By enabling **ON**, data is only sent when the device has adequate battery power and is not in power saving mode.  <ul><li>iOS: 20% battery and not charging.</li><li>Android: 15% battery</li></ul> </li><li>The default value is **ON**.</li></ul>|

### Data Retention

| Configuration| Description|
|:------------ |:------------|
| Dispatch Expiration in (#) days       | <ul><li>Specify how long (in days) the data persists in the application if no data has been sent back.</li><li>A value of **-1** means there is no dispatch expiration.</li><li>The default value is set to **-1**.</li><li>Dispatch expiration is also applied to events queued due to WiFi only Sending or Battery Saver settings.</li></ul>                                      |
| Minutes Between Synchronization       | <ul><li>The number of minutes between configuration checks (checks occur at launches and wakes).</li><li>The default value is **15.0**.</li></ul>|
| Queue Capacity                        | <ul><li>The number of events and views to store on the device until ready to send.  <ul><li>**0** = no offline dispatching</li><li>**-1** = no limit</li></ul> </li><li>The default value is **-1**.</li></ul>|

### Debugging

| Configuration| Description|
|:------------ |:------------|
| Set Debugging Log Level               | <ul><li>Lets you enable logging.</li><li>Select one of the following settings:  <ul><li>**Default** – Sets the log level to match the Environment setting in your configuration.</li><li>**Dev** – Log activity, info, warnings, and errors</li><li>**QA** – Log info, warnings, and errors</li><li>**Prod** – Log errors</li><li>**Silent** – Do not log</li></ul> </li></ul> |

When you are ready, click **Save**, and save and publish your settings.  

The next time your mobile application is loaded, the new configuration is detected and applied.
