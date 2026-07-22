---
title: 同意管理
description: iOS（Swift）での同意管理の実装方法を学びます。
url: https://docs.tealium.com/ja/platforms/ios-swift/consent-management/
---
## 使用方法

同意管理モジュールは、細かいレベルでのトラッキング同意を管理するためのシンプルなAPIを提供します。これは、すべてのAppleプラットフォーム（iOS、iPadOS、tvOS、watchOS、macOS、macOS Catalyst）でサポートされています。

Tealium Swiftライブラリのバージョン2.xでは、同意管理モジュールに重要な変更が導入されています：

* 同意管理はデフォルトで無効（有効にするには[完全同意](#full-consent)を参照）
* `TealiumCore`モジュールに同意管理が組み込まれています
* CCPAのサポートが導入されました
* 同意の有効期限オプション

[同意管理](https://docs.tealium.com/ja/platforms/getting-started-mobile/consent-management/)と同意ポリシーについてもっと学びましょう。

## 同意

### ポリシーの構成

初期化時に以下のいずれかを構成して同意ポリシーを構成します：

* `.gdpr`
* `.ccpa`

同意管理モジュールはコアライブラリに含まれており、同意ポリシーが構成されるまでアクティブになりません。


<blockquote>
任意の時点でデバイスに強制できるポリシーは1つだけです。
</blockquote>


GDPRポリシーを構成するには：

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

同意ステータスが変更されるたびに生成される同意ログイベントを構成するには：
```swift
config.consentLoggingEnabled = true
```

### 同意の有効期限

[`consentExpiry`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#consentexpiry)プロパティを使用して、同意選択の有効期限を構成します。

以下の例では、同意管理ポリシーをGDPRに構成し、有効期限を90日に構成しています：

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

同意が期限切れになった場合にコールバックをトリガーするには、[`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/)オブジェクトにコールバックを定義します：

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
または、[`TealiumConsentManager`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-consent-manager/)オブジェクトにコールバックを定義します：

```swift
tealium = Tealium(config: config) { [weak self] _ in
	self?.tealium?.consentManager?.onConsentExpiration = {
		print("Consent expired")
	}
}
```

### 完全同意の構成

完全同意を構成するには：
```swift
func grantFullConsent() {
	self.tealium?.consentManager?.userConsentStatus = .consented
}
```

### カテゴリ別の部分同意の構成

部分同意を構成するには、同意カテゴリのサブセットを指定します。これにより、暗黙的に[`userConsentStatus`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-consent-manager/#userconsentstatus)が`.consented`に構成されます。
```swift
func grantPartialConsent(categories: [TealiumConsentCategories]) {
	self.tealium?.consentManager?.userConsentCategories = categories
}
```

使用例：`grantPartialConsent([.analytics, .cdp])`（パラメータカテゴリを参照）

### 同意の拒否

同意を拒否するには、同意ステータスを構成します：
```swift
func declineConsent() {
	self.tealium?.consentManager?.userConsentStatus = .notConsented
}
```

## カスタム同意

組織の同意要件が標準のGDPRおよびCCPAポリシーに含まれていない場合、カスタム同意ポリシーを作成します。

1. `ConsentPolicy`プロトコルを実装します。
```swift
class SomeCustomConsentPolicy: ConsentPolicy {
      // メソッドを実装...
}
```

2. `TealiumConfig`オブジェクトの[`consentPolicy`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#consentpolicy)プロパティに新しいカスタムポリシーを構成します。`TealiumConsentPolicy.custom`列挙型を関連付けたタイプで使用します。
```swift
config.consentPolicy = .custom(SomeCustomConsentPolicy.self)
```

カスタム同意ポリシーが実装された後、必要に応じて`ConsentPolicy`で利用可能な以下のプロパティをオーバーライドします：

| プロパティ | タイプ | 説明 |
| ---- | ---- | ---- |
| `name` | `String` | `ConsentPolicy`の名前 |
| `consentPolicyStatusInfo` | `[String: Any]?`| 戻り値：各`TealiumDispatch`のペイロードに追加されるキー値データの`[String: Any]` |
| `consentTrackingEventName` | `String` | 同意の変更をログに記録する際に使用するイベント名（キー：`tealium_event`）を構成します |
| `defaultConsentExpiry` | `(time: Int, unit: TimeUnit)` | この`ConsentPolicy`のデフォルトの有効期限を構成します |
| `preferences` | `UserConsentPreferences` | `ConsentManager`によって構成が変更されるたびに自動的に更新される現在の`UserConsentPreferences` |
| `shouldLogConsentStatus` | `Bool` | 同意の変更のログ記録が必要かどうかを構成します |
| `shouldUpdateConsentCookie` | `Bool` | TagManagementモジュールのウェブビューでクッキーを更新するかどうかを構成します |
| `trackAction` | `TealiumConsentTrackAction`| 同意ステータスに基づくトラッキングアクション（許可、禁止、キュー） |
| `updateConsentCookieEventName` | `String` | `shouldUpdateConsentCookie`がtrueに構成されている場合に使用するイベント名を構成します |

以下はカスタム同意ポリシーの完全な例です：

```swift
class MyCustomConsentPolicy: ConsentPolicy {

    var preferences: UserConsentPreferences

    required init(_ preferences: UserConsentPreferences) {
        this.preferences = preferences
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
/// ... その他の構成オプション
tealium = Tealium(config: config)
```

`GDPRConsentPolicyCreatable`または`CCPAConsentPolicyCreatable`プロトコルに準拠するカスタムポリシーを作成します。カスタムポリシーを作成し、オーバーライドしたいものをオーバーライドした後、`config.consentPolicy`を`.custom(YourCustomPolicy.self)`に構成します。
### 例

既存のGDPR実装を使用して、ポリシーの名前をオーバーライドする（トラッキングペイロードの `policy` 値をオーバーライドします）：
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

Tealium EventStreamの固定同意値を避けるためにポリシーデータキーを再マッピングする：
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

送信される同意ログイベント名をカスタマイズする：
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

代わりに第三者の同意値を返す場合、`thirdPartyConsentProvider` が別の同意プロバイダーを参照している場合：
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

次の例は、ユーザーに同意ポリシーに同意または拒否するオプションを与える方法を示しています。ユーザーが同意または拒否すると、選択した同意ポリシーのルールが有効になります。[同意ポリシー](https://docs.tealium.com/ja/platforms/getting-started-mobile/consent-management/#consent-policies)についてもっと学びましょう。

```swift
func setConsentStatusSimple(_ consented: Bool) {
    let status: TealiumConsentStatus = consented ? .consented: .notConsented
    self.tealium?.consentManager?.userConsentStatus = status
}
```

Tealium Helperクラスでこのメソッドを定義し、呼び出して、アプリユーザーがトラッキングに同意または拒否したときに使用します。ユーザーがトラッキングに同意すると、同意マネージャーは自動的にすべてのトラッキングカテゴリにユーザーを含めます。

![](https://docs.tealium.com/images/platforms/ios-swift/simple-consent)

### カテゴリ別の部分同意（GDPR）

カテゴリベースの同意では、ユーザーはカテゴリの完全なリストから各カテゴリを明示的に選択する必要があります。

次のヘルパーメソッドは、[`TealiumConsentManager`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-consent-manager/) APIのメソッドを呼び出します：
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

カテゴリのリストを更新するには：
```swift
func setUserConsentPreferences(_ categories: [String]){
	let settingsDict: [String: Any] = ["consentStatus": "consented", "consentCategories": categories]
	updateConsentPreferences(settingsDict)
}
```

#### カテゴリグループ（GDPR）

カテゴリベースの同意モデルでは、トラッキングカテゴリは、顧客によって定義された少数の高レベルのカテゴリにグループ化されます。

たとえば、Tealiumの同意カテゴリ `"big_data"`, `"analytics"`, `"monitoring"` を `"performance"` という単一のカテゴリにグループ化することを選択するかもしれません。これは、ユーザーがカテゴリの完全なリストから選択するよりも簡単かもしれません。最も許可されていないものから最も許可されているものまでの範囲のスライダーインターフェースでこれを表現することを選択するかもしれません。

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

次のヘルパー関数は、カテゴリのグループを定義し、ユーザーの同意構成を構成します：

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

当社のライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れるために、Tealium for Swift [consent manager sample app](https://github.com/Tealium/tealium-swift/tree/master/samples/ConsentManagerDemo)を探索してください。

![](https://docs.tealium.com/images/platforms/ios-swift/category-based)