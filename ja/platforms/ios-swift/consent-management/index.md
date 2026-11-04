---
title: 同意管理
description: iOS（Swift）向けの同意管理を実装する方法について説明します。
url: https://docs.tealium.com/ja/platforms/ios-swift/consent-management/
---
## 使用方法

同意管理モジュールは、トラッキングへの同意を詳細なレベルで管理するためのシンプルなAPIを提供します。すべてのAppleプラットフォーム（iOS、iPadOS、tvOS、watchOS、macOS、macOS Catalyst）でサポートされています。

Tealium Swiftライブラリのバージョン2.xでは、同意管理モジュールに以下の重要な変更が導入されています。

* 同意管理はデフォルトで無効（有効にするには[完全な同意](#full-consent)を参照）
* 同意管理を`TealiumCore`モジュールに統合
* CCPAのサポートを導入
* 同意の有効期限オプション

[同意管理](https://docs.tealium.com/ja/platforms/getting-started-mobile/consent-management/)および同意ポリシーの詳細について確認してください。

## 同意

### ポリシーの構成

初期化時に、同意ポリシーを以下のいずれかに構成します。

* `.gdpr`
* `.ccpa`

同意管理モジュールはコアライブラリに含まれていますが、同意ポリシーが構成されるまで有効になりません。


<blockquote>
1台のデバイスで同時に適用できるポリシーは1つだけです。
</blockquote>


GDPRポリシーを構成するには、次のようにします。  

```swift
class TealiumHelper {
	var tealium: Tealium?

	private func initTealium() {
		let config = TealiumConfig(...)
		config.consentPolicy = .gdpr
    //...
	}
}
```

同意ステータスが変更されるたびに生成される同意ログイベントを構成するには、次のようにします。  

```swift
config.consentLoggingEnabled = true
```

### 同意の有効期限

[`consentExpiry`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#consentexpiry)プロパティを使用して、同意の選択内容の有効期限を構成します。

以下の例では、同意管理ポリシーをGDPRに構成し、有効期限を90日に構成しています。

```swift
class TealiumHelper {
	var tealium: Tealium?

	private func initTealium() {
		let config = TealiumConfig(...)
		config.consentPolicy = .gdpr
		config.consentExpiry = (90, .days)
    //...
	}
}
```

同意の有効期限が切れたときにコールバックを実行するには、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/)オブジェクトにコールバックを定義します。

```swift
class TealiumHelper {
	var tealium: Tealium?

	private func initTealium() {
		let config = TealiumConfig(...)
		config.consentPolicy = .gdpr
		config.consentExpiry = (90, .days)
		config.onConsentExpiration = {
       	print("Consent expired")
       }
    //...
	}
}
```

または、[`TealiumConsentManager`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-consent-manager/)オブジェクトにコールバックを定義します。

```swift
tealium = Tealium(config: config) { [weak self] _ in
	self?.tealium?.consentManager?.onConsentExpiration = {
		print("Consent expired")
	}
}
```

### 完全な同意の構成

完全な同意を構成するには、次のようにします。  

```swift
func grantFullConsent() {
	self.tealium?.consentManager?.userConsentStatus = .consented
}
```

### カテゴリ別の部分的な同意の構成

部分的な同意を構成するには、同意カテゴリのサブセットを指定します。これにより、[`userConsentStatus`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-consent-manager/#userconsentstatus)が暗黙的に`.consented`に構成されます。   

```swift
func grantPartialConsent(categories: [TealiumConsentCategories]) {
	self.tealium?.consentManager?.userConsentCategories = categories
}
```

使用例：`grantPartialConsent([.analytics, .cdp])`（パラメータのカテゴリを参照）

### 同意拒否の構成

同意を拒否するには、同意ステータスを構成します。  

```swift
func declineConsent() {
	self.tealium?.consentManager?.userConsentStatus = .notConsented
}
```

## カスタム同意

組織の同意要件が標準のGDPRおよびCCPAポリシーで対応できない場合は、カスタム同意ポリシーを作成します。

1. `ConsentPolicy`プロトコルを実装します。   

```swift
class SomeCustomConsentPolicy: ConsentPolicy {
      // implement methods...
}
```

2. 関連型を持つ`TealiumConsentPolicy.custom`列挙型を使用して、`TealiumConfig`オブジェクトの[`consentPolicy`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#consentpolicy)プロパティに新しいカスタムポリシーを構成します。   

```swift
config.consentPolicy = .custom(SomeCustomConsentPolicy.self)
```

カスタム同意ポリシーを実装した後、必要に応じて`ConsentPolicy`で使用可能な以下のプロパティをオーバーライドします。

| プロパティ | 型 | 説明 |
| ---- | ---- | ---- |
| `name` | `String` | `ConsentPolicy`の名前 |
| `consentPolicyStatusInfo` | `[String: Any]?` | 各`TealiumDispatch`のペイロードに追加するキーと値のデータを`[String: Any]`として返します |
| `consentTrackingEventName` | `String` | 同意の変更を記録するときに使用するイベント名（キー：`tealium_event`）を構成します |
| `defaultConsentExpiry` | `(time: Int, unit: TimeUnit)` | この`ConsentPolicy`のデフォルトの有効期限を構成します |
| `preferences` | `UserConsentPreferences` | 現在の`UserConsentPreferences`。構成が変更されると、`ConsentManager`によって自動的に更新されます |
| `shouldLogConsentStatus` | `Bool` | 同意の変更を記録する必要があるかどうかを構成します |
| `shouldUpdateConsentCookie` | `Bool` | TagManagementモジュールのWebView内にあるCookieを更新するかどうかを構成します |
| `trackAction` | `TealiumConsentTrackAction` | 同意ステータスに基づくトラッキングアクション（許可、禁止、キューへの追加） |
| `updateConsentCookieEventName` | `String` | `shouldUpdateConsentCookie`がtrueに構成されている場合に使用するイベント名を構成します |

以下は、カスタム同意ポリシーの完全な例です。  

```swift
class MyCustomConsentPolicy: ConsentPolicy {

    var preferences: UserConsentPreferences

    required init(_ preferences: UserConsentPreferences) {
        self.preferences = preferences
    }

    var name: String = "my custom policy"

    var defaultConsentExpiry: (time: Int, unit: TimeUnit) = (90, .days)

    var shouldUpdateConsentCookie: Bool = false

    var updateConsentCookieEventName: String = "custom_consent_update"

    var consentPolicyStatusInfo: [String : Any]? {
        ["custom_consent_status": preferences.consentStatus.rawValue,
         "custom_consent_categories": preferences.consentCategories?.map({ $0.rawValue }),
         "custom_policy_key": name]
    }

    var trackAction: TealiumConsentTrackAction  = .trackingAllowed

    var consentTrackingEventName: String = "custom_consent_update"

    var shouldLogConsentStatus: Bool = true

}
var tealium: Tealium?
let config = TealiumConfig(...)
config.consentPolicy = .custom(MyCustomConsentPolicy.self)
/// ... other configuration options
tealium = Tealium(config: config)
```

`GDPRConsentPolicyCreatable`または`CCPAConsentPolicyCreatable`プロトコルのいずれかに準拠するカスタムポリシーを作成します。カスタムポリシーを作成し、必要な項目をオーバーライドした後、`config.consentPolicy`を`.custom(YourCustomPolicy.self)`に構成します。
### 例

既存の GDPR 実装を使用しつつ、ポリシー名をオーバーライドします（トラッキングペイロードの `policy` 値をオーバーライドします）。   
```swift
class CustomGDPRConsentPolicy: GDPRConsentPolicyCreatable {

    var preferences: UserConsentPreferences

    required init(_ preferences: UserConsentPreferences) {
        self.preferences = preferences
    }

    var name: String {
        "customGDPRPolicy"
    }

}

config.consentPolicy = .custom(CustomGDPRConsentPolicy.self)
```

Event Streaming の固定された同意値を回避するため、ポリシーデータのキーを再マッピングします。   
```swift
class CustomGDPRConsentPolicy: GDPRConsentPolicyCreatable {

    var preferences: UserConsentPreferences

    required init(_ preferences: UserConsentPreferences) {
        self.preferences = preferences
    }

    var consentPolicyStatusInfo: [String : Any]? {
        ["custom_consent_status": preferences.consentStatus.rawValue,
         "custom_consent_categories": preferences.consentCategories?.map({ $0.rawValue }),
         "custom_policy_key": "customGDPRPolicy"]
    }

}
```

送信される同意ログイベントの名前をカスタマイズします。   
```swift
class CustomGDPRConsentPolicy: GDPRConsentPolicyCreatable {

    var preferences: UserConsentPreferences

    required init(_ preferences: UserConsentPreferences) {
        self.preferences = preferences
    }

    var consentTrackingEventName: String {
        switch preferences.consentStatus {
        case .consented:
            return "user_consented"
        case .notConsented:
            return "user_not_consented"
        case .unknown:
            return "user_consent_unknown"
        }
    }

}
```

`thirdPartyConsentProvider` が別の同意プロバイダーへの参照である場合は、代わりにサードパーティの同意値を返します。   
```swift
class CustomGDPRConsentPolicy: GDPRConsentPolicyCreatable {

    let thirdPartyConsentProvider = ThirdPartyProvider()
    var preferences: UserConsentPreferences

    required init(_ preferences: UserConsentPreferences) {
        self.preferences = preferences
    }

    var consentPolicyStatusInfo: [String: Any]? {
        let status = thirdPartyConsentProvider.getConsent()
        return ["my_consent_status": status]
    }

}
```


## ユースケース

### 完全な同意

次の例は、同意ポリシーに同意するか拒否するかをユーザーが選択できるようにする方法を示しています。ユーザーが同意または拒否すると、選択した同意ポリシーのルールが適用されます。詳しくは、[同意ポリシー](https://docs.tealium.com/ja/platforms/getting-started-mobile/consent-management/#consent-policies)を参照してください。

```swift
func setConsentStatusSimple(_ consented: Bool) {
    let status: TealiumConsentStatus = consented ? .consented: .notConsented
    self.tealium?.consentManager?.userConsentStatus = status
}
```

アプリのユーザーがトラッキングに同意または拒否したときに、Tealium Helper クラスでこのメソッドを定義して呼び出します。ユーザーがトラッキングに同意すると、同意マネージャーは自動的にそのユーザーをすべてのトラッキングカテゴリーに含めます。

![](https://docs.tealium.com/images/platforms/ios-swift/simple-consent)

### カテゴリー別の部分的な同意（GDPR）

カテゴリーに基づく同意では、ユーザーがカテゴリーの全リストから各カテゴリーを明示的に選択する必要があります。

次のヘルパーメソッドは、[`TealiumConsentManager`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-consent-manager/) API のメソッドを呼び出します。  
```swift
func updateConsentPreferences(_ dict: [String: Any]) {
      var tealiumConsentCategories = [TealiumConsentCategories]()
        if let categories = dict["consentCategories"] as? [String] {
            tealiumConsentCategories = TealiumConsentCategories.consentCategoriesStringArrayToEnum(categories)
            tealium.consentManager?.userConsentCategories = tealiumConsentCategories
        } else if let status = dict["consentStatus"] as? String {
            let tealiumConsentStatus = (status == "consented") ? TealiumConsentStatus.consented : TealiumConsentStatus.notConsented
            self.tealium?.consentManager?.consentStatus = status
        }
    }
}
```

カテゴリーのリストを更新するには、次のようにします。  
```swift
func setUserConsentPreferences(_ categories: [String]){
	let settingsDict: [String: Any] = ["consentStatus": "consented", "consentCategories": categories]
	updateConsentPreferences(settingsDict)
}
```

#### カテゴリーグループ（GDPR）

カテゴリーに基づく同意モデルでは、トラッキングカテゴリーは、顧客が定義した少数の上位カテゴリーにグループ化されます。

たとえば、Tealium の同意カテゴリーである `"big_data"`、`"analytics"`、`"monitoring"` を、`"performance"` という単一のカテゴリーにまとめることができます。ユーザーにとっては、カテゴリーの全リストから選択するよりも簡単な場合があります。これを、最も制限の厳しい構成から最も制限の緩い構成（すべてのカテゴリー）までを範囲とするスライダーインターフェイスで表現することもできます。

```swift
func updateConsentPreferences(_ dict: [String: Any]) {
      var tealiumConsentCategories = [TealiumConsentCategories]()
        if let categories = dict["consentCategories"] as? [String] {
            tealiumConsentCategories = TealiumConsentCategories.consentCategoriesStringArrayToEnum(categories)
            tealium.consentManager?.userConsentCategories = tealiumConsentCategories
        } else if let status = dict["consentStatus"] as? String {
            let tealiumConsentStatus = (status == "consented") ? TealiumConsentStatus.consented : TealiumConsentStatus.notConsented
            self.tealium?.consentManager?.consentStatus = status
        }
    }
}
```

次のヘルパー関数は、カテゴリーのグループを定義し、ユーザーの同意構成を指定します。  

```swift
func setUserConsentPreferences(){
	let consentGroups = ["Off" : [],
	        "Performance": ["analytics", "monitoring", "big_data", "mobile", "crm"],
	        "Marketing": ["analytics", "monitoring", "big_data", "mobile", "crm", "affiliates", "email", "search", "engagement", "cdp"],
	        "Personalized Advertising": ["analytics", "monitoring", "big_data", "mobile", "crm", "affiliates", "email", "search", "engagement", "cdp", "display_ads", "personalization", "social", "cookiematch", "misc"]]

	let userSelection = "Marketing"

	if let userList = consentGroups[userSelection] {
	  let settingsDict: [String: Any] = ["consentStatus": "consented", "consentCategories": userList]

	  updateConsentPreferences(settingsDict)
	}
}
```

![](https://docs.tealium.com/images/platforms/ios-swift/grouped-gif.gif)

## サンプルアプリ

Tealium のライブラリ、トラッキングメソッド、実装のベストプラクティスについて理解を深めるには、Tealium for Swift の[同意マネージャーサンプルアプリ](https://github.com/Tealium/tealium-swift/tree/master/samples/ConsentManagerDemo)を参照してください。

![](https://docs.tealium.com/images/platforms/ios-swift/category-based)