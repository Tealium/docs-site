---
title: Tealium
description: The Tealium class serves as the main API entry point for all modules.
url: https://docs.tealium.com/platforms/nativescript/api/tealium/
---

## Class: `Tealium`

The following summarizes the commonly used methods and properties of the `Tealium` class for the NativeScript plugin.

| Method/Property | Description |
| ----- | ------ |
| [`addRemoteCommand()`](#addremotecommand)| Adds a remote command to the remote command manager |
| [`addData()`](#adddata)| Adds data to persistent data storage |
| [`consentCategories`](#consentcategories)| Gets or sets the consent categories of a user |
| [`consentStatus`](#consentstatus)| Gets or sets the consent status of a user |
| [`getData()`](#getdata)| Retrieves data from the data layer |
| [`gatherTrackData()`](#gathertrackdata)| Gathers data from all collectors and data layer |
| [`initialize()`](#initialize) | Initializes Tealium with configuration parameters |
| [`joinTrace()`](#jointrace)| Joins a trace with the given ID |
| [`leaveTrace()`](#leavetrace)| Leaves active trace session |
| [`removeData()`](#removedata)| Remove persistent data that has been previously set using `addData()`|
| [`removeRemoteCommand()`](#removeremotecommand) | Removes a remote command from the remote command manager |
| [`removeVisitorServiceListener()`](#removevisitorservicelistener)| Removes the visitor service listener/callback |
| [`setVisitorServiceListener()`](#setvisitorservicelistener)| Defines the visitor service listener/callback |
| [`terminateInstance()`](#terminateinstance)| Disables the Tealium library and removes all module references |
| [`track()`](#track)| Track an event or screen view |
| [`visitorId`](#visitorid) | Gets the current visitor ID |

### `addRemoteCommand()`

Adds a remote command to the remote command manager.

```javascript
Tealium.addRemoteCommand(id, callback);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `id` | `String` | Name of the remote command ID from the tag configuration | `"test_command"` |
| `callback` | `Function ` | A callback function to execute once the response is received from the remote command. The callback returns a payload of key-value pairs from the tag mappings. | (see example) |

Example:

```javascript
Tealium.addRemoteCommand('mycommand', (result: any): void => {
	console.log(result["payload"]["command_id"]);            // logs "mycommand"
	console.log(result["payload"]["my_remote_command_key"]); // logs value for key "my_remote_command_key"
});
```

### `addData()`

Adds data to the persistent data storage for the given [expiration time](https://docs.tealium.com/platforms/nativescript/api/tealium-config/#expiry).

```javascript
Tealium.addData(data, expiry);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `data` | `Object` | Map of key-value pairs, where keys are strings and the values are either a string or array of strings | `{"persistent_key2" : "persistent_val2"}` |
| `expiry` | [`Expiry`](https://docs.tealium.com/platforms/nativescript/api/tealium-config/#expiry) | Length of time for which to persist the data | `Expiry.forever` |

Example:

```javascript
let data: Map<string, any> = new Map([['test_session_data', 'test']]);
data.set('my_test_value', 1);
data['my_test_value'] = 1;
Tealium.addData(data, Expiry.session);
```

#### `Expiry`

Defines the expiration time for setting a property that expires.

The following expiry options are available:

| Value | Description |
| :-- | :-- |
| `Expiry.session` (default)| Expires at the end of the current session |
| `Expiry.forever` | Never expires while the app is installed |
| `Expiry.untilRestart` | Expires when device is restarted |

### `consentCategories`

Gets or sets the user's consent categories.

To set the user's consent categories:

```javascript
Tealium.consentCategories = categories
```

To get the user's consent categories:  
```javascript
let categories = Tealium.consentCategories
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `categories` | `ConsentCategories[]` | Array of  user consent categories | `[ConsentCategories.email, ConsentCategories.personalization]` |

Example:

```javascript
Tealium.consentCategories = [ConsentCategories.analytics, ConsentCategories.email];
```

The following consent categories are available:

| Value | Description |
| --- | --- |
| `analytics` | Analytics |
| `affiliates` | Affiliates |
| `displayAds` | Display Ads |
| `email` | Email |
| `personalization` | Personalization |
| `search` | Search |
| `social` | Social |
| `bigData` | Big Data |
| `mobile` | Mobile |
| `engagement` | Engagement |
| `monitoring` | Monitoring |
| `crm` | CRM |
| `cdp` | CDP |
| `cookieMatch` | Cookie Match |
| `misc` | Misc |


### `consentStatus`

Gets or sets the user's consent status. Default is `.unknown` until changed.

To set the user's consent status:  
```javascript
Tealium.consentStatus = status;
```

To get the user's consent status:  
```javascript
let status = Tealium.consentStatus
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `status` | `ConsentStatus` | User consent status | `ConsentStatus.consented` |

Example:

```javascript
Tealium.consentStatus = ConsentStatus.consented;
```

The following consent status are available:

| Value | Description |
| --- | --- |
| `.consented` | Consented |
| `.notConsented` | Not Consented |
| `.unknown` | Unknown |


### `getData()`
Retrieves data from the data layer as `any` type.

```javascript
let data = Tealium.getData(key);
```
| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `key` | `String` | The key of the data to retrieve | `"KEY"` |

```javascript
let data: Tealium.getData("KEY")
```

### `initialize()`

Initialize Tealium before calling any other method.

```javascript
Tealium.initialize(config);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `config` | [`TealiumConfig`](https://docs.tealium.com/platforms/nativescript/api/tealium-config/#tealiumconfig) | Tealium configuration parameters | (see example) |

Example:

```javascript
let config: TealiumConfig =
{
	account: 'ACCOUNT',
	profile: 'PROFILE',
	environment: TealiumEnvironment.dev,
	dispatchers: [Dispatchers.Collect,
	 			  Dispatchers.TagManagement,
	  			Dispatchers.RemoteCommands],
	collectors: [Collectors.AppData,
				 Collectors.DeviceData,
				 Collectors.Lifecycle,
				 Collectors.Connectivity],
	consentLoggingEnabled: true,
	consentPolicy: ConsentPolicy.gdpr,
	visitorServiceEnabled: true
};

Tealium.initialize(config);
```

### `joinTrace()`

Joins a trace with the specified ID. Learn more about the [Trace](https://docs.tealium.com/manage-traces/) feature in the Tealium Customer Data Hub.

```javascript
Tealium.joinTrace(id);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `id` | `String` | Trace ID retrieved from the data source key | `abc123xy` |

Example:

```javascript
Tealium.joinTrace("abc123xy");
```

### `leaveTrace()`

A trace remains active for the duration of the app session until the `leaveTrace()` method is called, which leaves a previously joined trace and ends the visitor session.

```javascript
Tealium.leaveTrace();
```


### `removeData()`
Remove persistent data that has been previously set using `Tealium.addData()`.

```javascript
Tealium.removeData(keys);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `keys` | `String[]` | Array of key names  | `["foo", "bar"]` |

Example:

```javascript
Tealium.removeData(["foo", "bar"]);
```

### `gatherTrackData()`
Gathers all data from all collectors and data layer.

Example:
```javascript
Tealium.gatherTrackData((response: Map<string, any>): void => {				
	console.log(response);
});
```

### `removeRemoteCommand()`

Removes a remote command from the remote command manager.

```javascript
Tealium.removeRemoteCommand(id);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `id ` | `String` | Name of the command ID to remove  | `"test_command"` |

Example:

```javascript
Tealium.removeRemoteCommand("test_command");
```

### `setVisitorServiceListener()`
Defines a callback to execute when the visitor profile has been updated. The updated [`VisitorProfile`](https://docs.tealium.com/platforms/nativescript/api/tealium-config/#visitorprofile) is provided in the callback response.

The VisitorService module implements the [Data Layer Enrichment](https://docs.tealium.com/enable-data-layer-enrichment/) feature of the Tealium Customer Data Hub.

Usage of this module is recommended if you are licensed for Tealium AudienceStream and you want to use the visitor profile to enhance the user experience in your mobile application. If you are not licensed for AudienceStream, usage of this module is not recommended as no visitor profile is returned.

```javascript
Tealium.setVisitorServiceListener(callback);
```

| Parameters | Type | Description | Example |
| --- | --- | --- | --- |
| `callback` | `Function` | Code to execute once the updated visitor profile is returned | (see example) |

The following example logs the visitor's audiences and badges to the console:  

```javascript
Tealium.setVisitorServiceListener(profile => {
    console.log(profile["audiences"]);
    console.log(profile["badges"]);
});
```

### `terminateInstance()`

Disables the Tealium library and removes all module references. Re-enable by creating a new Tealium instance if required.

```javascript
Tealium.terminateInstance();
```

### `track()`

Tracks a screen view or event with optional associated data.

```
tealium?.track(tealEvent)
```

| Parameters | Type  | Description | 
|:-----------|:------|:------------|
| `tealEvent` | string | [TealiumDispatch](https://docs.tealium.com/platforms/nativescript/api/tealium-config/#dispatchers) with the event name, passed as the `tealium_event` attribute, and an optional event data object. |

To track events, pass an instance of [`TealiumEvent`](#class-tealiumevent) to the `track()` method:

```javascript
let tealEvent = new TealiumEvent(
	"cart_add", 
	new Map([
		[
			"customer_id": "abc123", 
			"product_id": ["PROD123", "PROD456"], 
			"product_price": [4.00, 6.00]
		]
	])
);
Tealium.track(tealEvent);
```

### `visitorId`

Gets the current visitor ID.

```javascript
let visitorId = Tealium.visitorId;
```

## Interface: `TealiumDispatch`

An interface that defines the type of dispatch to be tracked. The following classes implement `TealiumDispatch`:

### Class: `TealiumEvent`

To track a user's interaction with a screen or a screen view, pass an instance of `TealiumEvent(tealiumEvent, dataLayer)` to the [`Track()`](#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```javascript
let tealEvent = new TealiumEvent(tealiumEvent, eventData);
Tealium.track(tealEvent);
```

| Parameters  | Type    | Description      | 
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | The event name, passed as the `tealium_event` attribute  |
| `eventData` | `<string, object>` | (Optional) Data to be sent with the event in key-value format. | 

Example:

```javascript
let tealEvent = new TealiumEvent(
	"cart_add", 
	new Map([
		[
			"customer_id": "abc123", 
			"product_id": ["PROD123", "PROD456"], 
			"product_price": [4.00, 6.00]
		]
	)
);
Tealium.track(tealEvent);
```

### Class: `TealiumView`

To track screen views, pass an instance of `TealiumView(tealiumEvent, dataLayer)` to the [`Track()`](#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```javascript
let screenView = new TealiumEvent(tealiumEvent, eventData);
Tealium.track(screenView);
```

| Parameters  | Type    | Description      | 
|:------------|:--------|:-----------------|
| `tealiumEvent`  | `string`| The event name, passed as the `tealium_event` attribute.          | 
| `eventData` | `Dictionary<string, object>` | (Optional) Data to be sent with the event in key-value format. | 

Example:

```javascript
let screenView = new TealiumView(
	'purchase', 
	new Map([
		[
			'customer_id', 'abc123', 
			'order_total', 10.00, 
			'product_id', ["PROD123", "PROD456"], 
			'order_id': "0123456789"
		]
	])
);
Tealium.track(screenView);
```