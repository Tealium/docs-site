---
title: ディープリンク
description: モバイル向けのディープリンクについて学びます。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/deep-linking/
---
ディープリンクは、モバイルアプリを起動し、オプションでアプリ内の特定のコンテンツを提供するハイパーリンクです。ディープリンクは、ユーザーをあなたのアプリにリンクする広告キャンペーンやプロモーションメールのパフォーマンスを測定するためによく使用されます。

## サポートされているプラットフォーム

以下のプラットフォームではディープリンクのトラッキングがサポートされています：

- [Android (Kotlin)](/ja/platforms/android-kotlin/)
- [iOS (Swift v2.x)](/ja/platforms/ios-swift/)

## 仕組み

アプリがディープリンクから起動されると、TealiumライブラリはURLをデータレイヤーに`deep_link_url`という属性として追加します。

ディープリンクのクエリパラメータは、`deep_link_param_&lt;param name&gt;`という形式の属性名でデータレイヤーに追加されます。

例えば、`https://example.com/?campaign_code=SUMMER`は次のようになります：  
```javascript
deep_link_url = &#34;https://example.com/?campaign_code=SUMMER&#34;
deep_link_param_campaign_code = &#34;SUMMER&#34;
```

ディープリンクのデータレイヤー属性はセッション中のみ保存されます。

## 構成

### Android Kotlin

Tealium for Android (Kotlin)では、ディープリンクのトラッキングが自動的に有効化されています。

ディープリンクの自動トラッキングを無効にするには、[`deepLinkTrackingEnabled`](/ja/platforms/android-kotlin/api/tealium-config/#deeplinktrackingenabled)プロパティを`false`に構成します。

### Swift v2.x

Tealium for iOS (Swift v2.x)では、メソッドスワッピング技術を通じてディープリンクの自動トラッキングがデフォルトで有効化されています。メソッドスワッピングとは、プログラムの実行時に一つのメソッドの実装を別のものと動的に交換することです。

メソッドスワッピングを使用したくない場合やディープリンクを自動的にトラッキングしたくない場合は、`info.plist`のキー`TealiumAutotrackingDeepLinkEnabled`を`false`に構成して自動ディープリンクトラッキングを無効にできます。

メソッドスワッピングなしでディープリンクをトラッキングしたい場合、または`SwiftUI`を使用している場合は、`info.plist`で自動トラッキングを無効にした後、アプリケーションコンテンツの`View`に`TealiumAppTrackable`ラッパーを使用します：

```swift
var body: some Scene {
    WindowGroup {
        TealiumAppTrackable {
            ContentView()
        }
    }
}
```

`UIKit`を使用している場合は、代わりに`tealium`インスタンス上の`handleDeeplink`メソッドを手動で呼び出すことができます。

### Swift v1.x

Tealium for iOS (Swift v1.x)では、ディープリンクを有効にするためにアプリの`AppDelegate`クラスに一行のコードを追加する必要があります。  

```swift
func application(_ app: UIApplication,
                 open url: URL,
                 options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -&gt; Bool {
  tealium?.handleDeepLink(url)
  return true
}
```

## データレイヤー

アプリがディープリンクから起動されると、以下のプロパティがデータレイヤーに追加されます：

| イベント属性 | タイプ | 説明 | 例 |
| :-- | :-- | :-- | :-- |
| `deep_link_url` | `String` | アプリを開いたディープリンクの完全なURL、クエリパラメータを含む。 | `https://example.com/?campaign_code=SUMMER` |
| `deep_link_param_X` | `String` | ディープリンクURLの各クエリパラメータ、ここで`X`はパラメータの名前、例えば`deep_link_param_campaign_code`。| `SUMMER` |
| `deep_link_referrer_url` (iOS) | `String` | ディープリンクがクリックされたブラウザページの完全なURL。 | `https://www.example.com/referring/page` |
| `deep_link_referrer_app` (iOS) | `String` | ディープリンクが同じチームによって署名された別のアプリのカスタムスキーマから来た場合のリファラーアプリの識別子。 | `com.example.appId` |