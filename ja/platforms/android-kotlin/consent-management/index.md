---
title: 同意管理
description: Android Kotlin 向けの同意管理の実装方法について説明します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/consent-management/
---
## 使用方法

同意管理モジュールの使用を推奨します。このモジュールは初期化時に自動的に有効になります。Android モバイルおよび Android TV でサポートされています。

[`TealiumConfig`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/#consentmanagerpolicy) 内で同意管理ポリシーを初期化します。その後、[`tealium.consentManager`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium/#consentmanager) の Tealium インスタンスを使用してユーザーの同意を管理します。

[同意管理](https://docs.tealium.com/ja/platforms/getting-started-mobile/consent-management/)と同意ポリシーの詳細をご覧ください。

## 同意

### ポリシーの構成

初期化時に、同意ポリシーを次のいずれかに構成します。

* `ConsentPolicy.GDPR`
* `ConsentPolicy.CCPA`


<blockquote>
Only one policy may be enforced on a device at any given time.
</blockquote>


```java
val config = TealiumConfig(...).apply {
  consentManagerPolicy = ConsentPolicy.GDPR
}
```

### 同意の有効期限

[`consentExpiry`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/#consentexpiry) プロパティを使用して、同意の選択内容の有効期限を構成します。

次の例では、同意管理ポリシーを GDPR に構成し、有効期限を 90 日に構成します。

```java
val config = TealiumConfig(...).apply {
  consentManagerPolicy = ConsentPolicy.GDPR
  consentExpiry = ConsentExpiry(90, TimeUnit.DAYS)
}
```

同意の有効期限が切れたときにコールバックをトリガーするには、[`onUserConsentPreferencesUpdated()`](https://docs.tealium.com/ja/platforms/android-kotlin/api/consent-manager/#onuserconsentpreferencesupdated) メソッドを使用して、`ConsentStatus` が `UNKNOWN` になったかどうかを確認します。

```java
Tealium.create(BuildConfig.TEALIUM_INSTANCE, config) {
    events.subscribe(object : UserConsentPreferencesUpdatedListener {
        override fun onUserConsentPreferencesUpdated(userConsentPreferences: UserConsentPreferences,
                                                     policy: ConsentManagementPolicy) {
            if (userConsentPreferences.consentStatus == ConsentStatus.UNKNOWN) {
                Logger.dev(BuildConfig.TAG, "Re-prompt for consent")
            }
        }
    })
}
```

### 完全な同意の構成

完全な同意を構成するには、次のようにします。

```java
tealium.consentManager.userConsentStatus = ConsentStatus.CONSENTED
```


<blockquote>
Setting full consent implicitly sets the consent categories to the full list of available [`ConsentCategory`](https://docs.tealium.com/ja/platforms/android-kotlin/api/consent-category/#class-consentcategory) types.
</blockquote>


### カテゴリ別の部分的な同意の構成

部分的な同意を構成するには、同意カテゴリのサブセットを指定します。これにより、[`userConsentStatus`](https://docs.tealium.com/ja/platforms/android-kotlin/api/consent-manager/#userconsentstatus) は暗黙的に `CONSENTED` に構成されます。

```java
tealium.consentManager.userConsentCategories = setOf(ConsentCategory.ANALYTICS, ConsentCategory.EMAIL)
```

### 同意拒否の構成

同意を拒否するには、同意ステータスを構成します。  
```java
tealium.consentManager.userConsentStatus = ConsentStatus.NOT_CONSENTED
```

または、同意カテゴリを `null` に構成します。

## カスタム同意

組織の同意要件が、標準の[オプトイン](https://docs.tealium.com/ja/glossary/#opt-in-model-consent)および[オプトアウト](https://docs.tealium.com/ja/glossary/#opt-out-model-consent)の同意管理ポリシーで対応できない場合は、カスタム同意ポリシーを作成します。

1. `ConsentManagementPolicy` インターフェイスを実装します。      
      ```java
      val customPolicy = object: ConsentManagementPolicy {
            //implement methods...
      }
      ```
2. `setCustomPolicy()` メソッドを使用して、`ConsentManagementPolicy` の実装を `ConsentPolicy.CUSTOM` 列挙型に渡します。      
      ```java
      ConsentPolicy.CUSTOM.setCustomPolicy(customPolicy)
      ```
3. [`consentManagerPolicy`](https://docs.tealium.com/ja/platforms/android-kotlin/api/tealium-config/#consentmanagerpolicy) プロパティを使用して、`TealiumConfig` オブジェクトに `ConsentPolicy.CUSTOM` オプションを渡します。   
      ```java
      config.consentManagerPolicy = ConsentPolicy.CUSTOM
      ```

カスタムの `ConsentManagementPolicy` 実装では、既存の同意管理のメソッドとプロパティを、指定された `superPolicy` に委任できます。`superPolicy` は各イベントの `policy` キーを独自の名前で上書きします。

```java
class CustomPolicy(
        val superPolicy: ConsentManagementPolicy
        ) : ConsentManagementPolicy by superPolicy {
    override val name: String = "custom_policy"

    override fun policyStatusInfo(): Map<String, Any> {
        return superPolicy.policyStatusInfo().toMutableMap().apply {
            put(ConsentManagerConstants.CONSENT_POLICY, name)
        }
    }
}

val customPolicy = CustomPolicy(ConsentPolicy.GDPR.create(
    UserConsentPreferences(ConsentStatus.UNKNOWN, null)))
```

カスタム同意ポリシーを実装した後、必要に応じて `ConsentManagementPolicy` で使用可能な次のプロパティおよびメソッドをオーバーライドします。

| プロパティ／メソッド | 型 | 説明 |
| ----- | ------ | ----- |
| `name` | `String` | `ConsentManagementPolicy` の名前 |
| `userConsentPreferences` | `UserConsentPreferences` | 現在の `UserConsentPreferences`。構成が変更されると、`ConsentManager` によって自動的に更新されます |
| `consentLoggingEnabled` | `Boolean` | 同意の変更をログに記録する必要があるかどうかを構成します |
| `consentLoggingEventName` | `String` | 同意の変更をログに記録するときに使用するイベント名（キー：`tealium_event`）を構成します |
| `defaultConsentExpiry`] |`ConsentExpiry` | `ConsentManagementPolicy` のデフォルトの有効期限を構成します |
| `cookieUpdateRequired`| `Boolean` | TagManagement モジュールの WebView で Cookie を更新するかどうかを構成します |
| `cookieUpdateEventName` |  `String` | `cookieUpdateRequired` が `true` に構成されている場合に使用するイベント名を構成します |
| `policyStatusInfo()` |`Map<String, Any>` | 各ディスパッチのペイロードに追加するキーと値のデータのマップを返します |
| `shouldQueue()` | `Boolean` | `ConsentPolicy` のルールに従ってディスパッチをキューに追加するかどうかを返します |
| `shouldDrop()`| `Boolean` | `ConsentPolicy` のルールに従ってディスパッチを破棄するかどうかを返します |

### 例

次の例では、Event Streaming の固定された同意値を回避するために、ポリシーデータのキーを再マッピングします。   
```java
class CustomPolicy(
        val superPolicy: ConsentManagementPolicy
) : ConsentManagementPolicy by superPolicy {
    return superPolicy.policyStatusInfo().toMutableMap().apply {
        get(ConsentManagerConstants.CONSENT_STATUS)?.let { status ->
            remove(ConsentManagerConstants.CONSENT_STATUS)
            put("custom_consent_status", status)
        }
        get(ConsentManagerConstants.CONSENT_CATEGORIES)?.let { categories ->
            remove(ConsentManagerConstants.CONSENT_CATEGORIES)
            put("custom_consent_categories", categories)
        }
    }
}
```

次の例では、送信される同意ログイベント名をカスタマイズします。   
```java
class CustomPolicy(
        val superPolicy: ConsentManagementPolicy
) : ConsentManagementPolicy by superPolicy {
    override val consentLoggingEventName: String
        get() {
            return when(userConsentPreferences.consentStatus) {
                ConsentStatus.CONSENTED -> "user_consented"
                ConsentStatus.NOT_CONSENTED -> "user_not_consented"
                ConsentStatus.UNKNOWN -> "user_consent_unknown"
            }
        }
}
```

次の例では、サードパーティの同意値を返します。ここで、`thirdPartyConsentProvider` は別の同意プロバイダーへの参照です。   
```java
class CustomPolicy(
        val superPolicy: ConsentManagementPolicy,
        val thirdPartyConsentLibrary: OtherConsentProvider
) : ConsentManagementPolicy by superPolicy {
    override fun policyStatusInfo(): Map<String, Any> {
        val status = thirdPartyConsentLibrary
                .getConsent(userConsentPreferences.consentStatus == ConsentStatus.CONSENTED)
        return mapOf("my_consent_status" to status)
    }
}
```