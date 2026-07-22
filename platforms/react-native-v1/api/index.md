---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for React Native.
url: https://docs.tealium.com/platforms/react-native-v1/api/
---

<blockquote>
This is the previous version (1.x) of Tealium for React Native.  
For the current version, see [Tealium for React Native 2.x](https://docs.tealium.com/platforms/react-native/).
</blockquote>


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
| `setConsentLoggingEnabled()`| Sets user's consent logging|
| `setConsentLoggingEnabledForInstanceName()`| Sets user's consent logging, for a specific Tealium instance|
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
| `commandID` | `String` | Name of the command ID from the tag configuration | `"test_command"` |
| `description` | `String ` | Description of the remote command | `"Firebase remote command"` |
| `callback` | `Function ` | A callback function to execute once the response is received from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example) |

Example:

```javascript
Tealium.addRemoteCommand("firebase", "Firebase remote command", function(payload) {

  var eventName = payload["firebase_event_name"];
  var eventProperties = payload["firebase_event_properties"];

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
| `instanceName` | `String` | Name of the Tealium instance | `"instance-2"` |
| `commandID` | `String` | Name of the command ID from the tag configuration | `"test_command"` |
| `description` | `String ` | Description of the remote command | `"Firebase remote command"` |
| `callback` | `Function ` |  A callback function to execute once the response is received from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example) |

Example:

```javascript
Tealium.addRemoteCommand("instance-2", "survey", "Display feedback survey", function(payload) {

	var title = payload["survey_title"];
	var question = payload["survey_question"];

	Alert.alert(title, question, [{text: 'Yes', onPress: () => surveyHandler()},
								  {text: 'No', onPress: () => surveyHandler()}]);

});
```

### `getPersistentData()`
Gets the value for a specific key.

```javascript
Tealium.getPersistentData(key, value);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `key` | `String` | Key name of value  | `"foo"` |
| `value` | `Object` | JSON object of key-value pairs | `function(value) {console.log("get persistent: " + value);}` |


### `getPersistentDataForInstanceName()`
Get a persistent data value, for a specific Tealium instance and key. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.getPersistentDataForInstanceName(instanceName, key, value);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name  | `"instance-2"` |
| `key` | `String` | Key name of value  | `"foo"` |
| `data` | `Object` | JSON object of key-value pairs | `function(value) {console.log("get volatile: " + value);}` |

### `getUserConsentCategories()`
Gets the consent categories of a user. Pass in a callback to use the userConsentCategories.

```javascript
Tealium.getUserConsentCategories(userConsentCategories);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `userConsentCategories` | `Callback` | Callback function to use the user consent categories | `function (consentCategories) {console.log("categories 'main': " + consentCategories);}` |


### `getUserConsentCatgoriesForInstanceName()`
Gets the consent categories of a user, for a specific Tealium instance. Pass in a callback to use the userConsentCategories. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.getUserConsentCategoriesForInstanceName(name, userConsentCategories);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `"instance-2"` |
| `userConsentCategories` | `Callback` | Callback function to use the user consent categories | `function (consentCategories) {console.log("categories 'main': " + consentCategories);}` |

### `getUserConsentStatus()`
Gets the consent status of a user. Pass in a callback to use the userConsentStatus.

```javascript
Tealium.getUserConsentStatus(userConsentStatus);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `userConsentStatus` | `Callback` | Callback function to use the user consent status | `function(userConsentStatus) {console.log("consent status 'instance-2': " + userConsentStatus);}` |


### `getUserConsentStatusForInstanceName()`
Gets the consent status of a user, for a specific Tealium instance. Pass in a callback to use the userConsentStatus. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.getUserConsentStatusForInstanceName(name, userConsentStatus);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `"instance-2"` |
| `userConsentStatus` | `Callback` | Callback function to use the user consent status | `function(userConsentStatus) {console.log("consent status 'instance-2': " + userConsentStatus);}` |

### `getVisitorID()`
Gets the visitorID of a user. Pass in a callback to use the visitorID.

```javascript
Tealium.getVisitorID(visitorID);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `visitorID` | `Callback` | Callback function to use the visitor ID | `function (visitorID) {console.log("visitorID: " + visitorID);}` |


### `getVisitorIDForInstanceName()`
Gets the visitorID of a user, for a specific Tealium instance. Pass in a callback to use the visitorID. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.getVisitorIDForInstanceName(name, visitorID);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `"instance-2"` |
| `visitorID` | `Callback` | Callback function to use the visitor ID | `function (visitorID) {console.log("visitorID: " + visitorID);}` |

### `getVolatileData()`
Gets the value for the key passed in.

```javascript
Tealium.getVolatileData(key, value);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `key` | `String` | Key name of value  | `"foo"` |
| `value` | `Object` | JSON object of key-value pairs | `function(value) {console.log("get volatile: " + value);}` |


