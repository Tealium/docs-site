---
title: ビジターサービス
description: ビジターサービスモジュールを使用して、モバイルアプリで顧客データプラットフォーム（CDP）のビジタープロファイルデータを取得します。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/tealium-visitor-service/
---
## サポート対象プラットフォーム

* [Tealium for Android：ビジターサービスモジュール](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/visitor-service/)
* [Tealium for iOS：ビジターサービスモジュール](https://docs.tealium.com/ja/platforms/ios-swift/module-list/visitor-service/)

## 仕組み

ビジターサービスモジュールでは、次の2つの方法でビジタープロファイルデータにアクセスできます。

* **イベントリスナー**  
ビジタープロファイルの更新イベントをサブスクライブします。新しいイベントがトラッキングされると、モジュールは更新されたビジタープロファイルをTealiumにリクエストします。前回のリクエスト以降にプロファイルが変更されている場合、登録されているすべてのリスナー（Androidでは`VisitorUpdatedListener`、iOSでは`VisitorServiceDelegate`）に更新が配信されます。
* **直接リクエスト**  
任意のタイミングで`requestVisitorProfile()`を呼び出し、最新のビジタープロファイルをオンデマンドで取得します。

デバイスのリソースを節約するため、モジュールは各イベントの発生後に最大5回更新をポーリングし、その後、次のイベントがトラッキングされるまで一時停止します。組み込みのLifetime Event Count指標が増加すると、プロファイルが更新されたとみなされます。

## ビジタープロファイルの構造

ビジタープロファイルは、CDPの**属性ID**をキーとする属性を含むオブジェクトです。属性IDは数値文字列です（たとえば、Lifetime Event Countの場合は`"22"`）。オーディエンスはオーディエンスIDをキーとし、オーディエンス名を値とします。

属性タイプと使用例の完全な一覧については、各プラットフォーム固有のリファレンスを参照してください。

* [Tealium for Android：VisitorProfile](https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-profile/)
* [Tealium for iOS：ビジターデータオブジェクト](https://docs.tealium.com/ja/platforms/ios-swift/module-list/visitor-service/#visitor-data-object)

## 例

**例：ユーザーがオーディエンスのメンバーであるかどうかを確認する。**




```kotlin
Tealium.create(BuildConfig.TEALIUM_INSTANCE, tealiumConfig) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            visitorProfile.audiences?.let { audiences ->
                if (audiences.containsValue("Premium User")) {
                    // enable premium features
                }
            }
        }
    })
}
```




```swift
extension TealiumHelper: VisitorServiceDelegate {
    func didUpdate(visitorProfile: TealiumVisitorProfile) {
        guard let audiences = visitorProfile.audiences else {
            return
        }
        if audiences.contains(where: { $0.value == "Premium User" }) {
            // enable premium features
        }
    }
}
```




**例：属性IDを使用して、ビジタープロファイルから数値属性にアクセスする。**




```kotlin
Tealium.create(BuildConfig.TEALIUM_INSTANCE, tealiumConfig) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            visitorProfile.numbers?.let { numbers ->
                numbers["5057"]?.let { sessionCount ->
                    if (sessionCount > 5) {
                        // take action for returning users
                    }
                }
            }
        }
    })
}
```




```swift
extension TealiumHelper: VisitorServiceDelegate {
    func didUpdate(visitorProfile: TealiumVisitorProfile) {
        guard let numbers = visitorProfile.numbers else {
            return
        }
        if let sessionCount = numbers["5057"] {
            if sessionCount > 5 {
                // take action for returning users
            }
        }
    }
}
```




## ユースケース

ビジターサービスモジュールを使用すると、アプリをリアルタイムでパーソナライズできます。たとえば、次のことが可能です。

* ユーザーが希望する製品カテゴリーに基づいてコンテンツを表示する
* 過去の閲覧または検索行動に基づいておすすめを提示する
* 価値の高い顧客やロイヤルティプログラムのメンバーに異なるUIを表示する
* 特定のオーディエンスセグメントに対して機能を有効または無効にする

## プロファイルの更新タイミング

ほとんどの場合、ビジタープロファイルはほぼリアルタイムで更新されますが、即時に更新されるとは限りません。次の2つのシナリオが更新タイミングに影響する可能性があります。

* **ポーリング上限**  
各イベントの発生後、モジュールはプロファイルの更新を最大5回ポーリングし、その後は次のイベントまで待機します。5回以内に更新が検出されなかった場合、プロファイルの更新は次のイベントまで延期されます。
* **非同期のプロファイル変更**  
モバイルデバイス外でトリガーされたプロファイル更新（ファイルのインポートやビジタースティッチングなど）は、モジュールがポーリングサイクルを完了した後に到着することがあります。この場合、プロファイルの更新は次のイベントがトラッキングされた後に配信されます。