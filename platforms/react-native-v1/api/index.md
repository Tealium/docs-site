---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for React Native.
url: https://docs.tealium.com/platforms/react-native-v1/api/
---
This is the previous version (1.x) of Tealium for React Native.  
For the current version, see [Tealium for React Native 2.x](/platforms/react-native/).

## Class: `Tealium`

The following summarizes the commonly used methods of the `Tealium` class for React Native library.

| Method | Description |
| ----- | ------ |
| `addRemoteCommand()`| Adds a remote command to the remote command manager |
| `addRemoteCommandForInstance()`| Adds a remote command to the remote command manager, for a specific Tealium instance |
| `getPersistentData()`| Gets the value for a specific key|
| `getPersistentDataForInstanceName()`| Get a persistent data value, for a specific Tealium instance and key|
| `getUserConsentCategories()` | Gets the consent categories of a user |
| `getUserConsentCatgoriesForInstanceName()`| Gets the consent categories of a user, for a specific Tealium instance |
| `getUserConsentStatus()`| Gets the consent status of a user|
| `getUserConsentStatusForInstanceName()`| Gets the consent status of a user, for a specific Tealium instance|
| `getVisitorID()`| Gets the visitorID of a user |
| `getVisitorIDForInstanceName()`| Gets the visitorID of a user, for a specific Tealium instance|
| `getVolatileData()`| Gets the value for the key passed in|
| `getVolatileDataForInstanceName()`| Get a volatile data value, for a specific Tealium instance and key|
| `initialize()` |Initialize Tealium before calling any other method |
| `initializeCustom()`|Initialize Tealium with all options before calling any other method |
| `initializeWithConsentManager()`| Initialize Tealium with consent management before calling any other method|
| `isConsentLoggingEnabled()`| Checks if consent logging is enabled for a user|
| `isConsentLoggingEnabledForInstanceName()`|Checks if consent logging is enabled, for a specific Tealium instance |
| `removePersistentData()`| Remove persistent data that has been previously set using `setPersistentData()`|
| `removePersistentDataForInstanceName()`| Remove persistent data that has been previously set using `setPersistentData()` for a specific Tealium instance|
| `removeRemoteCommand()` | Removes a remote command from the remote command manager |
| `removeRemoteCommandForInstanceName()` | Removes a remote command from the remote command manager, for a specific Tealium instance |
| `removeVolatileData()`| Remove volatile data that has been previously set using `setVolatileData()`|
| `removeVolatileDataForInstanceName()`| Remove volatile data that has been previously set using `setVolatileData()`, for a specific Tealium instance|
| `resetUserConsentPreferences()`|Resets the user consent status and categories of a user |
| `resetUserConsentPreferencesForInstanceName()`|Resets the user consent status and categories of a user, for a specific Tealium instance|
| `setConsentLoggingEnabled()`| Sets user&#39;s consent logging|
| `setConsentLoggingEnabledForInstanceName()`| Sets user&#39;s consent logging, for a specific Tealium instance|
| `setPersistentData()`|Set persistent data to be sent with each subsequent event or view, even between app restarts |
| `setPersistentDataForInstanceName()`|Set persistent data to be sent with each subsequent event or view, even between app restarts, for a specific Tealium instance |
| `setUserConsentCategories()`| Sets the consent categories of a user|
| `setUserConsentCategoriesForInstanceName()`| Sets the consent categories of a user, for a specific Tealium instance|
| `setUserConsentStatus()`|Sets the consent status of a user |
| `setUserConsentStatusForInstanceName()`|Sets the consent status of a user, for a specific Tealium instance |
| `setVolatileData()`| Set volatile data to be sent with each subsequent event or view until the app is terminated|
| `setVolatileDataForInstanceName()`| Set volatile data to be included with each subsequent tracking call until the app is terminated, for a specific Tealium instance |
| `trackEvent()`| Track an event with an event name and event data|
| `trackEventForInstanceName()`|Track an event when you have multiple instances of Tealium in your app, for a specific Tealium instance |
|`trackView()` | Track a view with a screen name and view data |
|`trackViewForInstanceName()` | Track a view when you have multiple instances of Tealium in your app, for a specific Tealium instance|

### `addRemoteCommand()`

Adds a remote command to the remote command manager.

```javascript
addRemoteCommand(commandID, description, callback);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `commandID` | `String` | Name of the command ID from the tag configuration | `&#34;test_command&#34;` |
| `description` | `String ` | Description of the remote command | `&#34;Firebase remote command&#34;` |
| `callback` | `Function ` | A callback function to execute once the response is received from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example) |

