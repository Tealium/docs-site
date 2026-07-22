---
title: AdobeVisitorServiceモジュール
description: 各ユーザーに対してクロスデバイスの訪問IDを提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/adobe-visitor-service/
---
Adobe Visitor Serviceモジュールは、訪問のExperience Cloud ID（ECID）を取得および維持するためにAdobeのREST APIと直接連携します。

[AdobeVisitorService](https://docs.tealium.com/ja/platforms/getting-started-mobile/adobe-visitor-service/)モジュールについてもっと学びましょう。

## 要件

* [Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/) (2.0.0以上)
* 有効なAdobeアカウントとAdobe組織ID
* [TealiumAdobeVisitorAPI GitHubリポジトリ](https://github.com/Tealium/tealium-swift-adobe-visitor-api)

## サンプルアプリ

Tealiumライブラリとベストプラクティスの実装に慣れるために、iOS用の[AdobeVisitorServiceモジュールサンプルアプリ](https://github.com/Tealium/tealium-swift-adobe-visitor-api/tree/main/VisitorAPIExample)を探索してください。

## インストール

AdobeVisitorServiceモジュールはTealium SDKの初期化時に構成され、リモート構成機能はありません。

このモジュールは`DispatchValidator`として機能し、Adobe組織IDなしでは送信が阻止されます。Adobe APIからECIDを取得しようと試みますが、5回の失敗後は、データ損失を避けるためにECIDなしでの続行が許可されます。有効なECIDを持つことよりもデータ送信が優先されます。

ECIDが取得できなかった可能性のある原因は以下の通りです：

* 無効な応答、例えば応答は受け取ったが有効なECIDを含んでいなかった。
* 応答がなかった。
* Adobe組織IDが無効だった。

### Carthage

CarthageでAdobeServiceモジュールをインストールするには、次の内容をcartfileに追加してください：

```bash
github "tealium/tealium-swift-adobe-visitor-api"
```

[iOSのCarthageインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)についてもっと学びましょう。

### CocoaPods

CocoaPodsでAdobeVisitorモジュールをインストールするには、次のpodをpodfileに追加してください：  
```perl
pod 'TealiumAdobeVisitorAPI'
```

[iOSのCocoaPodsインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)についてもっと学びましょう。

### Swift Package Manager（推奨）

Swift Package ManagerはTealium Swiftライブラリをインストールする推奨方法です：

1. Xcodeプロジェクトで**File > Add Package Dependencies**を選択します。
1. リポジトリURLを入力します：`https://github.com/Tealium/tealium-swift-adobe-visitor-api`。
1. バージョンルールを構成します。デフォルトの「Up to next major」が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールするモジュールのリストから`TealiumAdobeVisitorAPI`モジュールを選択します。Xcodeプロジェクトの**Frameworks and Libraries**の下にあるアプリターゲットごとにモジュールを追加します。

[iOSのSwift Package Managerインストール](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended)についてもっと学びましょう。

```swift
import TealiumAdobeVisitorAPI

let config = TealiumConfig(account: "ACCOUNT",
    profile: "PROFILE",
    environment: "ENVIRONMENT")
config.collectors = [Collectors.AppData,
    Collectors.Connectivity,
    Collectors.Device,
    Collectors.Lifecycle,
    Collectors.AdobeVisitor]
config.dispatchers = [Dispatchers.Collect]
self.tealium = Tealium(config: config)
```


<blockquote>
[Collectors](https://docs.tealium.com/ja/platforms/ios-swift/modules/#collectors)のドキュメントを確認して、必要なコレクターを正しく指定する方法を理解してください。
</blockquote>


[iOSのSwift Package Managerインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)についてもっと学びましょう。


<blockquote>
既知の訪問IDをリンクするか認証状態を構成するには、[既知の訪問IDと認証状態を構成する](https://docs.tealium.com/ja/platforms/getting-started-mobile/adobe-visitor-service/#set-a-known-visitor-id-and-authentication-state)を参照してください。
</blockquote>
