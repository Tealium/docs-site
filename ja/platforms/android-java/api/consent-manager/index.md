---
title: ConsentManager
description: Tealium for Androidで提供されているConsentManagerクラスおよびメソッドに関するリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-java/api/consent-manager/
---
## クラス：`ConsentManager`

以下は、一般的に使用される`ConsentManager`クラスのメソッドをまとめたものです。

| メソッド | 説明|
| ----- | ------|
| `getPolicy()` | 現在のポリシーを返します|
| `getUserConsentCategories()` | ユーザーの現在の同意カテゴリを返します|
| `getUserConsentPreferences()` | UserConsentPreferencesオブジェクトを返します|
| `getUserConsentStatus()` | ユーザーの現在の同意ステータスを返します|
| `resetUserConsentPreferences()` | ユーザーの同意構成をリセットします|
| `setPolicy()` | デフォルトのポリシーパラメータをオーバーライドします（デフォルト：gdpr）|
| `setUserConsentCategories()` | ユーザーの同意ステータスと同意カテゴリを構成します|
| `setUserConsentStatus()`| ユーザーの同意ステータスを構成します|
| `setUserConsentStatusWithCategories()` | 1つのコールで同意ステータスとカテゴリを構成します|

### `getPolicy()`

現在のポリシーを返します。

```java
final String currentPolicy = tealiumInstance.getConsentManager().getPolicy();

```
| 戻り値 | 戻り値の型|
| --- | ---|
| User's current policy | `String` |


### `getUserConsentCategories()`

ユーザーの現在の同意カテゴリを返します。

```java
final String[] userCategories = tealiumInstance.getConsentManager().getUserConsentCategories();
```

| 戻り値 | 戻り値の型|
| --- | ---|
| User's current consent categories | `String[]` |


### `getUserConsentPreferences()`

ユーザーの同意構成を返します。

```java
final UserConsentPreferences userPreferences = tealiumInstance.getConsentManager().getUserConsentPreferences();
```

| 戻り値 | 戻り値の型|
| --- | ---|
| User's consent preferences | `UserConsentPreferences` |



### `getUserConsentStatus()`

ユーザーの現在の同意ステータスを返します。

```java
final String userStatus = tealiumInstance.getConsentManager().getUserConsentStatus();
```

| 戻り値 | 戻り値の型|
| --- | ---|
| User's current consent status | `String` |


### `resetUserConsentPreferences()`

保存されている同意構成をクリアし、ユーザー構成をデフォルトにリセットして、同意ステータスをカテゴリが何も構成されていない`UNKNOWN`に構成します。


```java
tealiumInstance.getConsentManager().resetUserConsentPreferences();
```

### `setPolicy()`

デフォルトのポリシーパラメータをオーバーライドします。デフォルトは`gdpr`です。

```java
tealiumInstance.getConsentManager().setPolicy(policy);
```
| パラメータ | 型| 説明| 例|
| --- | ---| --- | --- |
| `policy` | `String` |構成するポリシー| `"custompolicy"` |


### `setUserConsentCategories()`

ユーザーの同意ステータスと同意カテゴリを構成します。このメソッドはアプリの同意管理構成画面から呼び出します。このメソッドでは、任意の数のカテゴリが構成された場合に、ユーザーの同意ステータスが自動的に`CONSENTED`に構成されます。

```java
tealiumInstance.getConsentManager().setUserConsentCategories(categories);
```
| パラメータ | 型| 説明| 例|
| --- | ---| --- | --- |
| `categories` | `[String]` |構成するカテゴリ|`String[]` | `new String[]{ConsentManager.ConsentCategory.ANALYTICS, ConsentManager.ConsentCategory.BIG_DATA}` |

以下の静的定数は、サポートされている同意カテゴリの包括的なリストです。

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

ユーザーの同意ステータスを構成します。このメソッドは、ユーザーがトラッキングをオプトインまたはオプトアウトしたときに、アプリの同意管理構成画面から呼び出します。`true`の場合は、すべてのカテゴリが自動的に有効になります。`false`の場合は、すべてのカテゴリが自動的に無効になります。

このメソッドを使用してユーザーのステータスが`CONSENTED`に構成されると、Consent Managerでは、ユーザーが自動的に使用可能なすべての同意カテゴリにサブスクライブされます（一部のカテゴリのみにすることはできません）。

```java
tealiumInstance.getConsentManager().setUserConsentStatus(status);
```
| パラメータ | 型| 説明| 例|
| --- | ---| --- | --- |
| `status` | `String` |ユーザーの同意に構成するステータス|  [`ConsentManager.ConsentStatus.CONSENTED`, `ConsentManager.ConsentStatus.NOT_CONSENTED`]|

これらの静的定数は、サポートされている同意ステータスの包括的なリストです。
```
CONSENTED
NOT_CONSENTED
UNKNOWN
```

**`UNKNOWN`**  
`UNKNOWN`ステータスは、Consent Managerのデフォルト構成です。このステータスの場合、Consent Managerはローカルでイベントをキューに追加します。これは、断定的な`CONSENTED/NOT_CONSENTED`ステータスが構成されるまで続きます。
```java
tealiumInstance.getConsentManager().setUserConsentStatus(ConsentManager.ConsentStatus.UNKNOWN);
```

**`CONSENTED`**  
`CONSENTED`ステータスは、ユーザーがトラッキングに同意している場合に構成されます。このステータスの場合、Consent Managerは、以前キューに追加されたトラックコールをキューから取り出し、以降のすべてのトラッキングコールを通常通りに続行できます。
```java
tealiumInstance.getConsentManager().setUserConsentStatus(ConsentManager.ConsentStatus.CONSENTED);
```

**`NOT_CONSENTED`**  
`NOT_CONSENTED`ステータスは、ユーザーがトラッキングを拒否している場合に構成されます。このステータスの場合、Consent Managerは、以前キューに追加されたトラックコールを削除し、以降のすべてのトラッキングコールがそれ以上SDKによって処理されないようにします。
```java
tealiumInstance.getConsentManager().setUserConsentStatus(ConsentManager.ConsentStatus.NOT_CONSENTED);
```

### `setUserConsentStatusWithCategories()`  

1. のコールで同意ステータスとカテゴリを構成します。

```java
tealiumInstance.getConsentManager().setUserConsentStatusWithCategories(status, categories);
```

| パラメータ | 型| 説明| 例|
| --- | ---| --- | --- |
| `status` | `String` |ユーザーの同意に構成するステータス| [`ConsentManager.ConsentStatus.CONSENTED`, `ConsentManager.ConsentStatus.NOT_CONSENTED`]|
| `categories` | `[String]` | 構成するカテゴリ|  `new String[]{ConsentManager.ConsentCategory.ANALYTICS, ConsentManager.ConsentCategory.BIG_DATA}` |

サポートされている定数のリストについては、`setUserConsentStatus()`と`setUserConsentCategories()`を参照してください。