### `getVolatileDataForInstanceName()`
Get a volatile data value, for a specific Tealium instance and key. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.getVolatileDataForInstanceName(instanceName, key, value);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name  | `"instance-2"` |
| `key` | `String` | Key name of value  | `"foo"` |
| `data` | `Object` | JSON object of key-value pairs | `function(value) {console.log("get volatile: " + value);}` |

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
| `account` | `String` | Tealium account name | `"companyXYZ" `|
| `profile` | `String` | Tealium profile name | `"main"` |
| `environment` | `String` | Tealium environment name |  [`"dev"`, `"qa"`, `"prod"`] |
| `iosDatasource` | `String` | (Optional) Tealium iOS data source key | `"abc123"` |
| `androidDatasource` | `String` | (Optional) Tealium Android data source key | `"xyz123"` |
| `instance` | `String` | Tealium instance name (default: `"MAIN"`) | `"MAIN"` |
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
| `account` | `String` | Tealium account name | `"companyXYZ" `|
| `profile` | `String` | Tealium profile name | `"main"` |
| `environment` | `String` | Tealium environment name |  [`"dev"`, `"qa"`, `"prod"`] |
| `iosDatasource` | `String` | (Optional) Tealium iOS data source key | `"abc123"` |
| `androidDatasource` | `String` | (Optional) Tealium Android data source key | `"xyz123"` |
| `instance` | `String` | Tealium instance name (default: `"MAIN"`) | `"MAIN"` |
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
| `account` | `String` | Tealium account name | `"companyXYZ" `|
| `profile` | `String` | Tealium profile name | `"main"` |
| `environment` | `String` | Tealium environment name |  [`"dev"`, `"qa"`, `"prod"`] |
| `iosDatasource` | `String` | (Optional) Tealium iOS data source key | `"abc123"` |
| `androidDatasource` | `String` | (Optional) Tealium Android data source key | `"xyz123"` |
| `instancee` | `String` | Tealium instance name (default: `"MAIN"`) | `"MAIN"` |
| `isLifecycleEnabled` | `Boolean` | (Optional) To enable lifecycle tracking  (default: `true`) | [`true`, `false`] |


### `isConsentLoggingEnabled()`
Checks if consent logging is enabled for a user. Pass in a callback to use the value of consent logging.

```javascript
isConsentLoggingEnabled(enabled);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `callback` | `Callback` | Checks if consent logging is enabled for a user | 'function (enabled) {console.log("consent logging enabled 'main': " + enabled);}' |


### `isConsentLoggingEnabledForInstanceName()`

Checks if user's consent logging is enabled, for a specific Tealium instance. Pass in a callback to use the value of consent logging. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.isConsentLoggingEnabledForInstanceName(name, enabled);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `"instance-2"` |
| `callback` | `Callback` | Checks if consent logging is enabled for a user | 'function (enabled) {console.log("consent logging enabled 'main': " + enabled);}' |

### `removePersistentData()`
Remove persistent data that has been previously set using `Tealium.setPersistentData()`.

```javascript
Tealium.removePersistentData(keys);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `keys` | `[String]` | Array of key names  | `["foo", "bar"]` |


### `removePersistentDataForInstanceName()`
Remove persistent data that has been previously set using `Tealium.setPersistentData()`, for a specific Tealium instance. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.removePersistentDataForInstanceName(instanceName, keys);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name  | `"instance-2"` |
| `keys` | `[String]` | Array of key names  | `["foo", "bar"]` |

### `removeRemoteCommand()`

Removes a remote command from the remote command manager.

```javascript
removeRemoteCommand(commandID);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `commandID ` | `String` | Name of the command ID to remove  | `"test_command"` |

Example:

```javascript
Tealium.removeRemoteCommand("firebase");
```

### `removeRemoteCommandForInstanceName()`

Removes a remote command from the remote command manager, for a specific Tealium instance.

```javascript
removeRemoteCommandForInstanceName(instanceName, commandID);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `instanceName` | `String` | Name of the Tealium instance | `"instance-2"` |
| `commandID ` | `String` | Name of the command ID to remove  | `"test_command"` |

Example:

```javascript
Tealium.removeRemoteCommand("instance-2", "firebase");
```

### `removeVolatileData()`
Remove volatile data that has been previously set using `Tealium.setVolatileData()`.