Example:

```javascript
Tealium.addRemoteCommand(&#34;firebase&#34;, &#34;Firebase remote command&#34;, function(payload) {

  var eventName = payload[&#34;firebase_event_name&#34;];
  var eventProperties = payload[&#34;firebase_event_properties&#34;];

  analytics.logEvent(eventName, eventProperties);
});
```

### `addRemoteCommandForInstanceName()`

Adds a remote command to the remote command manager, for a specific Tealium instance.

```javascript
addRemoteCommandForInstanceName(instanceName, commandID, description, callback);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `instanceName` | `String` | Name of the Tealium instance | `&#34;instance-2&#34;` |
| `commandID` | `String` | Name of the command ID from the tag configuration | `&#34;test_command&#34;` |
| `description` | `String ` | Description of the remote command | `&#34;Firebase remote command&#34;` |
| `callback` | `Function ` |  A callback function to execute once the response is received from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example) |

Example:

```javascript
Tealium.addRemoteCommand(&#34;instance-2&#34;, &#34;survey&#34;, &#34;Display feedback survey&#34;, function(payload) {

	var title = payload[&#34;survey_title&#34;];
	var question = payload[&#34;survey_question&#34;];

	Alert.alert(title, question, [{text: &#39;Yes&#39;, onPress: () =&gt; surveyHandler()},
								  {text: &#39;No&#39;, onPress: () =&gt; surveyHandler()}]);

});
```

### `getPersistentData()`
Gets the value for a specific key.

```javascript
Tealium.getPersistentData(key, value);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `key` | `String` | Key name of value  | `&#34;foo&#34;` |
| `value` | `Object` | JSON object of key-value pairs | `function(value) {console.log(&#34;get persistent: &#34; &#43; value);}` |


### `getPersistentDataForInstanceName()`
Get a persistent data value, for a specific Tealium instance and key. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.getPersistentDataForInstanceName(instanceName, key, value);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name  | `&#34;instance-2&#34;` |
| `key` | `String` | Key name of value  | `&#34;foo&#34;` |
| `data` | `Object` | JSON object of key-value pairs | `function(value) {console.log(&#34;get volatile: &#34; &#43; value);}` |

### `getUserConsentCategories()`
Gets the consent categories of a user. Pass in a callback to use the userConsentCategories.

