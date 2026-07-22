---
title: Firebase Remote Command Order Event Example
url: https://docs.tealium.com/client-side-tags/firebase-remote-command-order-event-example/
---### Install

[Learn more](https://docs.tealium.com/platforms/remote-commands/integrations/firebase/) about the Tealium remote command integration for Firebase on Android and Swift/iOS

### Tag Setup

The Custom Command tag is a special tag that contains an implementation of the API required to trigger custom native code blocks you have registered with the Tealium mobile libraries.

[Learn more](https://docs.tealium.com/client-side-tags/firebase-remote-command-tag/) about setting up the Firebase Mobile Remote Command Tag in your Tealium iQ Tag Management (https://docs.tealium.com/client-side-tags/firebase-remote-command-tag/) account.

Extensions may be needed to update the data coming from the app through a tracking call. For example, you might be tracking a screen view using the Tealium SDK on the "Order Confirmation" screen, which you want to also log in the Firebase SDK.

The following is an example of the tracking call in Tealium for iOS (Swift):

```
`tealium?.trackView("order_confirmation", ["order_id":"A123456",
"user_id": "john.doe@someprovider.com", "user_loyalty_status":"vip", "travel_class" : "first"])
`
```

In the Firebase SDK, you may want to log this as an event using the `logEvent` API call, and also set a user property called `user_id`. In Tealium iQ, this is done in several different ways.

The value for the `command_name` variable is set to a comma-separated string of commands to execute. The 5 possible values that it may contains are:

* `config`
* `setUserId`
* `setScreenName`
* `setUserProperty`
* `logEvent`.

For this example, it is important to understand the order of operations in Tealium iQ. Extensions with the same "scope" are guaranteed to execute in order, from top to bottom as you see them in the Extensions tab. Therefore, logic is easily split into different extensions, but keep writing to a variable that was defined in an earlier extension.

1. Create a new data layer variable called `firebase_command_name` in your Tealium iQ profile.

1. Create a **Set Data Values** extension, select the new variable `firebase_command_name` from the dropdown list, and leave the data entry field blank. This initializes the variable to an empty string.

1. Create the following list of **Set Data Values** extensions, with the settings listed in the tables below:

#### config

Execute this configuration only once per session. The following lists the Tealium iQ configuration variables:

|TiQ Variable Name| Type| Example| Notes|
|---| ---| ---| ---|
|`command_name`| Text| `config`| Required, case-sensitive|
|`firebase_minimum_session_length`| Text| `10`| Optional|
|`firebase_session_timeout`| Text| `3600`| Optional|
|`firebase_analytics_enabled`| Text| `true`| Optional, case-sensitive, default = true|
|`firebase_log_level`| Text| `error`| Optional, case-sensitive|

This produces the following call in the native Firebase API:

Android:

```
`mFirebaseAnalytics = FirebaseAnalytics.getInstance(mCurrentActivity.getApplicationContext());
mFirebaseAnalytics.setSessionTimeoutDuration(3600);
mFirebaseAnalytics.setMinimumSessionDuration(10);
mFirebaseAnalytics.setAnalyticsCollectionEnabled(true);
`
```

Swift:

```
`let firConfig = FirebaseConfiguration.shared
let firAnalyticsConfig = AnalyticsConfiguration.shared()
firAnalyticsConfig.setSessionTimeoutInterval(3600)
firAnalyticsConfig.setMinimumSessionInterval(10)
firAnalyticsConfig.setAnalyticsCollectionEnabled(true)
firAnalyticsConfig.setLoggerLevel(FirebaseLoggerLevel.error)
firConfig.analyticsConfiguration = firAnalyticsConfig
FirebaseApp.configure()`
```

#### setUserId

The following user ID variables are available:

|TiQ Variable Name| Type| Example| Notes|
|---| ---| ---| ---|
|`firebase_command_name`| JS Code| `b.firebase\_command\_name + ",setUserId"`| Case-sensitive, comma-separated, no spaces|
|`firebase_user_id`| Text| `john.doe@someprovider.com`| (Required) Any valid string|

This produces the following call in the native Firebase API:

Android:

```
`FirebaseAnalytics.setUserId("john.doe@someprovider.com");
`
```

Swift:

```
`Analytics.setUserID("john.doe@someprovider.com")
`
```

#### setScreenName

The following screen name variables are available:

|TiQ Variable Name| Type| Example| Notes|
|---| ---| ---| ---|
|`firebase_command_name`| JS Code| `b.firebase_command_name + ",setScreenName"`| Case-sensitive, comma-separated, no spaces|
|`firebase_screen_name`| Text| `Order Confirmation`| (Required) Any valid string|
|`firebase_screen_class`| Text| `Order`| (Optional) Any valid string|

This produces the following call in the native Firebase API:

Android:

```
`FirebaseAnalytics.setCurrentScreen(&lt;current activity reference&gt;, "Order Confirmation", "Order");
`
```

Swift:

```
`Analytics.setScreenName("Order Confirmation", screenClass: "Order)
`
```

#### setUserProperty

The following user property variables are available:

|TiQ Variable Name| Type| Example| Notes|
|---| ---| ---| ---|
|`firebase_command_name`| JS Code| `b.firebase_command_name + ",setUserProperty"`| Case-sensitive, comma-separated, no spaces|
|`firebase_property_name`| Text| `user_loyalty_status`| (Required) Any valid string|
|`firebase_property_value`| Text| `vip`| (Required) Any valid string. Set to empty string to clear previously-set value.|

This produces the following call in the native Firebase API:

Android:

```
`FirebaseAnalytics.setUserProperty("user_loyalty_status", "vip");
`
```

Swift:

```
`Analytics.setUserProperty("vip", forName: "user_loyalty_status")
`
```

#### logEvent

The following log event variables are available:

|TiQ Variable Name| Variable| Example| Notes|
|---| ---| ---| ---|
|`firebase_command_name`| JS Code| `b.firebase_command_name + ",logEvent"`| Case-sensitive, comma-separated, no spaces|
|`firebase_event_name`| Text| `event_ecommerce_purchase`| (Required) Any valid string. Use one of the recommended event types listed above for best results.|
|`firebase_event_params`| JS Code| `{"param_travel_class" : b.travel_class, "param_transaction_id": b.order_id};`| (Optional) Any valid JSON object. Use one of the recommended default parameters listed above for best results. Custom parameters must be defined in the Firebase console before they show in reports.|

This produces the following call in the native Firebase API:

Android:

```
`Bundle b = new Bundle();
b.putString("param_travel_class", "first");
b.putString("param_transaction_id", "A123456")

FirebaseAnalytics.logEvent(FirebaseAnalytics.Event.ECOMMERCE_PURCHASE, b);
`
```

Swift:

```
`Analytics.logEvent(AnalyticsEventEcommercePurchase, parameters: [AnalyticsParameterTravelClass: "first", AnalyticsParameterTransactionID: "A123456"])`
```
