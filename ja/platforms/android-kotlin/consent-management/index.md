---
title: 同意管理
description: Android Kotlinの同意管理の実装方法を学びます。
url: https://docs.tealium.com/ja/platforms/android-kotlin/consent-management/
---
## 使用法

同意管理モジュールは推奨され、初期化時に自動的に有効化されます。AndroidモバイルとAndroid TVでサポートされています。

[`TealiumConfig`](/ja/platforms/android-kotlin/api/tealium-config/#consentmanagerpolicy)内で同意管理ポリシーを初期化します。その後、[`tealium.consentManager`](/ja/platforms/android-kotlin/api/tealium/#consentmanager)のTealiumインスタンスを使用してユーザーの同意を管理します。

[同意管理](/ja/platforms/getting-started-mobile/consent-management/)と同意ポリシーについて詳しく学びましょう。

## 同意

### ポリシーの構成

初期化時に同意ポリシーを以下のいずれかに構成します：

* `ConsentPolicy.GDPR`
* `ConsentPolicy.CCPA`

一度に一つのポリシーしかデバイスに適用できません。

```java
val config = TealiumConfig(...).apply {
  consentManagerPolicy = ConsentPolicy.GDPR
}
```

### 同意の有効期限

[`consentExpiry`](/ja/platforms/android-kotlin/api/tealium-config/#consentexpiry)プロパティを使用して、同意選択の有効期限を構成します。

以下の例では、同意管理ポリシーをGDPRに構成し、有効期限を90日に構成しています：

```java
val config = TealiumConfig(...).apply {
  consentManagerPolicy = ConsentPolicy.GDPR
  consentExpiry = ConsentExpiry(90, TimeUnit.DAYS)
}
```

同意が期限切れになったときにコールバックをトリガーするには、[`onUserConsentPreferencesUpdated()`](/ja/platforms/android-kotlin/api/consent-manager/#onuserconsentpreferencesupdated)メソッドを使用して`ConsentStatus`が`UNKNOWN`になったときを確認します：

```java
Tealium.create(BuildConfig.TEALIUM_INSTANCE, config) {
    events.subscribe(object : UserConsentPreferencesUpdatedListener {
        override fun onUserConsentPreferencesUpdated(userConsentPreferences: UserConsentPreferences,
                                                     policy: ConsentManagementPolicy) {
            if (userConsentPreferences.consentStatus == ConsentStatus.UNKNOWN) {
                Logger.dev(BuildConfig.TAG, &#34;Re-prompt for consent&#34;)
            }
        }
    })
}
```

### 全面的な同意の構成

全面的な同意を構成するには：

```java
tealium.consentManager.userConsentStatus = ConsentStatus.CONSENTED
```

全面的な同意を構成すると、暗黙的に同意カテゴリが利用可能な[`ConsentCategory`](/ja/platforms/android-kotlin/api/consent-category/#class-consentcategory)タイプの全リストに構成されます。

### カテゴリ別の部分的な同意の構成

部分的な同意を構成するには、同意カテゴリのサブセットを指定します。これにより、[`userConsentStatus`](/ja/platforms/android-kotlin/api/consent-manager/#userconsentstatus)が`CONSENTED`に暗黙的に構成されます。

```java
tealium.consentManager.userConsentCategories = setOf(ConsentCategory.ANALYTICS, ConsentCategory.EMAIL)
```

### 同意の拒否の構成

同意を拒否するには、同意ステータスを構成します：  
```java
tealium.consentManager.userConsentStatus = ConsentStatus.NOT_CONSENTED
```

あるいは、同意カテゴリを`null`に構成します。

## カスタム同意

あなたの組織の同意要件が、私たちの標準的な[Opt-in](/ja/glossary/#opt-in-model-consent)および[Opt-out](/ja/glossary/#opt-out-model-consent)同意管理ポリシーによってカバーされていない場合、カスタム同意ポリシーを作成します。

1. `ConsentManagementPolicy`インターフェースを実装します。      
      ```java
      val customPolicy = object: ConsentManagementPolicy {
            //implement methods...
      }
      ```
2. `setCustomPolicy()`メソッドを使用して、`ConsentPolicy.CUSTOM`列挙型に`ConsentManagementPolicy`の実装を渡します。      
      ```java
      ConsentPolicy.CUSTOM.setCustomPolicy(customPolicy)
      ```
3. [`consentManagerPolicy`](/ja/platforms/android-kotlin/api/tealium-config/#consentmanagerpolicy)プロパティを介して`TealiumConfig`オブジェクトに`ConsentPolicy.CUSTOM`オプションを渡します。   
      ```java
      config.consentManagerPolicy = ConsentPolicy.CUSTOM
      ```

カスタム`ConsentManagementPolicy`の実装は、提供された`superPolicy`に既存の同意管理メソッドとプロパティを委任することができ、それぞれのイベントで`policy`キーを自身の名前で上書きします。

```java
class CustomPolicy(
        val superPolicy: ConsentManagementPolicy
        ) : ConsentManagementPolicy by superPolicy {
    override val name: String = &#34;custom_policy&#34;

    override fun policyStatusInfo(): Map&lt;String, Any&gt; {
        return superPolicy.policyStatusInfo().toMutableMap().apply {
            put(ConsentManagerConstants.CONSENT_POLICY, name)
        }
    }
}

val customPolicy = CustomPolicy(ConsentPolicy.GDPR.create(
    UserConsentPreferences(ConsentStatus.UNKNOWN, null)))
```

カスタム同意ポリシーが実装された後、必要に応じて`ConsentManagementPolicy`で利用可能な以下のプロパティとメソッドを上書きします：

| プロパティ / メソッド | タイプ | 説明 |
| ----- | ------ | ----- |
| `name` | `String` | `ConsentManagementPolicy`の名前|
| `userConsentPreferences` | `UserConsentPreferences` | プリファレンスが変更されたときに`ConsentManager`によって自動的に更新される現在の`UserConsentPreferences`|
| `consentLoggingEnabled` | `Boolean` | 同意の変更のログ記録が必要かどうかを構成します |
| `consentLoggingEventName` | `String` | 同意の変更をログに記録するときに使用するイベント名（キー：`tealium_event`）を構成します |
| `defaultConsentExpiry`] |`ConsentExpiry` | `ConsentManagementPolicy`のデフォルトの有効期限を構成します |
| `cookieUpdateRequired`| `Boolean` | TagManagementモジュールのwebview内のクッキーを更新するかどうかを構成します|
| `cookieUpdateEventName` |  `String` | `cookieUpdateRequired`が`true`に構成されているときに使用するイベント名を構成します|
| `policyStatusInfo()` |`Map&lt;String, Any&gt;` | 各ディスパッチのペイロードに追加するキー値データのマップを返します |
| `shouldQueue()` | `Boolean` | `ConsentPolicy`のルールに従ってディスパッチをキューに入れるかどうかを返します|
| `shouldDrop()`| `Boolean` | `ConsentPolicy`のルールに従ってディスパッチをドロップするかどうかを返します|

### 例

以下の例では、ポリシーデータキーを再マップして、Tealium EventStreamの固定同意値を避けます：   
```java
class CustomPolicy(
        val superPolicy: ConsentManagementPolicy
) : ConsentManagementPolicy by superPolicy {
    return superPolicy.policyStatusInfo().toMutableMap().apply {
        get(ConsentManagerConstants.CONSENT_STATUS)?.let { status -&gt;
            remove(ConsentManagerConstants.CONSENT_STATUS)
            put(&#34;custom_consent_status&#34;, status)
        }
        get(ConsentManagerConstants.CONSENT_CATEGORIES)?.let { categories -&gt;
            remove(ConsentManagerConstants.CONSENT_CATEGORIES)
            put(&#34;custom_consent_categories&#34;, categories)
        }
    }
}
```

以下の例では、送信される同意ログイベント名をカスタマイズします：   
```java
class CustomPolicy(
        val superPolicy: ConsentManagementPolicy
) : ConsentManagementPolicy by superPolicy {
    override val consentLoggingEventName: String
        get() {
            return when(userConsentPreferences.consentStatus) {
                ConsentStatus.CONSENTED -&gt; &#34;user_consented&#34;
                ConsentStatus.NOT_CONSENTED -&gt; &#34;user_not_consented&#34;
                ConsentStatus.UNKNOWN -&gt; &#34;user_consent_unknown&#34;
            }
        }
}
```

以下の例では、`thirdPartyConsentProvider`が別の同意プロバイダーへの参照である場合、サードパーティの同意値を返します：   
```java
class CustomPolicy(
        val superPolicy: ConsentManagementPolicy,
        val thirdPartyConsentLibrary: OtherConsentProvider
) : ConsentManagementPolicy by superPolicy {
    override fun policyStatusInfo(): Map&lt;String, Any&gt; {
        val status = thirdPartyConsentLibrary
                .getConsent(userConsentPreferences.consentStatus == ConsentStatus.CONSENTED)
        return mapOf(&#34;my_consent_status&#34; to status)
    }
}
```

