---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for Xamarin.
url: https://docs.tealium.com/platforms/xamarin/api/
---
## Class: `Tealium`

The methods and constants of the `Tealium` class for the Tealium Xamarin library.

### `AddRemoteCommand()`

Adds a remote command to the remote command manager.

```csharp
void AddRemoteCommand(IRemoteCommand remoteCommand);
```

| Parameters      | Type             | Description                                                                                      |
|:----------------|:-----------------|:-------------------------------------------------------------------------------------------------|
| `remoteCommand` | `IRemoteCommand` | An implementation of the IRemoteCommand interface, supplying required remote command properties. |

Example:

```csharp
public class MyRemoteCommand : IRemoteCommand
    {
        public string CommandId => "my_remote_command";
        public string Description => "description of my remote command";
        public string Path => null;
        public string Url => null;

        public void Dispose()
        {
            //
        }

        public void HandleResponse(IRemoteCommandResponse response)
        {
            var str = response.Payload.GetValueForKey<String>("key");
            if (str == "")
            {
                // etc
            }
        }
    }

tealium.AddRemoteCommand(new MyRemoteCommand());
```

### `AddToDataLayer()`
Adds data to the persistent data storage for the given expiration.

```csharp
void AddToDataLayer(IDictionary<string, object> data, Expiry expiry);
```

