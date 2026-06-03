---
title: Consent management
description: Learn to implement consent for Android.
url: https://docs.tealium.com/platforms/android-java/consent-management/
---
## Usage

Usage of the consent management module is recommended, as it is automatically included in the library and enabled in the native code upon initialization.  

Supported platforms include: Android mobile, Android TV, and Android Wear.

For more information, see 

## Sample App

To help to familiarize yourself with our library, tracking methods, and best practice implementation, explore the Android consent management [sample app](https://github.com/Tealium/tealium-android/tree/master/Samples/ConsentManagerDemoApp).

See the [API Reference](/platforms/android-java/api/consent-manager/) for a list of consent management methods for Android.

## Enable

The following example enables consent management:

```java
//TealiumHelper.java
import com.tealium.library.ConsentManager;

public static final String TEALIUM_MAIN = &#34;main&#34;;

public static void initialize(Application application) {
	final Tealium.Config config = Tealium.Config.create(application, &#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;ENVIRONMENT&#34;);

	config.enableConsentManager(TEALIUM_MAIN); //enable with tealium instance name

	final Tealium tealiumInstance = Tealium.createInstance(TEALIUM_MAIN, config);
}
```

## Data Layer

The following variables are transmitted with each tracking call while consent management is enabled:

| Variable Name | Description | Example |
| --- | --- | --- |
| `policy` | The policy under which consent was collected | `gdpr` |
| `consent_status` | The user&#39;s current consent status | `consented` |
| `consent_categories` | The user&#39;s current categories they are consented to | `[ANALYTICS, CDP]` |


## Examples

### Simple Opt-in  

The following example shows how to opt-in to consent management:

```java
tealiumInstance.getConsentManager()
      .setUserConsentStatus(ConsentManager.ConsentStatus.CONSENTED);
```

### Group Opt-in

The following example shows a category-based consent model, where tracking categories are grouped into a smaller number of higher-level categories, defined by you:

```java
tealiumInstance.getConsentManager()
     .setUserConsentStatusWithCategories(ConsentManager.ConsentStatus.CONSENTED,
          new String[] {ConsentManager.ConsentCategory.ANALYTICS});
```

For examples, you may choose to group the Tealium consent categories `&#34;big_data&#34;`, `&#34;analytics&#34;`, and `&#34;monitoring&#34;` under a single category called &#34;performance&#34;. This may be easier for the user than selecting from the full list of categories. You may choose to represent this in a slider interface, ranging from least-permissive to most permissive (all categories).

![](/images/platforms/android/consent-slider.gif)

### Category-based Opt-in

The following example shows a category-based consent model where the user must explicitly select each category from the full list of categories. The default is `UNKNOWN`, which queues hits until the user provides their consent. If the user consents to any categories, events are de-queued, and the consent category data is appended to each tracking call.

```java
tealiumInstance.getConsentManager()
   .setUserConsentStatusWithCategories(ConsentManager.ConsentStatus.CONSENTED,
       new String[] {ConsentManager.ConsentCategory.ANALYTICS,
                     ConsentManager.ConsentCategory.PERSONALIZATION});
```


![](/images/platforms/android/consent-categories.gif)

