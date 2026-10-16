---
title: 同意
description: Tealium Prism SDKで同意管理を実装します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/consent-management/
---
このページでは、Prismとあなたの同意管理プロバイダー（CMP）を統合する方法について説明します。


<blockquote>
同意統合はまだReact Native SDKで利用できません。
</blockquote>


## 動作原理

同意統合を有効にすると、SDKはディスパッチャーに到達する前に各イベントを傍受し、以下のように処理します：

1. イベントが追跡され、同意マネージャーに渡されます。
1. 同意決定がまだ受信されていない場合、イベントは内部キューに保持されます。
1. CMPアダプターが同意決定を発行すると、SDKはキューからイベントを取得し、各イベントに同意目的を適用します。
1. SDKは、決定にTealium目的ID（`setTealiumPurposeId`によって構成）が含まれているかどうかを確認します。含まれていない場合、SDKはすべてのディスパッチャーのすべてのイベントをドロップします。
1. 残った各イベントはディスパッチャーの構成に対して評価されます。各ディスパッチャーについて、SDKはそのディスパッチャーに必要な目的が決定に含まれているかどうかを確認します。必要な目的を満たしていないイベントはそのディスパッチャーに対してドロップされます。
1. 目的チェックを通過したイベントはディスパッチャーに送信されます。

### 暗黙的および明示的な決定

SDKが暗黙的な決定を受け取ると、必要な目的に一致するイベントをディスパッチします。これらのイベントは後で再送信（再度送信）のために保持されます。

SDKが後で明示的な決定を受け取ると、同意ビルダー構成にリストされているディスパッチャーに保持されたイベントを再送信します。これにより、明示的な同意前に送信されたイベントからのデータがキャプチャされます。

## 同意統合を有効にする

`TealiumConfig`で`enableConsentIntegration()`を呼び出して、CMPアダプターを接続します。ディスパッチャーに目的IDをマッピングするために強制同意構成を提供します。




```kotlin
import com.tealium.prism.core.api.Tealium
import com.tealium.prism.core.api.TealiumConfig
import com.tealium.prism.core.api.modules.Modules

val config = TealiumConfig.Builder(
    accountName = "my_account",
    profileName = "my_profile",
    environment = Environment.PROD,
    modules = listOf(Modules.collect())
).enableConsentIntegration(cmpAdapter) { settings ->
    settings
        .setTealiumPurposeId("tealium")
        .addPurpose("tracking", setOf(Modules.Types.COLLECT))
        .setRefireDispatcherIds(setOf(Modules.Types.COLLECT))
}.build()

val tealium = Tealium.create(config)
```


```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
#endif

var config = TealiumConfig(account: "my_account",
                           profile: "my_profile",
                           environment: "prod",
                           modules: [Modules.collect()],
                           settingsUrl: "https://tags.tiqcdn.com/dle/my_account/my_profile/settings.json")

config.enableConsentIntegration(with: cmpAdapter) { enforcedConfiguration in
    enforcedConfiguration
        .setTealiumPurposeId("tealium")
        .addPurpose("tracking", dispatcherIds: [Modules.Types.collect])
        .setRefireDispatcherIds([Modules.Types.collect])
}

let tealium = Tealium.create(config: config)
```



イベントディスパッチの前提条件：

* CMPアダプターが`ConsentDecision`を返します。
* そのアダプターに対する同意構成が見つかります。

同意がまだ利用できない場合、決定が受信されるまでイベントはキューに入れられます。

## CMPアダプターを実装する

SDKにCMPを接続するためにCMPアダプターを実装します。CMPアダプターは以下のプロパティを使用します：

| プロパティ          | タイプ     | 説明 |
| :---------------- | :------- | :---------- |
| `id`              | `String` | このアダプターのユニークな識別子。同意構成に対して照合に使用されます。 |
| `consentDecision` | `Observable<ConsentDecision?>` | ユーザーからの同意決定のオブザーバブルストリーム。 |
| `allPurposes`     | `Set<String>?` | 利用可能な場合、CMPからのすべての可能な目的。 |

`allPurposes`はオプションです。以下の例では明確さのために非nullセットを使用しています。




