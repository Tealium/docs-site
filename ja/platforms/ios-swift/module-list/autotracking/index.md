---
title: 自動追跡モジュール
description: 画面のビューを自動的に追跡します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/autotracking/
---
自動追跡モジュールは、追加コードを最小限に抑えつつ、アプリの画面ビューの自動追跡を追加します。

以下のプラットフォームがサポートされています：
* iOS
* tvOS
* watchOS
* macOS

## 仕組み

ビルドと初期化に自動追跡モジュールを追加することで、自動的な画面ビューの追跡を利用できます。モジュールには、追跡する画面とその命名方法を制御するためのいくつかのオプションがあります。

自動追跡モジュールは、以下の2つの追跡モードをサポートしています：

* **フルトラッキング**
  * UIKit - すべての画面ビューを自動的に追跡し、ブロックリストを使用して画面を省略するオプションがあります。
  * SwiftUI - サポートされていません。
* **部分的な追跡**
  * UIKit - 追跡する各ビューに対して、ビューコントローラのサブクラスを作成します。
  * SwiftUI - 追跡する各ビューに対して、ビューモディファイアを作成するか、Tealiumの追跡コンテナにビューを埋め込みます。
  
### フルトラッキング

フルトラッキングは、UIKitアプリでのみ利用可能です。

UIKitでは、自動追跡モジュールは`ViewController`の`viewDidAppear`インスタンスメソッドにメソッドスワッピングを使用します。追跡されるイベントの名前は、`UIViewController.title`プロパティに構成されます。それが利用できない場合は、&#34;ViewController&#34;接尾辞を削除した後の`UIViewController`クラス名に構成されます。

### 部分的な追跡

自動追跡とパフォーマンスの最適化をより制御するために、部分的な追跡を使用します。このアプローチは、`ViewController`コード内の注釈を使用して、必要なビューのみを追跡します。このアプローチは、特定のアプリデザインパラダイムに依存せず、UIKitアプリまたはSwiftUIアプリで動作します。

### ブロックリスト

フルトラッキングモードでブロックリスト機能を使用して、特定の追跡呼び出しを抑制します。
ブロックリストは、文字列の単一配列を含むJSONファイルです。文字列は、自動追跡から省略するビューを表します。ブロックリストにある文字列がビューコントローラ名のどこかに現れると、それは追跡されません。文字列の比較は大文字と小文字を区別しません。

例えば、&#34;Settings&#34;や&#34;Profile&#34;という文字列を含むビューコントローラ名を追跡したくない場合、ブロックリストには以下のように含めることができます：

```json
[
  &#34;settings&#34;, &#34;profile&#34;
]
```

ブロックリストファイルは、アプリ内にローカルに保存するか、URLとしてリモートにホストすることができます。

ブロックリストを使用するには、以下の`TealiumConfig`プロパティのいずれかを使用します：

