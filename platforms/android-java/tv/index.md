---
title: Android TV
description: Learn to install the Tealium SDK for Android TV.
url: https://docs.tealium.com/platforms/android-java/tv/
---

## Requirements

* Android TV app with [Tealium for Android](https://docs.tealium.com/platforms/android-java/)
* Android (Lollipop/5.0+ / API Level 21+ for Android TV)
* Android (Lollipop/5.1+ / API Level 22+ for Fire TV)
* [Tealium iQ Mobile Profile](https://docs.tealium.com/creating-a-mobile-profile/)
* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)

## API Reference

For the complete reference of classes and methods for Android TV, see the [`com.tealium.library`](https://tealium.github.io/tealium-android/com/tealium/library/package-summary.html) package in the Tealium SDK for Android API (it is the same for Android TV).


## Sample App

To help familiarize yourself with the Tealium library, tracking methods, and best practice implementation, explore the Tealium for Android TV [sample app](https://github.com/Tealium/tealium-android/tree/master/Samples/AndroidTVSample).

To abstract the Tealium implementation from the rest of your app, we recommend the use of the [sample helper class](https://github.com/Tealium/tealium-android/blob/master/Samples/BlankApp%2BTealium/app/src/main/java/com/tealium/blankapp/helper/TealiumHelper.java). This gives you a single entry point from which to initialize and make tracking calls. It also lets you update the code in your helper file, and not in every single Java file.

## Install

Install Tealium for Android TV on any Android TV device, including Amazon Fire TV.

### Android TV Device

To install Tealium for Android TV, the installation steps are the same as found on the [Tealium for Android](https://docs.tealium.com/platforms/android-java/install/) install guide.

### Amazon Fire TV

It is recommended to leverage Tealium when developing using the Amazon's Fire TV [Fire App Builder framework](https://github.com/amzn/fire-app-builder). Tealium is a vendor-neutral solution allowing you to send your data to multiple platforms without being locked into a single vendor.

Clone this fork of Amazon's [Fire App Builder](https://github.com/jonwongswong/fire-app-builder) library to get started with developing streaming apps on Fire TV and leverage the Tealium SDK.

## Tracking

### Track Views

The [`trackView()`](https://docs.tealium.com/platforms/android-java/api/tealium/#trackview) method tracks screen views, as shown in the following example:

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE KEY").trackView("SCREEN_NAME", data);
```

### Track Events

The [`trackEvent()`](https://docs.tealium.com/platforms/android-java/api/tealium/#trackevent) method tracks non-view events, as shown in the following example:

```java
Map<String, Object> data = new HashMap<>(1);
data.put("KEY", "VALUE");
Tealium.getInstance("INSTANCE KEY").trackEvent("EVENT NAME"", data);
```