| Parameters | Type | Description |
|:-----------|:-----|:------------|
| `data`     | `IDictionary<string, object>` | IDictionary of key-value pairs, where keys are strings and the values are primitives or collections |
| `expiry`   | [`Expiry`](#expiry)           | Length of time for which to persist the data|

```csharp
tealium.AddToDataLayer(new Dictionary<string, object> {
  { "user_language", lang }
}, Expiry.Forever);
```

### `ClearStoredVisitorIds()`

Clears the stored visitor IDs and generates a new one. Primarily used for legal compliance.

Visitor IDs will contiue to be stored based on the config setting `visitorIdentityKey`, if the data layer contains that key.

```csharp
tealium.ClearStoredVisitorIds();
```


<blockquote>
To avoid storing the newly reset `visitorId` with the current identity after the storage is cleared, the identity key must be previously deleted from the data layer (see [`RemoveFromDataLayer()`](#removefromdatalayer)).
</blockquote>


### ConsentCategory
The consent category values. For use with [`GetConsentCategories`](#getconsentcategories) and [`SetConsentCategories`](#setconsentcategories).

The consent categories are:

* `ConsentManager.ConsentCategory.Analytics`
* `ConsentManager.ConsentCategory.Affiliates`
* `ConsentManager.ConsentCategory.BigData`
* `ConsentManager.ConsentCategory.Cdp`
* `ConsentManager.ConsentCategory.CookieMatch`
* `ConsentManager.ConsentCategory.Crm`
* `ConsentManager.ConsentCategory.DisplayAds`
* `ConsentManager.ConsentCategory.Email`
* `ConsentManager.ConsentCategory.Engagement`
* `ConsentManager.ConsentCategory.Misc`
* `ConsentManager.ConsentCategory.Mobile`
* `ConsentManager.ConsentCategory.Monitoring`
* `ConsentManager.ConsentCategory.Personalization`
* `ConsentManager.ConsentCategory.Search`
* `ConsentManager.ConsentCategory.Social`

### ConsentStatus
The consent status values. For use with [`SetConsentStatus()`](#setconsentstatus).

| Value                                       | Description   |
|:--------------------------------------------|:--------------|
| `ConsentManager.ConsentStatus.Consented`    | Consented     |
| `ConsentManager.ConsentStatus.NotConsented` | Not Consented |
| `ConsentManager.ConsentStatus.Unknown`      | Unknown       |

### Environment

The environment is one of three default environments (Dev, QA, Prod) or any custom environment that you publish to.

| Value              | Description |
|:-------------------|:------------|
| `Environment.dev`  | Development |
| `Environment.qa`   | QA/UAT      |
| `Environment.prod` | Production  |

### Expiry

Defines the expiration of persistent or volatile data. For use with [`AddToDataLayer()`](#addtodatalayer).

| Value                 | Description                                  |
|:----------------------|:---------------------------------------------|
| `Expiry.Session`      | The length of the current active session.    |
| `Expiry.UntilRestart` | The length of time until the next restart.   |
| `Expiry.Forever`      | The length of time until the app is deleted. |


### `GetFromDataLayer()`
Retrieves the value for a specified key in the persistent data layer.

```csharp
object? GetFromDataLayer(string key);
```

| Parameters | Type     | Description                         |
|:-----------|:---------|:------------------------------------|
| `key`      | `String` | Key to retrieve from the data layer |

```csharp
string myString = (string)tealium.GetFromDataLayer("user_language");
```

### `GetConsentCategories()`
Get the list of categories that the user consented to.

```csharp
List<ConsentCategory>? GetConsentCategories();
```

Example:

```csharp
tealium.GetConsentCategories().ForEach((c) =>
{
    if (c == ConsentManager.ConsentCategory.Analytics)
    {
        // consented to Analytics
    }
});
```

### `GetConsentStatus()`
Gets the current state of the user's consent. Returns a [`ConsentStatus`](#consentstatus) value.

```csharp
ConsentStatus GetConsentStatus();
```

Example:

```csharp
switch (tealium.GetConsentStatus()) {
    case ConsentManager.ConsentStatus.Unknown:
        break;
    case ConsentManager.ConsentStatus.Consented:
        break;
    case ConsentManager.ConsentStatus.NotConsented:
        break;
}
```

### `GetVisitorId()`
Retrieves the user's visitor ID and returns in the form of a callback function.

```csharp
string? visitorId = tealium.GetVisitorId();
```

### `JoinTrace()`

Joins a trace with the specified ID. Learn more about the [Trace](https://docs.tealium.com/manage-traces/) feature in the Tealium Customer Data Hub.

```csharp
tealium.JoinTrace(id);
```

| Parameters | Type     | Description | Example    |
|:-----------|:---------|:------------|:-----------|
| `id`       | `String` | Trace ID    | `abc123xy` |

### `LeaveTrace()`

A trace remains active for the duration of the app session until the `leaveTrace()` method is called, which leaves a previously joined trace and ends the visitor session.

```csharp
tealium.LeaveTrace();
```

### `RemoveFromDataLayer()`

Remove persistent data that has been previously set using [`AddToDataLayer()`](#addtodatalayer).

```csharp
void RemoveFromDataLayer(ICollection<string> keys);
```

| Parameters | Type                  | Description             |
|:-----------|:----------------------|:------------------------|
| `keys`     | `ICollection<String>` | Collection of key names |
  
```csharp
tealium.RemoveFromDataLayer(new string[] { "key1", "key2" });
```

### `RemoveRemoteCommand()`

Removes a remote command from the remote command manager.

```csharp
void RemoveRemoteCommand(string id);
```

| Parameters | Type     | Description                      |
|:-----------|:---------|:---------------------------------|
| `id`       | `String` | Name of the command ID to remove |

```csharp
tealium.RemoveRemoteCommand("firebase");
```


### `ResetVisitorId()`

Resets the visitor ID and generates a new one.

```csharp
tealium.ResetVisitorId();
```

### `SetConsentCategories()`
Sets the list of categories that the user consented to. For use with [`ConsentCategory`](#consentcategory).

```csharp
void SetConsentCategories(List<ConsentCategory> categories);
```

| Parameters   | Type                    | Description                      |
|:-------------|:------------------------|:---------------------------------|
| `categories` | `List<ConsentCategory>` | List of user consent categories. |

```csharp
tealium.SetConsentCategories(new List<ConsentManager.ConsentCategory>()
{
    ConsentManager.ConsentCategory.DisplayAds,
    ConsentManager.ConsentCategory.Analytics
});
```

### `SetConsentExpiryListener()`
Sets a callback method to execute when the consent preferences have expired.

```csharp
void SetConsentExpiryListener(Action callback);
```

| Parameters   | Type     | Description                           |
|:-------------|:---------|:--------------------------------------|
| `callback  ` | `Action` | Code to execute when consent expires. |
  
```csharp
tealium.SetConsentExpiryListener(() =>
{
    System.Diagnostics.Debug.WriteLine("Consent Expired");
});
```

### `SetConsentStatus()`
Sets the consent status for a user. Default value is `.Unknown` until it's set.

```csharp
void SetConsentStatus(ConsentStatus status);
```

| Parameters | Type            | Description                                                              |
|:-----------|:----------------|:-------------------------------------------------------------------------|
| `status  ` | `ConsentStatus` | User consent status. See [ConsentManager.ConsentStatus](#consentstatus). |

```csharp
tealium.SetConsentStatus(ConsentManager.ConsentStatus.NotConsented);
```

### `SetVisitorServiceListener()`
Sets a callback function to execute when the visitor profile has been updated. The updated [`VisitorProfile`](#instance-ivisitorprofile) is provided in the callback response. For use when [`visitorServiceEnabled`](https://docs.tealium.com/platforms/xamarin/install/#config) is set to `true`.

Use this feature if you are licensed for Tealium AudienceStream and you want to use the visitor profile to enhance the user experience in your mobile application.

```csharp
void SetVisitorServiceListener(Action callback);
```

| Parameters   | Type     | Description                                          |
|:-------------|:---------|:-----------------------------------------------------|
| `callback  ` | `Action` | Code to execute when a visitor profile is retrieved. |
  
```csharp
tealium.SetVisitorServiceListener((visitorProfile) =>
{
    System.Diagnostics.Debug.WriteLine("Visitor Updated");
    System.Diagnostics.Debug.WriteLine($"Visitor: {visitorProfile}");
});
```

### `TerminateIntance()`

Disables the Tealium library and removes all module references.

```csharp
tealium.TerminateIntance();
```

### `Track()`

Track an event with either a `TealiumEvent` or `TealiumView` dispatch.

```csharp
tealium.Track(tealEvent);
```

| Parameters | Type    | Description          |
|:-----------|:--------|:---------------------|
| `tealEvent` | `string`| The event name, passed as the `tealium_event` attribute, and an optional event data object. |

To track events, create a [`TealiumEvent`](#class-tealiumevent) object, and pass it to the `track()` method:

```csharp
tealium.Track(new TealiumEvent("cart_add", new Dictionary<string, object> {
    { "customer_id", "abc123" }, 
    { "product_id", ["PROD123", "PROD456"] },
    { "product_price", [4.00, 6.00] }
}));
```

## Class: `TealiumConfig`

The following summarizes the properties of the `TealiumConfig` class.

| Parameters| Type| Description| Example|
|:----------|:----|:-----------|:-------|
| `account`| `String`| (Required) Tealium account name| `"companyXYZ" `|
| `profile`| `String`| (Required) Tealium profile name| `"main"`|
| `environment`| [`Environment`](#environment) | (Required) Tealium environment name| `Environment.dev`|
| `dataSource`| `String`| CDH data source key| `"abc123"`|
| `collectors`| `Collectors[]`| (Required) Sets the list of [`Collectors`](#collectors) to initialize the Tealium library with| `[Collectors.AppData]`|
| `dispatchers`| `Dispatchers[]`| (Required) Sets the list of [`Dispatchers`](#dispatchers) to initialize the Tealium library with| `[Dispatchers.Collect]`|
| `customVisitorId`| `String`| Sets a custom Visitor ID| `"ALK2398LSDKJ3289SLKJ3298SLKJ3"`|
| `memoryReportingEnabled`       | `Boolean`| Enables or disables memory reporting in the DeviceData module (default: disabled).| `true`|
| `overrideCollectDomain`           | `String`| Overrides the domain of the Tealium Collect URL. For use with [first-party domains](https://docs.tealium.com/iq-tag-management/administration/first-party-domains/manage/). | `"your-domain.com"`|
| `overrideCollectURL`           | `String`| Overrides the Tealium Collect URL to send data to a different endpoint. If using the event batching feature, also override the `overrideCollectBatchURL` property.| `"https://custom-domain.com/event"`|
| `overrideCollectBatchURL`      | `String`| Overrides the Tealium Collect batch URL to send data to a different endpoint.| `"https://custom-domain.com/batch-event"`|
| `overrideLibrarySettingsURL`   | `String`| Overrides the publish settings URL.| `"https://custom-domain.com/mobile.html"`|
| `overrideTagManagementURL`     | `String`| Overrides the default URL used by the Tag Management module. This is needed if you are self-hosting your Tealium JavaScript files.| `"https://custom-domain.com/path/env/utag.js"`|
| `deepLinkTrackingEnabled`      | `Boolean`| Enables or disables [automatic tracking of standard deep links](https://docs.tealium.com/platforms/getting-started-mobile/deep-linking/#readout), such as links to the app from Facebook or other sources, as well as QR trace.  (default: enabled)| `false`|
| `qrTraceEnabled`               | `Boolean`| Enables or disables [QR trace](https://docs.tealium.com/platforms/getting-started-mobile/trace/#how-it-works). (default: enabled)| `false`|
| `loglevel`                     | [`LogLevel`](#loglevel)                     | Sets the log level property, which controls how much information is logged (default: silent)| `LogLevel.dev`|
| `consentExpiry`                | [`ConsentExpiry`](#consentexpiry)           | Sets the expiration of the user's consent preferences. (defaults dependent upon policy)| `ConsentExpiry(90, TimeUnit.days)`|
| `consentLoggingEnabled`        | `Boolean`| Enables the [Consent Logging](https://docs.tealium.com/consent-change-event-specifications/) feature, which sends all consent status changes to Tealium Customer Data Hub for auditing purposes. (default: enabled)   | `true`|
| `consentPolicy`                | [`ConsentPolicy`](#consentpolicy)           | Sets the consent policy. For example, CCPA or GDPR. Consent manager is only enabled if this property is set.| `ConsentPolicy.gdpr`|
| `lifecycleAutotrackingEnabled` | `Boolean`| Enables or disables lifecycle auto tracking. (default: enabled)| `false`|
| `useRemoteLibrarySettings`     | `Boolean`| Enables or disables the [Mobile Publish Settings](https://docs.tealium.com/creating-a-mobile-profile/) (default: enabled) Configure the Mobile Publish Settings in Tealium iQ Tag Management, or disable the feature. | `false`|
| `visitorServiceEnabled`        | `Boolean`| Enables or disables the automatic retrieval of the Visitor Profile using the [Data Layer Enrichment API](https://docs.tealium.com/data-layer-enrichment-api/) (default: disabled)| `true`|
| `remoteCommands`               | `RemoteCommand[]`| Sets a list of [RemoteCommand](#RemoteCommand) objects to add when the instance is ready| `[{ id: "hello-world", callback: (payload) => { console.log("hello-world: " + JSON.stringify(payload)); } }]` |
| `overrideConsentCategoriesKey` | `String` | Overrides the name of the consent categories event attribute. Use this to support custom enforcement of server-side consent. Learn more about [disabling automatic enforcement of server-side consent](https://docs.tealium.com/server-side-consent-management/). (default: `consent_categories`)| `consent_categories_granted` |
| `visitorIdentityKey` | `String` | Use to support visitor switching and to specify the shared key to identify multiple users of the app. | `user_profile_id` |

### Collectors

Collectors are modules that gather supplemental information from the device and append it to the data layer before it's transmitted to the Tealium Customer Data Hub. Some collectors are included in the core library, while others are optional and installed as separate modules.

The following table lists the available collectors. Default collectors are denoted by a `*` next to the collector name.

| Collector Name  | TealiumConfig Reference   |
|:----------------|:--------------------------|
| `AppData`*      | `Collectors.AppData`      |
| `Connectivity`* | `Collectors.Connectivity` |
| `Device`        | `Collectors.Device`       |
| `Lifecycle`     | `Collectors.Lifecycle`    |

These modules are enabled or disabled using the `Collectors` property set in  [`TealiumConfig`](#class-tealiumconfig).

```csharp
TealiumConfig tealConfig = new TealiumConfig(
    // ...
    new List<Collectors> {
        Collectors.LifeCycle, Collectors.Device
    }
    // ...
);
```

### ConsentExpiry

Sets the expiration of consent preferences on the [`TealiumConfig`](#class-tealiumconfig) object.

| Parameters | Type       | Description|
|:-----------|:-----------|:-----------|
| `time`     | `Number`   | The amount of time before expiration.|
| `unit`     | `TimeUnit` | The unit of time before expiration. One of: `TimeUnit.Minutes`, `TimeUnit.Hours`, `TimeUnit.Days`, `TimeUnit.Months` |

```csharp
TealiumConfig config = new TealiumConfig(
  //...
  consentExpiry = new TimeUnit(90, TimeUnit.Days)),
  //...
);
```

### ConsentPolicy

Sets the consent policy to use on the [`TealiumConfig`](#class-tealiumconfig) object. If a consent policy is not set, the consent manager is disabled.

```csharp
TealiumConfig config = new TealiumConfig(
  //...
  consentPolicy = ConsentPolicy.GDPR,
  //...
);
```

Consent values:

* `ConsentPolicy.GDPR`
* `ConsentPolicy.CCPA`

### Dispatchers

Dispatchers are modules that send the data to a Tealium endpoint. These are set on the [`TealiumConfig`](#class-tealiumconfig) object.

```csharp
TealiumConfig tealConfig = new TealiumConfig(
    // ...
    new List<Dispatchers> {
        Dispatchers.Collect, Dispatchers.RemoteCommands
    }
    // ...
);
```

The following dispatchers are available:

* `Dispatchers.Collect`
* `Dispatchers.RemoteCommands`
* `Dispatchers.TagManagement`


<blockquote>
At least one dispatcher is required.
</blockquote>


### LogLevel

Sets the log level property, which controls how much information is logged, to one of the following values:

| Value             | Description                                                         |
|:------------------|:--------------------------------------------------------------------|
| `LogLevel.dev`    | Informational events that highlight the progress of the application |
| `LogLevel.qa`     | Debug-level events used for debugging an application                |
| `LogLevel.prod`   | Error events such as critical errors and failures                   |
| `LogLevel.silent` | No Logging (default)                                                |


## `IRemoteCommand`

An interface that defines a configured remote command.

| Value         | Description                                                 |
|:--------------|:------------------------------------------------------------|
| `CommandId`   | The unique identifier name for the RemoteCommand            |
| `Description` | (Optional) The unique identifier name for the RemoteCommand |
| `Path`        | (Optional) local file to use for mappings                   |
| `Url`         | (Optional) remote file to use for mappings                  |

## `IVisitorProfile`

(For use with [`TealiumConfig.visitorServiceEnabled`](#class-tealiumconfig).)

The visitor profile object contains visitor attributes returned from the visitor service. The `currentVisit` property contains attributes scoped to the current visit. Access each attribute value by ID using a subscript. If the attribute does not exist, `null` is returned.


| Parameters| Properties| Value|
|:----------|:----------|:-----|
| `ArraysOfBooleans` | `IDictionary<string, IList<bool>>`                 | `id: "5129", value: [true,false,true,true]`                          |
| `ArraysOfNumbers`  | `IDictionary<string, IList<double>>`               | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`               |
| `ArraysOfStrings`  | `IDictionary<string, IList<string>>`               | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]` |
| `Audiences`        | `IDictionary<string, string>`                      | `id: "tealiummobile\_demo\_103", value: "iOS Users"`                 |
| `Badges`           | `IDictionary<string, bool>`                        | `id: "2815", value: true`                                            |
| `Booleans`         | `IDictionary<string, bool>`                        | `id: "4868", value: true`                                            |
| `CurrentVisit`     | `ICurrentVisit`                                    |                                                                      |
| `Dates`            | `IDictionary<string, long>`                        | `id: "22", value: 1567120112000`                                     |
| `Numbers`          | `IDictionary<string, double>`                      | `id: "5728", value: 4.82125`                                         |
| `SetOfStrings`     | `IDictionary<string, ISet<string>>`                | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`   |
| `Strings`          | `IDictionary<string, string>                       | `id: "5380", value: "green shirts"`                                  |
| `Tallies`          | `IDictionary<string, IDictionary<string, double>>` | `"57": [["category 1": 2.0], "category 2": 1.0]]`                    |

### `ICurrentVisit`

The object that contains attributes scoped to the current visit.

| Parameters| Properties| Value|
|:----------|:----------|:-----|
| `ArraysOfBooleans` | `IDictionary<string, IList<bool>>`                 | `id: "5129", value: [true,false,true,true]`                          |
| `ArraysOfNumbers`  | `IDictionary<string, IList<double>>`               | `id: "57", value: [4.82125, 16.8, 0.5714285714285714]`               |
| `ArraysOfStrings`  | `IDictionary<string, IList<string>>`               | `id: "5213", value: ["green shirts", "green shirts", "blue shirts"]` |
| `Booleans`         | `IDictionary<string, bool>`                        | `id: "4868", value: true`                                            |
| `Dates`            | `IDictionary<string, long>`                        | `id: "22", value: 1567120112000`                                     |
| `Numbers`          | `IDictionary<string, double>`                      | `id: "5728", value: 4.82125`                                         |
| `SetOfStrings`     | `IDictionary<string, ISet<string>>`                | `id: "5211", value: ["green shirts", "red shirts", "blue shirts"]`   |
| `Strings`          | `IDictionary<string, string>                       | `id: "5380", value: "green shirts"`                                  |
| `Tallies`          | `IDictionary<string, IDictionary<string, double>>` | `"57": [["category 1": 2.0], "category 2": 1.0]]`                    |
| `TotalEventCount`  | `int`                                              | `42`                                                                 |
| `CreatedAt`        | `long`                                             | `1638236024`                                                         |

## Interface: `TealiumDispatch`

An interface that defines the type of dispatch to be tracked. The following classes implement `TealiumDispatch`:

### Class: `TealiumEvent`

To track a user's interaction with a screen or a screen view, pass an instance of `TealiumEvent(tealiumEvent, dataLayer)` to the [`Track()`](#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```csharp
tealium.Track(new TealiumEvent("tealiumEvent", new Dictionary<string, object> {
    eventData
}));
```

| Parameters  | Type    | Description      | 
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | The event name, passed as the tealium_event attribute.  |
| `eventData` | `Dictionary<string, object>` | (Optional) Data to be sent with the event in key-value format. | 

Example:

```csharp
tealium.Track(new TealiumEvent("cart_add", new Dictionary<string, object> {
    { "customer_id", "abc123" }, 
    { "product_id", ["PROD123", "PROD456"] },
    { "product_price", [4.00, 6.00] }
}));
```

### Class: `TealiumView`

To track screen views, pass an instance of `TealiumView(tealiumEvent, dataLayer)` to the [`Track()`](#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```csharp
tealium.Track(new TealiumView("tealiumEvent", new Dictionary<string, object> {
    eventData
}));
```

| Parameters  | Type    | Description      | 
|:------------|:--------|:-----------------|
| `tealiumEvent`  | `string`| The event name, passed as the `tealium_event` attribute.          | 
| `eventData` | `Dictionary<string, object>` | (Optional) Data to be sent with the event in key-value format. | 

Example:

```csharp
tealium.Track(new TealiumView("purchase", new Dictionary<string, object> {
    { "customer_id", "abc123" },
    { "order_total", 10.00 },
    { "product_id", ["PROD123", "PROD456"] },
    { "order_id", "0123456789" }
}));
```