* [`autoTrackingBlocklistFilename`](/ja/platforms/ios-swift/api/tealium-config/#autotrackingblocklistfilename)
* [`autoTrackingBlocklistUrl`](/ja/platforms/ios-swift/api/tealium-config/#autotrackingblocklisturl)


## 必要条件

* `UIKit`または`SwiftUI`
* `UIApplication`

## インストール

CocoaPodsまたはCarthageを使用して自動追跡モジュールをインストールします。

### CocoaPods

CocoaPodsで自動追跡モジュールをインストールするには、以下のpodをPodfileに追加します：  
```perl
pod &#39;tealium-swift/Autotracking&#39;
```

[iOS向けのCocoaPodsインストール](/ja/platforms/ios-swift/install/#cocoapods)について詳しくはこちらをご覧ください。

### Carthage

Carthageで自動追跡モジュールをインストールするには、以下の手順に従います：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 以下のフレームワークを**Embedded Binaries**セクションに追加します：  
      ```perl
      TealiumAutotracking.framework
      ```

[iOS向けのCarthageインストール](/ja/platforms/ios-swift/install/#carthage)について詳しくはこちらをご覧ください。

## 初期化

自動追跡モジュールを初期化するには、[`TealiumConfig.collectors`](/ja/platforms/ios-swift/api/tealium-config/#collectors)プロパティに追加します。

```swift
config.collectors = [Collectors.Autotracking]
```

必要なコレクタを正しく指定する方法については、[Collectors](/ja/platforms/ios-swift/modules/#collectors)のドキュメンテーションを参照してください。

## 部分的な追跡の構成

### UIKit

UIKitアプリでは、追跡したいビューコントローラのみを変更して部分的な追跡を実装します。

フルトラッキングをオフにして部分的な追跡を追加するには、まずアプリケーションの`info.plist`に`TealiumAutotrackingViewControllersEnabled`エントリを追加し、値を`false`に構成します：

```xml
&lt;key&gt;TealiumAutotrackingViewControllersEnabled&lt;/key&gt;
&lt;false/&gt;
```

特定のビューコントローラを自動的に追跡するには、`TealiumViewController`のサブクラスを作成します：

```swift
class MyAutomaticallyTrackedViewController: TealiumViewController { 
    // ...
}
```

あるいは、`TealiumViewControllerTrackable`に準拠し、ビューコントローラの`viewDidAppear`メソッドで`trackViewControllerAppearence`を呼び出すこともできます。

```swift
class MyViewController: UITableViewController, TealiumViewControllerTrackable {
     @objc
     open override func viewDidAppear(_ animated: Bool) {
         super.viewDidAppear(animated)
         trackViewControllerAppearence()
     }
 }
```

### SwiftUI

SwiftUIで特定のビューを自動的に追跡するには、以下のアプローチのいずれかまたは両方を実装します： 

* 追跡したい各ビューにカスタム修飾子を追加します。
* 追跡したい各ビューをTealiumの自動追跡コンテナに埋め込みます。

以下のビューモディファイアのいずれかを使用します：

#### `autoTracking(viewSelf:) -&gt; some View`

この修飾子を使用して、クラス名を使用してビューを自動的に追跡します。

追跡したいビューの本体にこの修飾子を適用し、パラメータとして`self`を渡します：

```swift
struct SomeView: View {
    var body: some View {
        Group {
            Spacer()
            Text(&#34;Some Text&#34;)
            Spacer()
        }.autoTracking(viewSelf: self) 
    }
}
```

#### `autoTracking(viewClass:) -&gt; some View`

この修飾子を使用して、ビュークラスのクラス名を使用してビューを自動的に追跡します。

追跡したいビューの本体にこの修飾子を適用し、追跡したいクラスの名前を渡します（オブジェクトインスタンスにアクセスできない場合）：

```swift
struct SomeContainerView: View {
    var body: some View {
        SomeOtherView {
            Spacer()
            Text(&#34;Some Text&#34;)
            Spacer()
        }.autoTracking(viewClass: SomeOtherView.self) 
    }
}
```

#### `autoTracked(constantName:) -&gt; some View`

この修飾子を使用して、カスタム定数名でビューを自動的に追跡します。

定数を取る変数を変更しても、追跡される名前は変わりません。

ここに状態変数を渡さないでください。`onDisappear`呼び出しと競合する可能性があります。 

状態変数を渡したい場合は、代わりにバインディング値を渡し、オーバーロードされたメソッドを使用します。

```swift
struct SomeView: View {
    var body: some View {
        Group {
            Spacer()
            Text(&#34;Some Text&#34;)
            Spacer()
        }.autoTracked(constantName: &#34;Some Constant Name&#34;) 
    }
}
```

#### `autoTracked(name: Binding&lt;String&gt;) -&gt; some View`
  
この修飾子を使用して、カスタム状態変数名でビューを自動的に追跡します。

この場合、変数を変更すると、次回の自動追跡呼び出しで異なるイベント名が結果として得られます。

このメソッドは、状態変更に対して`onAppear`が`onDisappear`の後に呼び出される問題を解決し、次回の自動追跡名に対して変数名を変更することを可能にします。

```swift
struct SomeView: View {
    @State var name = &#34;Some Variable Name&#34;
    var body: some View {
        Group {
            Spacer()
            Text(&#34;Some Text&#34;)
            Spacer()
        }.autoTracked(name: $name) 
    }
}
```

#### 自動追跡コンテナの埋め込み

ビューモディファイアの代わりに、追跡したい各ビューに自動追跡コンテナ`TealiumViewTrackable`を埋め込みます。

このアプローチには3つのオプションがあります：

* **コンテンツビューで初期化**  
初期化子にコンテンツビューを渡して、コンテンツクラス名を自動的に追跡します。  
    ```swift
    TealiumViewTrackable {
      SomeView()
    }
    ```
* **定数名とコンテンツビューで初期化**  
コンテンツクラス名の代わりに追跡する状態変数を指定して定数名を指定します。  
    ```swift
    TealiumViewTrackable(constantName: &#34;Some Constant Name&#34;) {
      SomeView()
    }
    ```
* **状態変数のバインディング名とコンテンツビューで初期化**  
ビューの状態変数からバインディングを渡します。これは`onAppear`がトリガーされたときの状態変数の現在の値を使用します。  
    ```swift
    @State var name: String = &#34;Some Variable Name&#34;
    var body: some View {
      TealiumViewTrackable(viewName: $name) {
        SomeView()
      }
    }
    ```

## データレイヤー

このモジュールによってトリガーされる各追跡呼び出しには、以下の変数が含まれます：

| 変数      | 説明                                            | 例 |
|:--------------|:-------------------------------------------------------|:--------|
| `autotracked` | 自動追跡モジュールによって追跡されたすべてのイベントに構成されます。 | `true`  |

## APIリファレンス

* [`TealiumConfig`](/ja/platforms/ios-swift/api/tealium-config/)