```kotlin
import com.tealium.prism.core.api.consent.CmpAdapter
import com.tealium.prism.core.api.consent.ConsentDecision
import com.tealium.prism.core.api.pubsub.Observable
import com.tealium.prism.core.api.pubsub.Observables
import com.tealium.prism.core.api.pubsub.StateSubject

class MyCmpAdapter : CmpAdapter {

    private val _consentDecision: StateSubject<ConsentDecision?> =
        Observables.stateSubject(null)

    override val id: String = "my_cmp"

    override val consentDecision: Observable<ConsentDecision?>
        get() = _consentDecision.asObservableState()

    override val allPurposes: Set<String> = setOf("tealium", "tracking", "functional")

    fun updateConsent(decision: ConsentDecision) {
        _consentDecision.onNext(decision)
    }
}
```


```swift
#if COCOAPODS
import TealiumPrism
#else
import TealiumPrismCore
#endif

class MyCMPAdapter: CMPAdapter {

    let id = "my_cmp"

    @ReplaySubject<ConsentDecision?>(nil)
    var consentDecision

    let allPurposes: Set<String>? = ["tealium", "tracking", "functional"]

    func updateConsent(_ decision: ConsentDecision) {
        _consentDecision.publish(decision)
    }
}
```



## 同意決定

`ConsentDecision`はユーザーの現在の同意状態を表します。それには決定タイプとユーザーが同意した目的IDのセットが含まれます。




```kotlin
import com.tealium.prism.core.api.consent.ConsentDecision

// 暗黙的：ユーザーの行動から導き出される、例えばアプリの起動
val implicitDecision = ConsentDecision(
    decisionType = ConsentDecision.DecisionType.Implicit,
    purposes = set of("tealium")
)

// 明示的：ユーザーが積極的に同意を受け入れた
val explicitDecision = ConsentDecision(
    decisionType = ConsentDecision.DecisionType.Explicit,
    purposes = set of("tealium", "tracking", "functional")
)
```


```swift
// 暗黙的：ユーザーの行動から導き出される、例えばアプリの起動
let implicitDecision = ConsentDecision(
    decisionType: .implicit,
    purposes: ["tealium"]
)

// 明示的：ユーザーが積極的に同意を受け入れた
let explicitDecision = ConsentDecision(
    decisionType: .explicit,
    purposes: ["tealium", "tracking", "functional"]
)
```



| 決定タイプ | 説明 |
| :------------ | :---------- |
| `Implicit` / `.implicit` | ユーザーの行動から導き出される、例えばアプリを開くこと。SDKは後で明示的な同意が与えられたときにイベントを再発火するためにキューに入れることがあります。 |
| `Explicit` / `.explicit` | ユーザーが積極的に同意を与えたか拒否した。SDKは更新された目的に基づいて以前にキューに入れられたイベントを処理します。 |
## 目的の構成

`ConsentConfigurationBuilder`を使用して、CMPの目的IDをディスパッチャーにマッピングし、イベントの再発火を構成します。

| メソッド | 説明 |
| :----- | :---------- |
| `setTealiumPurposeId(id)` | Tealium SDKを有効にするために必要な目的ID。決定に含まれていない場合、イベントは破棄されます。 |
| `addPurpose(purposeId, dispatcherIds)` | 必要とするディスパッチャーに目的をマッピングします。ディスパッチャーは、その必要な目的が承認された場合にのみ発火します。 |
| `setRefireDispatcherIds(ids)` | 明示的な同意が得られたときに以前にキューに入れられたイベントを再発火するディスパッチャー。 |



```kotlin
TealiumConfig.Builder(...)
    .enableConsentIntegration(cmpAdapter) { settings ->
        settings
            .setTealiumPurposeId("tealium")
            .addPurpose("tracking", setOf(Modules.Types.COLLECT))
            .addPurpose("functional", setOf("logger"))
            .setRefireDispatcherIds(setOf(Modules.Types.COLLECT))
    }
```


```swift
config.enableConsentIntegration(with: cmpAdapter) { enforcedConfiguration in
    enforcedConfiguration
        .setTealiumPurposeId("tealium")
        .addPurpose("tracking", dispatcherIds: [Modules.Types.collect])
        .addPurpose("functional", dispatcherIds: ["logger"])
        .setRefireDispatcherIds([Modules.Types.collect])
}
```



詳細については、APIリファレンスを参照してください：

* [Kotlin 同意 API リファレンス](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.consent/)
* [Swift 同意 API リファレンス](https://docs.tealium.com/tealium-prism-swift/Consent.html)