---
title: 同意管理
description: iOS（Swift）での同意管理の実装方法を学びます。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/consent-management/
---
<blockquote>
これはiOS（Swift）用Tealiumの以前のバージョン（1.x）です。最新バージョンについては、[iOS（Swift）用Tealium 2.x](https://docs.tealium.com/ja/platforms/ios-swift/)をご覧ください。
</blockquote>


## 使用方法

同意管理モジュールは、追跡同意を詳細に管理するためのシンプルなAPIを提供します。CocoaPodsの依存関係またはCarthageフレームワークを含めている場合、同意管理はデフォルトで有効になっており、APIにユーザーが追跡に同意したことを明示的に通知するまで追跡呼び出しは送信されません。

このモジュールの使用は推奨されており、CarthageおよびCocoaPodsフレームワークビルドに自動的に含まれ、有効になっています。Foundationフレームワークは外部依存関係です。

サポートされているプラットフォームには、iOS、macOS、tvOS、およびwatchOSが含まれます。

[同意管理についてもっと学ぶ](https://docs.tealium.com/ja/platforms/getting-started-mobile/consent-management/)。




## サンプルアプリ

当社のライブラリ、追跡方法、およびベストプラクティスの実装に慣れるために、Tealium for Swift同意マネージャー[サンプルアプリ](https://github.com/Tealium/tealium-swift/tree/master/samples/ConsentManagerDemo)を探索してください。


## 無効化

同意管理を無効にするには、初期化時に[TealiumConfig](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/)オブジェクトの無効化モジュールリストに含めてください。


## データレイヤー

モジュールが有効な間に各追跡呼び出しで送信される変数は以下の通りです：

| 変数名 | 説明 | 例  |
| --- | --- | --- |
| `policy` | 同意が収集されたポリシー（デフォルト：`gdpr`） | `gdpr` |
| `consent_status` | ユーザーの現在の同意状態 | [`consented`, `notConsented`] |
| `consent_categories` | ユーザーが選択した同意カテゴリの配列 | [`"analytics"`, `"cdp"`] |


## 例

以下の例コードは、同意マネージャーにアクセスする方法を示しています。

```swift
class TealiumHelper {
	var tealium: Tealium?
	// ...
	private func initTealium() {
		let config = TealiumConfig(account: "ACCOUNT",
 	       		                 profile: "PROFILE",
        	   	                 environment: "ENVIRONMENT",
           		                 datasource: "DATASOURCE")

		// 初期状態をnotConsentedに構成します。送信されたすべてのイベントは削除されます。
		// config.initialUserConsentStatus = .notConsented
		// 初期状態をconsentedに構成します。同意状態が.notConsentedに変更されるまですべてのイベントが即座に送信されます。
		// config.initialUserConsentStatus = .consented

		// 初期状態をunknown（デフォルト）に構成します。同意状態が変更されるまですべてのイベントがキューに入れられます。
		config.initialUserConsentStatus = .unknown
		// trueの場合、同意状態が変更されるたびに同意ログイベントが生成されます。
		config.consentLoggingEnabled = false

		self.tealium = Tealium(config: config)

		// ...
	}

	// 全カテゴリに完全同意を与えます。
	func grantFullConsent() {
		self.tealium?.consentManager()?.setUserConsentStatus(.consented)
	}

	/// 特定のカテゴリに部分的に同意を与えます
	/// 使用例：`grantPartialConsent([.analytics, .cdp])`
	/// - パラメータ categories: `[TealiumConsentCategories]`。
	func grantPartialConsent(categories: [TealiumConsentCategories]) {
		self.tealium?.consentManager()?.setUserConsentStatusWithCategories(status: .consented, categories: categories)
	}

	// 同意を拒否します。今後のすべてのイベントは削除されます。
	func declineConsent() {
		self.tealium?.consentManager()?.setUserConsentStatus(.notConsented)
	}

}
```

## 使用例

### シンプルなオプトイン

この例では、ユーザーにシンプルな「オプトイン/オプトアウト」オプションを提供する方法を示しています。ユーザーが同意した場合、自動的にすべての追跡カテゴリにオプトインされます。同意を取り消した場合、アクティブなカテゴリは残らず、追跡呼び出しは送信されません。

```swift
func setConsentStatusSimple(_ consented: Bool) {
    let status: TealiumConsentStatus = consented ? .consented: .notConsented
    self.tealium?.consentManager()?.setUserConsentStatus(status)
}
```

Tealium Helperクラスで、アプリユーザーが追跡に同意または拒否したときに次のメソッドを定義して呼び出します。ユーザーが追跡に同意した場合、同意マネージャーは自動的にすべての追跡カテゴリにオプトインします。

![](https://docs.tealium.com/images/platforms/ios-swift/simple-consent)

### グループ化されたオプトイン

この例では、追跡カテゴリをより少ない数の上位カテゴリにグループ化するカテゴリベースの同意モデルを示しています。

たとえば、Tealiumの同意カテゴリ`"big_data"`, `"analytics"`, `"monitoring"`を`"performance"`という単一のカテゴリにグループ化することを選択するかもしれません。これは、ユーザーがカテゴリの完全なリストから選択するよりも簡単かもしれません。最も許可されていないものから最も許可されているもの（すべてのカテゴリ）までの範囲でスライダーインターフェースでこれを表現することを選択するかもしれません。

```swift
func updateConsentPreferences(_ dict: [String: Any]) {
    if let status = dict["consentStatus"] as? String {
        var tealiumConsentCategories = [TealiumConsentCategories]()
        let tealiumConsentStatus = (status == "consented") ? TealiumConsentStatus.consented : TealiumConsentStatus.notConsented
        if let categories = dict["consentCategories"] as? [String] {
            tealiumConsentCategories = TealiumConsentCategories.consentCategoriesStringArrayToEnum(categories)
        }
        self.tealium?.consentManager()?.setUserConsentStatusWithCategories(status: tealiumConsentStatus, categories: tealiumConsentCategories)
    }
}

// カテゴリのグループを定義し、consentManager APIで同意構成を構成する例関数。
// ユーザーが構成を保存するときにこの関数を呼び出します。
func setUserConsentPreferences(){
	// グループ化されたカテゴリを含む辞書を定義します。
	let consentGroups = ["Off" : [],
	        "Performance": ["analytics", "monitoring", "big_data", "mobile", "crm"],
	        "Marketing": ["analytics", "monitoring", "big_data", "mobile", "crm", "affiliates", "email", "search", "engagement", "cdp"],
	        "Personalized Advertising": ["analytics", "monitoring", "big_data", "mobile", "crm", "affiliates", "email", "search", "engagement", "cdp", "display_ads", "personalization", "social", "cookiematch", "misc"]]

	// これは実際のアプリでは通常動的ですが、ユーザーが選択した構成レベルです。
	let userSelection = "Marketing"

	if let userList = consentGroups[userSelection] {
	  let settingsDict: [String: Any] = ["consentStatus": "consented", "consentCategories": userList]

	  updateConsentPreferences(settingsDict)
	}
}
```

![](https://docs.tealium.com/images/platforms/ios-swift/grouped-gif.gif)
### カテゴリーベースのオプトイン

この例では、ユーザーが全カテゴリーのリストから明示的に各カテゴリーを選択する必要があるカテゴリーベースの同意モデルを示しています。デフォルト状態は`"Unknown"`で、ユーザーが同意を提供するまでヒットをキューに入れます。ユーザーが任意のカテゴリーに同意すると、イベントはキューから出され、同意したカテゴリーのデータが各トラッキングコールに追加されます。

```swift
// Tealium consentManager APIを呼び出すヘルパーメソッド
func updateConsentPreferences(_ dict: [String: Any]) {
    if let status = dict["consentStatus"] as? String {
        var tealiumConsentCategories = [TealiumConsentCategories]()
        let tealiumConsentStatus = (status == "consented") ? TealiumConsentStatus.consented : TealiumConsentStatus.notConsented
        if let categories = dict["consentCategories"] as? [String] {
            tealiumConsentCategories = TealiumConsentCategories.consentCategoriesStringArrayToEnum(categories)
        }
        self.tealium?.consentManager()?.setUserConsentStatusWithCategories(status: tealiumConsentStatus, categories: tealiumConsentCategories)
    }
}

// Tealium consentManager APIにカテゴリーリストを渡す例示関数
func setUserConsentPreferences(_ categories: [String]){

	let settingsDict: [String: Any] = ["consentStatus": "consented", "consentCategories": categories]
	updateConsentPreferences(settingsDict)
}
```

![](https://docs.tealium.com/images/platforms/ios-swift/category-based)