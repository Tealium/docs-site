---
title: 訪問サービス
description: 訪問サービスモジュールを使用して、モバイルアプリでAudienceStream訪問プロファイルデータを取得します。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/tealium-visitor-service/
---
## 対応プラットフォーム

* [Tealium for Android: 訪問サービスモジュール](/ja/platforms/android-kotlin/module-list/visitor-service/)
* [Tealium for iOS: 訪問サービスモジュール](/ja/platforms/ios-swift/module-list/visitor-service/)

## 動作原理

訪問サービスモジュールは、訪問プロファイルデータにアクセスするための2つの方法を提供します：

* **イベントリスナー**  
訪問プロファイル更新イベントを購読します。新しいイベントが追跡されると、モジュールはTealiumから更新された訪問プロファイルを要求します。プロファイルが前回のリクエスト以降に変更されている場合、更新はすべての登録されたリスナー（Androidの`VisitorUpdatedListener`、iOSの`VisitorServiceDelegate`）に配信されます。
* **直接リクエスト**  
いつでも`requestVisitorProfile()`を呼び出して、オンデマンドで最新の訪問プロファイルを取得します。

デバイスのリソースを節約するために、モジュールは各イベント後に最大5回更新をポーリングし、次のイベントが追跡されるまで一時停止します。プロファイルは、組み込みのLifetime Event Countメトリックが増加したときに更新されたと見なされます。

## 訪問プロファイルの構造

訪問プロファイルは、AudienceStreamの**属性ID**によってキーされた属性を含むオブジェクトです。属性IDは数値の文字列です（例えば、Lifetime Event Countのための`&#34;22&#34;`）。オーディエンスはオーディエンスIDによってキーされ、値としてオーディエンス名が使用されます。

属性タイプと使用例の完全なリストについては、プラットフォーム固有のリファレンスを参照してください：

* [Tealium for Android: VisitorProfile](/ja/platforms/android-kotlin/api/visitor-profile/)
* [Tealium for iOS: Visitor Data Object](/ja/platforms/ios-swift/module-list/visitor-service/#visitor-data-object)

## 例

**例：ユーザーがオーディエンスのメンバーかどうかを確認します。**




```kotlin
Tealium.create(BuildConfig.TEALIUM_INSTANCE, tealiumConfig) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            visitorProfile.audiences?.let { audiences -&gt;
                if (audiences.containsValue(&#34;Premium User&#34;)) {
                    // プレミアム機能を有効にする
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
        if audiences.contains(where: { $0.value == &#34;Premium User&#34; }) {
            // プレミアム機能を有効にする
        }
    }
}
```




**例：訪問プロファイルから属性IDを使用して数値属性にアクセスします。**




```kotlin
Tealium.create(BuildConfig.TEALIUM_INSTANCE, tealiumConfig) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            visitorProfile.numbers?.let { numbers -&gt;
                numbers[&#34;5057&#34;]?.let { sessionCount -&gt;
                    if (sessionCount &gt; 5) {
                        // リピーター向けのアクションを取る
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
        guard let numbers are visitorProfile.numbers else {
            return
        }
        if let sessionCount = numbers[&#34;5057&#34;] {
            if sessionCount &gt; 5 {
                // リピーター向けのアクションを取る
            }
        }
    }
}
```




## 使用例

訪問サービスモジュールを使用して、リアルタイムでアプリをパーソナライズします。例えば：

* ユーザーの好みの製品カテゴリに基づいてコンテンツを表示する
* 以前の閲覧や検索行動に基づいておすすめを提示する
* 高価値またはロイヤルティプログラムのメンバーに異なるUIを表示する
* 特定のオーディエンスセグメントに対して機能を有効または無効にする

## プロファイル更新のタイミング

訪問プロファイルの更新はほとんどの場合ほぼリアルタイムですが、即時性が保証されるわけではありません。タイミングに影響を与える2つのシナリオがあります：

* **ポーリング制限**  
各イベント後、モジュールはプロファイル更新を最大5回ポーリングし、次のイベントまで待機します。5回の試み内に更新が検出されない場合、プロファイルのリフレッシュは次のイベントまで延期されます。
* **非同期プロファイル変更**  
モバイルデバイスの外部（ファイルのインポートや訪問のスティッチングなど）でトリガーされたプロファイル更新は、モジュールが既にポーリングサイクルを完了した後に到着する場合があります。これらの場合、プロファイル更新は次のイベントが追跡された後に配信されます。