```javascript
Tealium.getUserConsentCategories(userConsentCategories);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `userConsentCategories` | `Callback` | Callback function to use the user consent categories | `function (consentCategories) {console.log(&#34;categories &#39;main&#39;: &#34; &#43; consentCategories);}` |


### `getUserConsentCatgoriesForInstanceName()`
Gets the consent categories of a user, for a specific Tealium instance. Pass in a callback to use the userConsentCategories. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.getUserConsentCategoriesForInstanceName(name, userConsentCategories);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `&#34;instance-2&#34;` |
| `userConsentCategories` | `Callback` | Callback function to use the user consent categories | `function (consentCategories) {console.log(&#34;categories &#39;main&#39;: &#34; &#43; consentCategories);}` |

### `getUserConsentStatus()`
Gets the consent status of a user. Pass in a callback to use the userConsentStatus.

```javascript
Tealium.getUserConsentStatus(userConsentStatus);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `userConsentStatus` | `Callback` | Callback function to use the user consent status | `function(userConsentStatus) {console.log(&#34;consent status &#39;instance-2&#39;: &#34; &#43; userConsentStatus);}` |


### `getUserConsentStatusForInstanceName()`
Gets the consent status of a user, for a specific Tealium instance. Pass in a callback to use the userConsentStatus. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.getUserConsentStatusForInstanceName(name, userConsentStatus);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `&#34;instance-2&#34;` |
| `userConsentStatus` | `Callback` | Callback function to use the user consent status | `function(userConsentStatus) {console.log(&#34;consent status &#39;instance-2&#39;: &#34; &#43; userConsentStatus);}` |

### `getVisitorID()`
Gets the visitorID of a user. Pass in a callback to use the visitorID.

```javascript
Tealium.getVisitorID(visitorID);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `visitorID` | `Callback` | Callback function to use the visitor ID | `function (visitorID) {console.log(&#34;visitorID: &#34; &#43; visitorID);}` |


### `getVisitorIDForInstanceName()`
Gets the visitorID of a user, for a specific Tealium instance. Pass in a callback to use the visitorID. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.getVisitorIDForInstanceName(name, visitorID);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `&#34;instance-2&#34;` |
| `visitorID` | `Callback` | Callback function to use the visitor ID | `function (visitorID) {console.log(&#34;visitorID: &#34; &#43; visitorID);}` |

### `getVolatileData()`
Gets the value for the key passed in.

```javascript
Tealium.getVolatileData(key, value);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `key` | `String` | Key name of value  | `&#34;foo&#34;` |
| `value` | `Object` | JSON object of key-value pairs | `function(value) {console.log(&#34;get volatile: &#34; &#43; value);}` |


### `getVolatileDataForInstanceName()`
Get a volatile data value, for a specific Tealium instance and key. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.getVolatileDataForInstanceName(instanceName, key, value);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name  | `&#34;instance-2&#34;` |
| `key` | `String` | Key name of value  | `&#34;foo&#34;` |
| `data` | `Object` | JSON object of key-value pairs | `function(value) {console.log(&#34;get volatile: &#34; &#43; value);}` |

### `initialize()`

Initialize Tealium before calling any other method.

```javascript
initialize(account,
    profile,
    environment,
    iosDatasource,
    androidDatasource,
    instance,
    isLifecycleEnabled);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `account` | `String` | Tealium account name | `&#34;companyXYZ&#34; `|
| `profile` | `String` | Tealium profile name | `&#34;main&#34;` |
| `environment` | `String` | Tealium environment name |  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `iosDatasource` | `String` | (Optional) Tealium iOS data source key | `&#34;abc123&#34;` |
| `androidDatasource` | `String` | (Optional) Tealium Android data source key | `&#34;xyz123&#34;` |
| `instance` | `String` | Tealium instance name (default: `&#34;MAIN&#34;`) | `&#34;MAIN&#34;` |
| `isLifecycleEnabled` | `Boolean` | (Optional) To enable lifecycle tracking (default: `true`) | [`true`, `false`] |

### `initializeCustom()`

Initialize Tealium with all options before calling any other method.

```javascript
initializeCustom(account,
        profile,
        environment,
        iosDatasource,
        androidDatasource,
        instance,
        isLifecycleEnabled,
        overridePublishSettingsURL,
        overrideTagManagementURL,
        collectURL,
        enableConsentManager,
        overrideCollectDispatchURL
    );
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `account` | `String` | Tealium account name | `&#34;companyXYZ&#34; `|
| `profile` | `String` | Tealium profile name | `&#34;main&#34;` |
| `environment` | `String` | Tealium environment name |  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `iosDatasource` | `String` | (Optional) Tealium iOS data source key | `&#34;abc123&#34;` |
| `androidDatasource` | `String` | (Optional) Tealium Android data source key | `&#34;xyz123&#34;` |
| `instance` | `String` | Tealium instance name (default: `&#34;MAIN&#34;`) | `&#34;MAIN&#34;` |
| `isLifecycleEnabled` | `Boolean` | (Optional) To enable lifecycle tracking  (default: `true`) | [`true`, `false`] |
| `overridePublishSettingsURL` | `String` | The publish settings URL if overriding (default: `null`) | `null` |
| `overrideTagManagementURL` | `String` | The tag management URL if overriding (default: `null`) | `null` |
| `collectURL` | `Boolean` | To send data to the Collect endpoint if enabled (default: true) | [`true`, `false`]|
| `enableConsentManager`| `Boolean` | To enable consent management |[`true`, `false`] |
| `overrideCollectDispatchURL`| `String` | The collect URL if overriding (default: `null`) | `null` |

### `initializeWithConsentManager()`

Initialize Tealium with consent management before calling any other method.

```javascript
initializeWithConsentManager(account,
  profile,
  environment,
  iosDatasource,
  androidDatasource,
  instance,
  isLifecycleEnabled);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `account` | `String` | Tealium account name | `&#34;companyXYZ&#34; `|
| `profile` | `String` | Tealium profile name | `&#34;main&#34;` |
| `environment` | `String` | Tealium environment name |  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `iosDatasource` | `String` | (Optional) Tealium iOS data source key | `&#34;abc123&#34;` |
| `androidDatasource` | `String` | (Optional) Tealium Android data source key | `&#34;xyz123&#34;` |
| `instancee` | `String` | Tealium instance name (default: `&#34;MAIN&#34;`) | `&#34;MAIN&#34;` |
| `isLifecycleEnabled` | `Boolean` | (Optional) To enable lifecycle tracking  (default: `true`) | [`true`, `false`] |


### `isConsentLoggingEnabled()`
Checks if consent logging is enabled for a user. Pass in a callback to use the value of consent logging.

```javascript
isConsentLoggingEnabled(enabled);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `callback` | `Callback` | Checks if consent logging is enabled for a user | &#39;function (enabled) {console.log(&#34;consent logging enabled &#39;main&#39;: &#34; &#43; enabled);}&#39; |


### `isConsentLoggingEnabledForInstanceName()`

Checks if user&#39;s consent logging is enabled, for a specific Tealium instance. Pass in a callback to use the value of consent logging. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.isConsentLoggingEnabledForInstanceName(name, enabled);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `&#34;instance-2&#34;` |
| `callback` | `Callback` | Checks if consent logging is enabled for a user | &#39;function (enabled) {console.log(&#34;consent logging enabled &#39;main&#39;: &#34; &#43; enabled);}&#39; |

### `removePersistentData()`
Remove persistent data that has been previously set using `Tealium.setPersistentData()`.

```javascript
Tealium.removePersistentData(keys);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `keys` | `[String]` | Array of key names  | `[&#34;foo&#34;, &#34;bar&#34;]` |


### `removePersistentDataForInstanceName()`
Remove persistent data that has been previously set using `Tealium.setPersistentData()`, for a specific Tealium instance. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.removePersistentDataForInstanceName(instanceName, keys);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name  | `&#34;instance-2&#34;` |
| `keys` | `[String]` | Array of key names  | `[&#34;foo&#34;, &#34;bar&#34;]` |

### `removeRemoteCommand()`

Removes a remote command from the remote command manager.

```javascript
removeRemoteCommand(commandID);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `commandID ` | `String` | Name of the command ID to remove  | `&#34;test_command&#34;` |

Example:

```javascript
Tealium.removeRemoteCommand(&#34;firebase&#34;);
```

### `removeRemoteCommandForInstanceName()`

Removes a remote command from the remote command manager, for a specific Tealium instance.

```javascript
removeRemoteCommandForInstanceName(instanceName, commandID);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `instanceName` | `String` | Name of the Tealium instance | `&#34;instance-2&#34;` |
| `commandID ` | `String` | Name of the command ID to remove  | `&#34;test_command&#34;` |

Example:

```javascript
Tealium.removeRemoteCommand(&#34;instance-2&#34;, &#34;firebase&#34;);
```

### `removeVolatileData()`
Remove volatile data that has been previously set using `Tealium.setVolatileData()`.

```javascript
Tealium.removeVolatileData(keys);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `keys` | `[String]` | Array of key names  | `[&#34;foo&#34;, &#34;bar&#34;]` |


### `removeVolatileDataForInstanceName()`
Remove volatile data for provided instance names. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.removeVolatileDataForInstanceName(name, keys);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name  | `&#34;instance-2&#34;` |
| `keys` | `[String]` | Array of key names  | `[&#34;foo&#34;, &#34;bar&#34;]` |



### `resetUserConsentPreferences()`
Resets the user consent status and categories of a user.

```javascript
Tealium.resetUserConsentPreferences();
```


### `resetUserConsentPreferencesForInstanceName()`
Resets the user consent status and categories of a user, for a specific Tealium instance. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.resetUserConsentPreferencesForInstanceName(name);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `&#34;instance-2&#34;` |



### `setConsentLoggingEnabled()`
Sets consent logging for a user.

```javascript
Tealium.setConsentLoggingEnabled(enabled);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `enabled` | `boolean` | Enables consent logging for a user | [`&#34;true&#34;`, `&#34;false&#34;`] |


### `setConsentLoggingEnabledForInstanceName()`
Sets user&#39;s consent logging, for a specific Tealium instance. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.setConsentLoggingEnabledForInstanceName(name, enabled);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `&#34;instance-2&#34;` |
| `enabled` | `boolean` | Enables consent logging for a user | [`&#34;true&#34;`, `&#34;false&#34;`] |

### `setPersistentData()`
Set persistent data to be sent with each subsequent event or view, even between app restarts.

```javascript
Tealium.setPersistentData(data);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `data` | `Object` | JSON object of key-value pairs, where keys are strings and the values are either a string or array of strings | `{&#34;persistent_key2&#34; : &#34;persistent_val2&#34;}` |


### `setPersistentDataForInstanceName()`
Set persistent data to be sent with each subsequent event or view, even between app restarts, for a specific Tealium instance. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.setPersistentDataForInstanceName(instanceName, data);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name  | `&#34;instance-2&#34;` |
| `data` | `Object` | JSON object of key-value pairs, where keys are strings and the values are either a string or array of strings | `{&#34;persistent_key2&#34; : &#34;persistent_val2&#34;}` |


### `setUserConsentCategories()`
Sets the consent categories of a user. Pass in an array of Strings to set the categories.

```javascript
Tealium.setUserConsentCategories(userConsentCategories);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `userConsentCategories` | `[String]` | Array of  user consent categories | `[&#34;email&#34;, &#34;personalization&#34;]` |

### `setUserConsentCategoriesForInstanceName()`
Sets the consent ;categories of a user, for a specific Tealium instance. Pass in an array of Strings to set the categories. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.setUserConsentCategoriesForInstanceName(name, userConsentCategories);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `&#34;instance-2&#34;` |
| `userConsentCategories` | `[String]` | Array of  user consent categories | `[&#34;analytics&#34;, &#34;big_data&#34;]` |


### `setUserConsentStatus()`

Sets the consent status of a user.

```javascript
Tealium.setUserConsentStatus(userConsentStatus);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `userConsentStatus` | `int` | User consent status | [`0`, `1`, `2`, `3`] |

| Consent Status Value | Description |
| --- | --- |
| 0 | Unknown |
| 1 | Consented |
| 2 | Not Consented |
| 3 | Disabled (Objective-C only) |

### `setUserConsentStatusForInstanceName()`
Sets the consent status of a user, for a specific Tealium instance. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.setUserConsentStatusForInstanceName(name, userConsentStatus);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `&#34;instance-2&#34;` |
| `userConsentStatus` | `int` | User consent status | [`0`, `1`, `2`, `3`] |

| Consent Status Value | Description |
| --- | --- |
| 0 | Unknown |
| 1 | Consented |
| 2 | Not Consented |
| 3 | Disabled (Objective-C only) |

### `setVolatileData()`
Set volatile data to be sent with each subsequent event or view until the app is terminated, where data is a JSON object of key-value pairs where keys are strings and the values are either a string or array of strings.

```javascript
Tealium.setVolatileData(data);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `data` | `Object` | JSON object of key-value pairs, where keys are strings and the values are either a string or array of strings | `{&#34;volatile_var&#34;: &#34;volatile_val&#34;, &#34;volatile_var2&#34;: &#34;volatile_val2&#34;}` |


### `setVolatileDataForInstanceName()`
Set volatile data to be included with each subsequent tracking call until the app is terminated, for a specific Tealium instance. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.setVolatileDataForInstanceName(name, data);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Key name of value | &#34;instance-2&#34; |
| `data` | `Object` | JSON object of key-value pairs | `{&#34;foo&#34;: &#34;bar&#34;}` |

### `trackEvent()`

Track an event with an event name and event data.

```javascript
trackEvent(stringTitle, data);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `stringTitle` | `String` | Name of event (becomes the `event_name` attribute in Tealium Customer Data Hub) | `&#34;test_event&#34;` |
| `data` | `Object` | JSON object of key-value pairs | `{&#34;title&#34;: &#34;test_event&#34;, &#34;event_title&#34;: &#34;test_event&#34;, &#34;testkey&#34;: &#34;testval&#34;, &#34;anotherkey&#34;: &#34;anotherval&#34;}` |


### `trackEventForInstanceName()`

Track an event when you have multiple instances of Tealium in your app, for a specific Tealium instance.

```javascript
trackEvent(name, stringTitle, data);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Name of the Tealium instance | `&#34;instance-2&#34;` |
| `stringTitle` | `String` | Name of event (becomes the `event_name` attribute in Customer Data Hub) | `&#34;test_event_2&#34;` |
| `data` | `Object` | JSON object of key-value pairs | |


### `trackView()`

Track a view with a screen name and view data.

```javascript
trackView(screenName, data);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `stringTitle` | `String` | Name of event (becomes the `screen_title` attribute in Customer Data Hub) | `&#34;test_view&#34;` |
| `data` | `Object` | JSON object of key-value pairs | `{&#34;title&#34;: &#34;test_view&#34;, &#34;event_title&#34;: &#34;test_view&#34;, &#34;testkey&#34;: &#34;testval&#34;, &#34;anotherkey&#34;: &#34;anotherval&#34;}` |


### `trackViewForInstanceName()`

Track a view when you have multiple instances of Tealium in your app, for a specific Tealium instance.

```javascript
Tealium.trackViewForInstanceName(instanceName, screenName, data);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Name of the Tealium instance | `&#34;instance-2&#34;` |
| `stringTitle` | `String` | Name of event (becomes the `screen_title` attribute in Customer Data Hub) | `&#34;instance_2_view&#34;` |
| `data` | `Object` | (Optional) JSON object of key-value pairs | |
