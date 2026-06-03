---
title: API Reference
description: Reference guide for classes and methods provided by Tealium for .NET MAUI.
url: https://docs.tealium.com/platforms/dotnet-maui/api/
---
## Class: `Tealium`

The methods and constants of the `Tealium` class for the Tealium .NET MAUI library.

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
        public string CommandId =&gt; &#34;my_remote_command&#34;;
        public string Description =&gt; &#34;description of my remote command&#34;;
        public string Path =&gt; null;
        public string Url =&gt; null;

        public void Dispose()
        {
            //
        }

        public void HandleResponse(IRemoteCommandResponse response)
        {
            var str = response.Payload.GetValueForKey&lt;String&gt;(&#34;key&#34;);
            if (str == &#34;&#34;)
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
void AddToDataLayer(IDictionary&lt;string, object&gt; data, Expiry expiry);
```

| Parameters | Type | Description |
|:-----------|:-----|:------------|
| `data`     | `IDictionary&lt;string, object&gt;` | IDictionary of key-value pairs, where keys are strings and the values are primitives or collections |
| `expiry`   | [`Expiry`](#expiry)           | Length of time for which to persist the data|

```csharp
tealium.AddToDataLayer(new Dictionary&lt;string, object&gt; {
  { &#34;user_language&#34;, lang }
}, Expiry.Forever);
```

### `ClearStoredVisitorIds()`

Clears the stored visitor IDs and generates a new one. Primarily used for legal compliance.

Visitor IDs will continue to be stored based on the config setting `visitorIdentityKey`, if the data layer contains that key.

```csharp
tealium.ClearStoredVisitorIds();
```

To avoid storing the newly reset `visitorId` with the current identity after the storage is cleared, the identity key must be previously deleted from the data layer (see [`RemoveFromDataLayer()`](#removefromdatalayer)).

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

### `GatherTrackData()`

Gathers all track data from Collectors and data layer.

```csharp
GatherTrackData(callback);
```

| Parameters | Type       | Description                                          | Example       |
|:-----------|:-----------|:-----------------------------------------------------|:--------------|
| `callback` | `Function` | A Callback function to use the retrieved value for key. The callback returns a JSON object. | (see example) |

Example:

```csharp
tealium.GatherTrackData(data =&gt; {
    foreach (var entry in data)
    {
        System.Diagnostics.Debug.WriteLine($&#34;key ({entry.Key}) - value: {Stringify(entry.Value)}&#34;);
    }
});
```

### `GetFromDataLayer()`

Retrieves the value for a specified key in the persistent data layer.

```csharp
object? GetFromDataLayer(string key);
```

| Parameters | Type     | Description                         |
|:-----------|:---------|:------------------------------------|
| `key`      | `String` | Key to retrieve from the data layer |

```csharp
string myString = (string)tealium.GetFromDataLayer(&#34;user_language&#34;);
```

### `GetConsentCategories()`

Get the list of categories that the user consented to.

```csharp
List&lt;ConsentCategory&gt;? GetConsentCategories();
```

Example:

```csharp
tealium.GetConsentCategories().ForEach((c) =&gt;
{
    if (c == ConsentManager.ConsentCategory.Analytics)
    {
        // consented to Analytics
    }
});
```

### `GetConsentStatus()`

Gets the current state of the user&#39;s consent. Returns a [`ConsentStatus`](#consentstatus) value.

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

Retrieves the user&#39;s visitor ID and returns in the form of a callback function.

```csharp
string? visitorId = tealium.GetVisitorId();
```

### `JoinTrace()`

Joins a trace with the specified ID. Learn more about the [Trace]() feature in the Tealium Customer Data Hub.

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
void RemoveFromDataLayer(ICollection&lt;string&gt; keys);
```

| Parameters | Type                  | Description             |
|:-----------|:----------------------|:------------------------|
| `keys`     | `ICollection&lt;String&gt;` | Collection of key names |
  
```csharp
tealium.RemoveFromDataLayer(new string[] { &#34;key1&#34;, &#34;key2&#34; });
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
tealium.RemoveRemoteCommand(&#34;firebase&#34;);
```

### `ResetVisitorId()`

Resets the visitor ID and generates a new one.

```csharp
tealium.ResetVisitorId();
```

### `SetConsentCategories()`

Sets the list of categories that the user consented to. For use with [`ConsentCategory`](#consentcategory).

```csharp
void SetConsentCategories(List&lt;ConsentCategory&gt; categories);
```

| Parameters   | Type                    | Description                      |
|:-------------|:------------------------|:---------------------------------|
| `categories` | `List&lt;ConsentCategory&gt;` | List of user consent categories. |

```csharp
tealium.SetConsentCategories(new List&lt;ConsentManager.ConsentCategory&gt;()
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
tealium.SetConsentExpiryListener(() =&gt;
{
    System.Diagnostics.Debug.WriteLine(&#34;Consent Expired&#34;);
});
```

### `SetConsentStatus()`

Sets the consent status for a user. Default value is `.Unknown` until it&#39;s set.

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

Sets a callback function to execute when the visitor profile has been updated. The updated [`VisitorProfile`](#instance-ivisitorprofile) is provided in the callback response. For use when [`visitorServiceEnabled`](/platforms/dotnet-maui/install/#config) is set to `true`.

Use this feature if you are licensed for Tealium AudienceStream and you want to use the visitor profile to enhance the user experience in your mobile application.

```csharp
void SetVisitorServiceListener(Action callback);
```

| Parameters   | Type     | Description                                          |
|:-------------|:---------|:-----------------------------------------------------|
| `callback  ` | `Action` | Code to execute when a visitor profile is retrieved. |
  
```csharp
tealium.SetVisitorServiceListener((visitorProfile) =&gt;
{
    System.Diagnostics.Debug.WriteLine(&#34;Visitor Updated&#34;);
    System.Diagnostics.Debug.WriteLine($&#34;Visitor: {visitorProfile}&#34;);
});
```

### `TerminateIntance()`

Disables the Tealium library and removes all module references.

```csharp
tealium.TerminateIntance();
```

### `Track()`

Tracks a screen view or event with optional event data.

```csharp
tealium.Track(tealiumEvent);
```

| Parameters | Type    | Description          |
|:-----------|:--------|:---------------------|
| `tealiumEvent` | `TealiumView` or `TealiumEvent`| A dispatch object with the name of event and optional data to be sent with the event in key-value format. |

To track events, pass an instance of [`TealiumView`](#class-tealiumview) or [`TealiumEvent`](#class-tealiumevent) to the `track()` method:

```csharp
tealium.Track(new TealiumEvent(&#34;cart_add&#34;, new Dictionary&lt;string, object&gt; {
    { &#34;customer_id&#34;, &#34;abc123&#34; }, 
    { &#34;product_id&#34;, new[] {&#34;PROD123&#34;, &#34;PROD456&#34;} },
    { &#34;product_price&#34;, new[] {4.00, 6.00} }
}));
```

## Class: `TealiumConfig`

The following summarizes the properties of the `TealiumConfig` class.

| Parameters| Type| Description| Example|
|:----------|:----|:-----------|:-------|
| `account`| `String`| (Required) Tealium account name| `&#34;companyXYZ&#34; `|
| `profile`| `String`| (Required) Tealium profile name| `&#34;main&#34;`|
| `environment`| [`Environment`](#environment) | (Required) Tealium environment name| `Environment.dev`|
| `dataSource`| `String`| CDH data source key| `&#34;abc123&#34;`|
| `collectors`| `Collectors[]`| (Required) Sets the list of [`Collectors`](#collectors) to initialize the Tealium library with| `[Collectors.AppData]`|
| `dispatchers`| `Dispatchers[]`| (Required) Sets the list of [`Dispatchers`](#dispatchers) to initialize the Tealium library with| `[Dispatchers.Collect]`|
| `customVisitorId`| `String`| Sets a custom Visitor ID| `&#34;ALK2398LSDKJ3289SLKJ3298SLKJ3&#34;`|
| `memoryReportingEnabled`       | `Boolean`| Enables or disables memory reporting in the DeviceData module (default: disabled).| `true`|
| `overrideCollectDomain`           | `String`| Overrides the domain of the Tealium Collect URL. For use with [first-party domains](/iq-tag-management/administration/first-party-domains/manage/). | `&#34;your-domain.com&#34;`|
| `overrideCollectProfile`           | `String`| Overrides the Tealium Collect profile to send data to a different Tealium profile. | `&#34;custom-profile&#34;`|
| `overrideCollectURL`           | `String`| Overrides the Tealium Collect URL to send data to a different endpoint. If using the event batching feature, also override the `overrideCollectBatchURL` property.| `&#34;https://custom-domain.com/event&#34;`|
| `overrideCollectBatchURL`      | `String`| Overrides the Tealium Collect batch URL to send data to a different endpoint.| `&#34;https://custom-domain.com/batch-event&#34;`|
| `overrideLibrarySettingsURL`   | `String`| Overrides the publish settings URL.| `&#34;https://custom-domain.com/mobile.html&#34;`|
| `overrideTagManagementURL`     | `String`| Overrides the default URL used by the Tag Management module. This is needed if you are self-hosting your Tealium JavaScript files.| `&#34;https://custom-domain.com/path/env/utag.js&#34;`|
| `deepLinkTrackingEnabled`      | `Boolean`| Enables or disables [automatic tracking of standard deep links](/platforms/getting-started-mobile/deep-linking/#readout), such as links to the app from Facebook or other sources, as well as QR trace.  (default: enabled)| `false`|
| `qrTraceEnabled`               | `Boolean`| Enables or disables [QR trace](/platforms/getting-started-mobile/trace/#how-it-works). (default: enabled)| `false`|
| `loglevel`                     | [`LogLevel`](#loglevel)                     | Sets the log level property, which controls how much information is logged (default: silent)| `LogLevel.dev`|
| `consentExpiry`                | [`ConsentExpiry`](#consentexpiry)           | Sets the expiration of the user&#39;s consent preferences. (defaults dependent upon policy)| `ConsentExpiry(90, TimeUnit.days)`|
| `consentLoggingEnabled`        | `Boolean`| Enables the [Consent Logging]() feature, which sends all consent status changes to Tealium Customer Data Hub for auditing purposes. (default: enabled)   | `true`|
| `consentPolicy`                | [`ConsentPolicy`](#consentpolicy)           | Sets the consent policy. For example, CCPA or GDPR. Consent manager is only enabled if this property is set.| `ConsentPolicy.gdpr`|
| `lifecycleAutotrackingEnabled` | `Boolean`| Enables or disables lifecycle auto tracking. (default: enabled)| `false`|
| `useRemoteLibrarySettings`     | `Boolean`| Enables or disables the [Mobile Publish Settings]() (default: enabled) Configure the Mobile Publish Settings in Tealium iQ Tag Management, or disable the feature. | `false`|
| `visitorServiceEnabled`        | `Boolean`| Enables or disables the automatic retrieval of the Visitor Profile using the [Data Layer Enrichment API]() (default: disabled)| `true`|
| `remoteCommands`               | `RemoteCommand[]`| Sets a list of [RemoteCommand](#RemoteCommand) objects to add when the instance is ready| `[{ id: &#34;hello-world&#34;, callback: (payload) =&gt; { console.log(&#34;hello-world: &#34; &#43; JSON.stringify(payload)); } }]` |
| `overrideConsentCategoriesKey` | `String` | Overrides the name of the consent categories event attribute. Use this to support custom enforcement of server-side consent. Learn more about [disabling automatic enforcement of server-side consent](). (default: `consent_categories`)| `consent_categories_granted` |
| `visitorIdentityKey` | `String` | Use to support visitor switching and to specify the shared key to identify multiple users of the app. | `user_profile_id` |

### Collectors

Collectors are modules that gather supplemental information from the device and append it to the data layer before transmitting it to the Tealium Customer Data Hub. Some collectors are included in the core library, while others are optional and installed as separate modules.

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
    new List&lt;Collectors&gt; {
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
    new List&lt;Dispatchers&gt; {
        Dispatchers.Collect, Dispatchers.RemoteCommands
    }
    // ...
);
```

The following dispatchers are available:

* `Dispatchers.Collect`
* `Dispatchers.RemoteCommands`
* `Dispatchers.TagManagement`

At least one dispatcher is required.

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
| `ArraysOfBooleans` | `IDictionary&lt;string, IList&lt;bool&gt;&gt;`                 | `id: &#34;5129&#34;, value: [true,false,true,true]`                          |
| `ArraysOfNumbers`  | `IDictionary&lt;string, IList&lt;double&gt;&gt;`               | `id: &#34;57&#34;, value: [4.82125, 16.8, 0.5714285714285714]`               |
| `ArraysOfStrings`  | `IDictionary&lt;string, IList&lt;string&gt;&gt;`               | `id: &#34;5213&#34;, value: [&#34;green shirts&#34;, &#34;green shirts&#34;, &#34;blue shirts&#34;]` |
| `Audiences`        | `IDictionary&lt;string, string&gt;`                      | `id: &#34;tealiummobile\_demo\_103&#34;, value: &#34;iOS Users&#34;`                 |
| `Badges`           | `IDictionary&lt;string, bool&gt;`                        | `id: &#34;2815&#34;, value: true`                                            |
| `Booleans`         | `IDictionary&lt;string, bool&gt;`                        | `id: &#34;4868&#34;, value: true`                                            |
| `CurrentVisit`     | `ICurrentVisit`                                    |                                                                      |
| `Dates`            | `IDictionary&lt;string, long&gt;`                        | `id: &#34;22&#34;, value: 1567120112000`                                     |
| `Numbers`          | `IDictionary&lt;string, double&gt;`                      | `id: &#34;5728&#34;, value: 4.82125`                                         |
| `SetOfStrings`     | `IDictionary&lt;string, ISet&lt;string&gt;&gt;`                | `id: &#34;5211&#34;, value: [&#34;green shirts&#34;, &#34;red shirts&#34;, &#34;blue shirts&#34;]`   |
| `Strings`          | `IDictionary&lt;string, string&gt;                       | `id: &#34;5380&#34;, value: &#34;green shirts&#34;`                                  |
| `Tallies`          | `IDictionary&lt;string, IDictionary&lt;string, double&gt;&gt;` | `&#34;57&#34;: [[&#34;category 1&#34;: 2.0], &#34;category 2&#34;: 1.0]]`                    |

### `ICurrentVisit`

The object that contains attributes scoped to the current visit.

| Parameters| Properties| Value|
|:----------|:----------|:-----|
| `ArraysOfBooleans` | `IDictionary&lt;string, IList&lt;bool&gt;&gt;`                 | `id: &#34;5129&#34;, value: [true,false,true,true]`                          |
| `ArraysOfNumbers`  | `IDictionary&lt;string, IList&lt;double&gt;&gt;`               | `id: &#34;57&#34;, value: [4.82125, 16.8, 0.5714285714285714]`               |
| `ArraysOfStrings`  | `IDictionary&lt;string, IList&lt;string&gt;&gt;`               | `id: &#34;5213&#34;, value: [&#34;green shirts&#34;, &#34;green shirts&#34;, &#34;blue shirts&#34;]` |
| `Booleans`         | `IDictionary&lt;string, bool&gt;`                        | `id: &#34;4868&#34;, value: true`                                            |
| `Dates`            | `IDictionary&lt;string, long&gt;`                        | `id: &#34;22&#34;, value: 1567120112000`                                     |
| `Numbers`          | `IDictionary&lt;string, double&gt;`                      | `id: &#34;5728&#34;, value: 4.82125`                                         |
| `SetOfStrings`     | `IDictionary&lt;string, ISet&lt;string&gt;&gt;`                | `id: &#34;5211&#34;, value: [&#34;green shirts&#34;, &#34;red shirts&#34;, &#34;blue shirts&#34;]`   |
| `Strings`          | `IDictionary&lt;string, string&gt;                       | `id: &#34;5380&#34;, value: &#34;green shirts&#34;`                                  |
| `Tallies`          | `IDictionary&lt;string, IDictionary&lt;string, double&gt;&gt;` | `&#34;57&#34;: [[&#34;category 1&#34;: 2.0], &#34;category 2&#34;: 1.0]]`                    |
| `TotalEventCount`  | `int`                                              | `42`                                                                 |
| `CreatedAt`        | `long`                                             | `1638236024`                                                         |


## Interface: `TealiumDispatch`

An interface that defines the type of dispatch to be tracked. The following classes implement `TealiumDispatch`:

### Class: `TealiumEvent`

To track a user&#39;s interaction with a screen , pass an instance of `TealiumEvent(tealiumEvent, dataLayer)` to the [`Track()`](#track) method. `TealiumEvent` consists of an event name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```csharp
tealium.Track(new TealiumEvent(tealiumEvent, eventData));
```

| Parameters  | Type    | Description      | 
|:------------|:--------|:-----------------|
| `tealiumEvent` | `string` | The event name, passed as the `tealium_event` attribute.  |
| `eventData` | `Dictionary&lt;string, object&gt;` | (Optional) Data to be sent with the event in key-value format. | 

Example:

```csharp
tealium.Track(new TealiumEvent(&#34;cart_add&#34;, new Dictionary&lt;string, object&gt; {
    { &#34;customer_id&#34;, &#34;abc123&#34; }, 
    { &#34;product_id&#34;, new[] {&#34;PROD123&#34;, &#34;PROD456&#34;} },
    { &#34;product_price&#34;, new[] {4.00, 6.00} }
}));
```

### Class: `TealiumView`

To track screen views, pass an instance of `TealiumView(tealiumEvent, dataLayer)` to the [`Track()`](#track) method. `TealiumView` consists of a view name, which appears in the tracking call as `tealium_event`, and an optional data dictionary.

```csharp
tealium.Track(new TealiumView(tealiumEvent, eventData));
```

| Parameters  | Type    | Description      | 
|:------------|:--------|:-----------------|
| `tealiumEvent`  | `string`| `tealium_event` name of view event or screen.          | 
| `eventData` | `Dictionary&lt;string, object&gt;` | (Optional) Data to be sent with the event in key-value format. |

Example:

```csharp
tealium.Track(new TealiumView(&#34;purchase&#34;, new Dictionary&lt;string, object&gt; {
    { &#34;customer_id&#34;, &#34;abc123&#34; },
    { &#34;order_total&#34;, 10.00 },
    { &#34;product_id&#34;, new[] {&#34;PROD123&#34;, &#34;PROD456&#34;} },
    { &#34;order_id&#34;, &#34;0123456789&#34; }
}));
```
