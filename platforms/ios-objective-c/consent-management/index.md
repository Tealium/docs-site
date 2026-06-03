---
title: Consent management
description: Learn to implement consent management for iOS (Objective-C).
url: https://docs.tealium.com/platforms/ios-objective-c/consent-management/
---
## Usage

Usage of this module is recommended, as it is automatically included and enabled in the CocoaPods framework builds.

Supported platforms include: iOS, macOS, tvOS, and watchOS.

For more information about consent management, see .

## Sample Apps

To help familiarize yourself with enabling Tealium consent management, it is recommended to download the sample apps:

*   [Objective-C Sample App](https://github.com/Tealium/tealium-ios/tree/master/Samples/ConsentManagerDemo_ObjC)
*   [Swift Sample App](https://github.com/Tealium/tealium-ios/tree/master/Samples/ConsentManagerDemo_Swift)


## Data Layer

The following variables are transmitted with each tracking call while consent management is enabled:

| Variable Name | Description | Example |
| --- | --- | --- |
| `policy` | The policy under which consent was collected (Default: `gdpr`)| `gdpr` |
| `consent_status` | The user&#39;s current consent status | [`&#34;Consented&#34;`, `&#34;Not Consented&#34;`] |
| `consent_categories` | The user&#39;s current categories they are consented to | `@[@&#34;analytics&#34;]` |


## Use Cases

### Use Case: Simple Opt-in

```objc
[_tealium.consentManager setUserConsentStatus:Consented];
```

This example shows you how to give your users a simple &#34;Opt-in/Opt-out&#34; option. If the user consents, they are automatically opted-in to all tracking categories. If they revoke their consent, no categories are active, and no tracking calls are sent.

Define and call the following method in your Tealium Helper class when your app user consents to or declines tracking. If the user consents to tracking, the consent manager automatically opts them in to all tracking categories.

![](/images/platforms/ios/consent-simple-optin.gif)

### Use Case: Grouped Opt-in

```objc
[_tealium.consentManager setUserConsentStatus:Consented withUserConsentCategories:@[@&#34;analytics&#34;, @&#34;monitoring&#34;, @&#34;big_data&#34;, @&#34;mobile&#34;, @&#34;crm&#34;]];
```

This example shows a category-based consent model, where tracking categories are grouped into a smaller number of higher-level categories, defined by you. For example, you may choose to group the Tealium consent categories `&#34;analytics&#34;`, `&#34;monitoring&#34;`, `&#34;big_data&#34;`, `&#34;mobile&#34;`, and `&#34;crm&#34;` under a single category called `&#34;performance&#34;`. This may be easier for the user than selecting from the full list of categories. You may choose to represent this in a slider interface, ranging from least-permissive to most-permissive (all categories).

![](/images/platforms/ios/consent-group-optin.gif)

### Use Case: Category-based Opt-in

```objc
[_tealium.consentManager setUserConsentStatus:Consented withUserConsentCategories:@[@&#34;analytics&#34;, @&#34;personalization&#34;]];
```

This example shows a category-based consent model where the user must explicitly select each category from the full list of categories. The default state of the consent manager is `&#34;Unknown&#34;`, which queues hits until the user provides their consent. If the user consents to any category, events are dequeued, and the consented category data is appended to each tracking call.

![](/images/platforms/ios/consent-category-optin.gif)

## API Reference

### `consentManager`
This code shows how to enable consent management on Tealium initialization.

```objc
// TealiumHelper.h

@import TealiumIOS;
@interface TealiumHelper : NSObject&lt;TealiumDelegate, TEALConsentManagerDelegate&gt;
@property (nonatomic, strong) Tealium *tealium;
@end

// TealiumHelper.m

@implementation TealiumHelper

&#43; (instancetype _Nonnull)sharedInstance {
  static TealiumHelper *tealiumHelper = nil;
  static dispatch_once_t onceToken;
  dispatch_once(&amp;onceToken, ^{
  tealiumHelper = [[self alloc] init];
  });

  return tealiumHelper;
}

- (instancetype)init {
  if (self = [super init]) {
    TEALConfiguration *configuration = [TEALConfiguration configurationWithAccount:@&#34;ACCOUNT&#34; profile:@&#34;PROFILE&#34; environment:@&#34;ENVIRONMENT&#34;];
    [configuration setLogLevel: TEALLogLevelDev];

    // enable Tealium consent manager
    [configuration setEnableConsentManager:YES];

    _tealium = [Tealium newInstanceForKey:@&#34;INSTANCE&#34; configuration:configuration];
    _tealium.delegate = self;

    // set optional Tealium consent manager Delegate
    _tealium.consentManagerDelegate = self;
    NSLog(@&#34;%s, %@&#34;, __FUNCTION__, [TEALConsentManager consentStatusString:_tealium.consentManager.userConsentStatus]);
  }

  return self;
}

@end
```

**`enable`**  
Enable consent manager. This method enables consent manager at a later time and not on Tealium initialization.

```objc
[_tealium.consentManager enable];
```

The recommended approach is to enable consent manager on Tealium initialization.  

**`isEnabled`**  
Checks if consent manager is enabled.

```objc
[_tealium.consentManager isEnabled];
```

**`disable`**  
Disables consent manager. This method disables consent manager after Tealium is fully initialized.

```objc
[_tealium.consentManager disable];
```

**`isDisabled`**  
Checks if the consent manager is disabled.

```objc
[_tealium.consentManager isDisabled];
```

**`consentManagerDelegate`**  
Registers a specific class conforming to the TEALConsentManagerDelegate protocol.

```objc
[_tealium setConsentManagerDelegate:(id&lt;TEALConsentManagerDelegate&gt;)];
```

**`setUserConsentStatus`**  
Sets the user&#39;s consent status. Designed to be called from your consent management preferences screen in your app when the user enables or disables tracking.

```objc
[_tealium.consentManager setUserConsentStatus:Consented];
```

Consent manager always sets the list of consented categories to include ALL available consent categories if the status is `Consented`. This method does not allow categories to be set selectively.  

| Parameters | Description | Example |
| --- | --- | --- |
| `TEALConsentStatus` | A value from TEALConsentStatus enum | [`Consented`, `NotConsented`, `Disabled`] |

**`setUserConsentCategories`**  
Sets the user&#39;s consent categories. Designed to be called from your consent management preferences screen in your app.

```objc
[_tealium.consentManager setUserConsentCategories:@[@&#34;analytics&#34;]];
```

Always sets consent status to `Consented` when any number of categories are set.

| Parameters | Description | Example |
| --- | --- | --- |
| `NSArray` | An array of predefined NSString categories | `@[@&#34;analytics&#34;, @&#34;big_data&#34;]` |

**`setUserConsentStatus:withUserConsentCategories`**  
Sets the user&#39;s consent status and user&#39;s consent categories in a single method.

```objc
[_tealium.consentManager setUserConsentStatus:Consented withUserConsentCategories:@[@&#34;analytics&#34;]];
```

| Parameters | Description | Example Value |
| --- | --- | --- |
| TEALConsentStatus | A value from TEALConsentStatus enum | [`Consented`, `NotConsented`] |
| NSArray | An array of predefined NSString categories | `@[@&#34;analytics&#34;, @&#34;big_data&#34;]` |

**`userConsentStatus`**  
Returns the current consent status of the user.

```objc
[_tealium.consentManager userConsentStatus];
```

**`userConsentCategories`**  
Returns the current consent categories of the user.

```objc
[_tealium.consentManager userConsentCategories];
```

**`isConsented`**  
Convenience method to determine if the user is consented.

```objc
[_tealium.consentManager isConsented];
```

**`consentStatusString`**  
Convenience method for human-readable string of the TEALConsentStatus enum.
```objc
[TEALConsentManager consentStatusString:_tealium.consentManager.userConsentStatus];
```

**`resetUserConsentPreferences`**  
Resets all currently stored consent preferences. Reverts to `Unknown` consent status with no categories.
```objc
[_tealium.consentManager resetUserConsentPreferences];
```

**`setConsentLoggingEnabled`**  
Enables the [Consent Logging]() feature, which sends all consent status changes to Tealium Customer Data Hub for auditing purposes.

```objc
[_tealium.consentManager setConsentLoggingEnabled:YES];
```

| Parameters | Description | Example Value |
| --- | --- | --- |
| `TEALConsentLoggingEnabled` | Enables or disables consent logging | [`YES`, `NO`] |

**`isConsentLoggingEnabled`**  
Returns the current state of the consent logging feature.
```objc
[_tealium.consentManager isConsentLoggingEnabled];
```

**`allCategories`**  
Returns the complete list of supported consent categories.
```objc
[_tealium.consentManager allCategories];
```

### `TEALConfiguration`

**`enableConsentManager`**  
Sets the initial consent status for the user when the library starts up for the first time. If there are saved preferences, they override any preferences passed in the config object.
```objc
self.configuration.enableConsentManager = YES;
```

Consent manager always sets the list of consented categories to include ALL available consent categories, if the status is `Consented`. This method does not allow categories to be set selectively.

**`userConsentStatus`**  
Sets the user&#39;s initial consent status when the library starts up for the first time. If there are saved preferences, these override any preferences passed in the config object.
```objc
self.configuration.userConsentStatus = Consented;
```

| Parameters | Description | Example Value |
| --- | --- | --- |
| `TEALConsentStatus` | A value from TEALConsentStatus enum | [`Consented`, `NotConsented`, `Disabled`] |

**`userConsentCategories`**  
Sets the user&#39;s initial consent categories when the library starts up for the first time. If there are saved preferences, these  override any preferences passed in the config object.
```objc
self.configuration.userConsentCategories = @[@&#34;analytics&#34;, @&#34;retargeting&#34;];
```

| Parameters | Description | Example Value |
| --- | --- | --- |
| `NSArray` | An array of predefined NSString categories | `@[@&#34;analytics&#34;, @&#34;big_data&#34;]` |


### `TEALConsentManagerDelegate`

**`consentManagerDidChangeWithState`**  
This method is called whenever the consent manager user consent status is changed. For example, the user consented or declined tracking.

```objc
- (void)consentManagerDidChangeWithState:(TEALConsentStatus)consentStatus;
```

**`consentManagerDidUpdateConsentCategories`**  
This method is called whenever the consent manager user consent categories are updated.

```objc
-(void)consentManagerDidUpdateConsentCategories:(NSArray * \_Nullable)categories;
```

**`consentManagerWillDropDispatch`**  
This method is called whenever the consent manager is going to drop a tracking call. For example, the user declined tracking.

```objc
- (void)consentManagerWillDropDispatch:(TEALDispatch * \_Nullable)dispatch;
```

**`consentManagerWillQueueDispatch`**  
This method is called whenever the consent manager is in the `Unknown` state. Tracking calls are being queued locally until the user grants or declines consent.

```objc
- (void)consentManagerWillQueueDispatch:(TEALDispatch * \_Nullable)dispatch;
```

## Consent Categories

The following lists all the supported consent categories:

*   `analytics`
*   `affiliates`
*   `display_ads`
*   `email`
*   `personalization`
*   `search`
*   `social`
*   `big_data`
*   `mobile`
*   `engagement`
*   `monitoring`
*   `cdm`
*   `cdp`
*   `cookiematch`
*   `misc`

## TEALConsentStatus

**`Unknown`**  
The `Unknown` status is the default setting for the consent manager. In this state, the consent manager queues events locally until an affirmative `Consented` / `NotConsented` status is provided.

```objc
self.tealium.consentManager.userConsentStatus = Unknown
```

**`Consented`**  
The `Consented` status is set when the user has consented to tracking. In this state, the consent manager allows all tracking calls to continue as normal.

```objc
self.tealium.consentManager.userConsentStatus = Consented
```

**`NotConsented`**  
The `NotConsented` status is set when the user has declined tracking. In this state, the consent manager drops all tracking calls and halt further processing by the SDK.

```objc
self.tealium.consentManager.userConsentStatus = NotConsented
```
