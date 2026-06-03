---
title: ConsentManager
description: Reference guide for ConsentManager class and methods provided by Tealium for Android.
url: https://docs.tealium.com/platforms/android-java/api/consent-manager/
---
## Class: `ConsentManager`

The following summarizes the commonly used methods of the `ConsentManager` class.

| Method | Description |
| ----- | ------ |
| `getPolicy()` | Returns the current policy |
| `getUserConsentCategories()` | Returns the current consent categories of the user |
| `getUserConsentPreferences()` | Returns the UserConsentPreferences object |
| `getUserConsentStatus()` | Returns the current consent status of the user |
| `resetUserConsentPreferences()` | Resets user consent consent preferences |
| `setPolicy()` | Overrides the default policy parameter (default: gdpr) |
| `setUserConsentCategories()` | Sets the user&#39;s consent status and categories |
| `setUserConsentStatus()`| Sets the user&#39;s consent status |
| `setUserConsentStatusWithCategories()` | Sets the consent status and categories in a single call|

### `getPolicy()`

Returns the current policy.

```java
final String currentPolicy = tealiumInstance.getConsentManager().getPolicy();

```
| Returns | Return Type |
| --- | --- |
| User&#39;s current policy | `String` |


### `getUserConsentCategories()`

Returns the current consent categories of the user.

```java
final String[] userCategories = tealiumInstance.getConsentManager().getUserConsentCategories();
```

| Returns | Return Type |
| --- | --- |
| User&#39;s current consent categories | `String[]` |


### `getUserConsentPreferences()`

Returns the user&#39;s consent preferences.

```java
final UserConsentPreferences userPreferences = tealiumInstance.getConsentManager().getUserConsentPreferences();
```

| Returns | Return Type |
| --- | --- |
| User&#39;s consent preferences | `UserConsentPreferences` |



### `getUserConsentStatus()`

Returns the current consent status of the user.

```java
final String userStatus = tealiumInstance.getConsentManager().getUserConsentStatus();
```

| Returns | Return Type |
| --- | --- |
| User&#39;s current consent status | `String` |


### `resetUserConsentPreferences()`

Clears stored consent preferences, resets user preferences to defaults, and sets consent status to `UNKNOWN` with no categories.


```java
tealiumInstance.getConsentManager().resetUserConsentPreferences();
```

### `setPolicy()`

Overrides the default policy parameter. Default is `gdpr`.

```java
tealiumInstance.getConsentManager().setPolicy(policy);
```
| Parameter | Type | Description| Example |
| --- | --- | --- | --- |
| `policy` | `String` |Policy to set | `&#34;custompolicy&#34;` |


### `setUserConsentCategories()`

Sets the user&#39;s consent status and categories. Call this method from your consent management preferences screen in your app. This method automatically sets the user&#39;s consent status to `CONSENTED` if any number of categories are set.

```java
tealiumInstance.getConsentManager().setUserConsentCategories(categories);
```
| Parameter | Type | Description | Example |
| --- | --- | --- | --- |
| `categories` | `[String]` |Categories to set |`String[]` | `new String[]{ConsentManager.ConsentCategory.ANALYTICS, ConsentManager.ConsentCategory.BIG_DATA}` |

The following static constants are the complete list of supported consent categories:

```
AFFILIATES
ANALYTICS
BIG_DATA
CDP
COOKIEMATCH
CRM
DISPLAY_ADS
EMAIL
ENGAGEMENT
MOBILE
MONITORING
PERSONALIZATION
SEARCH
SOCIAL
MISC
```

### `setUserConsentStatus()`  

Sets the user&#39;s consent status. Call this method from your consent management preferences screen in your app when the user opts in or opts out of tracking. If `true`, automatically enables all categories.  If `false`, all categories automatically disabled.

If the user&#39;s status is set to `CONSENTED` using this method, the consent manager automatically subscribes the user to ALL available consent categories (subset of categories not allowed).

```java
tealiumInstance.getConsentManager().setUserConsentStatus(status);
```
| Parameter | Type | Description | Example |
| --- | --- | --- | --- |
| `status` | `String` |Status to set the user&#39;s consent |  [`ConsentManager.ConsentStatus.CONSENTED`, `ConsentManager.ConsentStatus.NOT_CONSENTED`] |

These static constants are the complete list of supported consent statuses.
```
CONSENTED
NOT_CONSENTED
UNKNOWN
```

**`UNKNOWN`**  
The `UNKNOWN` status is the default setting for the consent manager. In this state, the consent manager queues events locally until an affirmative `CONSENTED/NOT_CONSENTED` status is provided.
```java
tealiumInstance.getConsentManager().setUserConsentStatus(ConsentManager.ConsentStatus.UNKNOWN);
```

**`CONSENTED`**  
The `CONSENTED` status is set when the user has consented to tracking. In this status, the consent manager dequeues any previously queued track calls and allow all subsequent tracking calls to continue as normal.
```java
tealiumInstance.getConsentManager().setUserConsentStatus(ConsentManager.ConsentStatus.CONSENTED);
```

**`NOT_CONSENTED`**  
The `NOT_CONSENTED` status is set when the user has declined tracking. In this state, the consent manager purges any previously queued track calls and drops all subsequent tracking calls from being further processed by the SDK.
```java
tealiumInstance.getConsentManager().setUserConsentStatus(ConsentManager.ConsentStatus.NOT_CONSENTED);
```

### `setUserConsentStatusWithCategories()`  

Sets the consent status and categories in a single call.

```java
tealiumInstance.getConsentManager().setUserConsentStatusWithCategories(status, categories);
```

| Parameter | Type | Description  | Example |
| --- | --- | --- | --- |
| `status` | `String` |Status to set the user&#39;s consent | [`ConsentManager.ConsentStatus.CONSENTED`, `ConsentManager.ConsentStatus.NOT_CONSENTED`] |
| `categories` | `[String]` | Categories to set |  `new String[]{ConsentManager.ConsentCategory.ANALYTICS, ConsentManager.ConsentCategory.BIG_DATA}` |

See `setUserConsentStatus()` and `setUserConsentCategories()` for a list of constant supported.