```javascript
Tealium.removeVolatileData(keys);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `keys` | `[String]` | Array of key names  | `["foo", "bar"]` |


### `removeVolatileDataForInstanceName()`
Remove volatile data for provided instance names. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.removeVolatileDataForInstanceName(name, keys);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name  | `"instance-2"` |
| `keys` | `[String]` | Array of key names  | `["foo", "bar"]` |



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
| `name` | `String` | Instance name | `"instance-2"` |



### `setConsentLoggingEnabled()`
Sets consent logging for a user.

```javascript
Tealium.setConsentLoggingEnabled(enabled);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `enabled` | `boolean` | Enables consent logging for a user | [`"true"`, `"false"`] |


### `setConsentLoggingEnabledForInstanceName()`
Sets user's consent logging, for a specific Tealium instance. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.setConsentLoggingEnabledForInstanceName(name, enabled);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `"instance-2"` |
| `enabled` | `boolean` | Enables consent logging for a user | [`"true"`, `"false"`] |

### `setPersistentData()`
Set persistent data to be sent with each subsequent event or view, even between app restarts.

```javascript
Tealium.setPersistentData(data);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `data` | `Object` | JSON object of key-value pairs, where keys are strings and the values are either a string or array of strings | `{"persistent_key2" : "persistent_val2"}` |


### `setPersistentDataForInstanceName()`
Set persistent data to be sent with each subsequent event or view, even between app restarts, for a specific Tealium instance. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.setPersistentDataForInstanceName(instanceName, data);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name  | `"instance-2"` |
| `data` | `Object` | JSON object of key-value pairs, where keys are strings and the values are either a string or array of strings | `{"persistent_key2" : "persistent_val2"}` |


### `setUserConsentCategories()`
Sets the consent categories of a user. Pass in an array of Strings to set the categories.

```javascript
Tealium.setUserConsentCategories(userConsentCategories);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `userConsentCategories` | `[String]` | Array of  user consent categories | `["email", "personalization"]` |

### `setUserConsentCategoriesForInstanceName()`
Sets the consent ;categories of a user, for a specific Tealium instance. Pass in an array of Strings to set the categories. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.setUserConsentCategoriesForInstanceName(name, userConsentCategories);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Instance name | `"instance-2"` |
| `userConsentCategories` | `[String]` | Array of  user consent categories | `["analytics", "big_data"]` |


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
| `name` | `String` | Instance name | `"instance-2"` |
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
| `data` | `Object` | JSON object of key-value pairs, where keys are strings and the values are either a string or array of strings | `{"volatile_var": "volatile_val", "volatile_var2": "volatile_val2"}` |


### `setVolatileDataForInstanceName()`
Set volatile data to be included with each subsequent tracking call until the app is terminated, for a specific Tealium instance. For use if you have multiple instances of Tealium in your app.

```javascript
Tealium.setVolatileDataForInstanceName(name, data);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Key name of value | "instance-2" |
| `data` | `Object` | JSON object of key-value pairs | `{"foo": "bar"}` |

### `trackEvent()`

Track an event with an event name and event data.

```javascript
trackEvent(stringTitle, data);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `stringTitle` | `String` | Name of event (becomes the `event_name` attribute in Tealium Customer Data Hub) | `"test_event"` |
| `data` | `Object` | JSON object of key-value pairs | `{"title": "test_event", "event_title": "test_event", "testkey": "testval", "anotherkey": "anotherval"}` |


### `trackEventForInstanceName()`

Track an event when you have multiple instances of Tealium in your app, for a specific Tealium instance.

```javascript
trackEvent(name, stringTitle, data);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Name of the Tealium instance | `"instance-2"` |
| `stringTitle` | `String` | Name of event (becomes the `event_name` attribute in Customer Data Hub) | `"test_event_2"` |
| `data` | `Object` | JSON object of key-value pairs | |


### `trackView()`

Track a view with a screen name and view data.

```javascript
trackView(screenName, data);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `stringTitle` | `String` | Name of event (becomes the `screen_title` attribute in Customer Data Hub) | `"test_view"` |
| `data` | `Object` | JSON object of key-value pairs | `{"title": "test_view", "event_title": "test_view", "testkey": "testval", "anotherkey": "anotherval"}` |


### `trackViewForInstanceName()`

Track a view when you have multiple instances of Tealium in your app, for a specific Tealium instance.

```javascript
Tealium.trackViewForInstanceName(instanceName, screenName, data);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `name` | `String` | Name of the Tealium instance | `"instance-2"` |
| `stringTitle` | `String` | Name of event (becomes the `screen_title` attribute in Customer Data Hub) | `"instance_2_view"` |
| `data` | `Object` | (Optional) JSON object of key-value pairs | |
