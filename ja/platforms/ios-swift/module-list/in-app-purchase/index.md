---
title: アプリ内購入モジュール
description: アプリ内購入モジュールは、アプリにアプリ内購入の自動追跡を追加します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/in-app-purchase/
---
## アプリ内購入とは何ですか？

アプリ内購入とは、アプリ内で購入する追加のコンテンツ、サービス、またはサブスクリプションのことを指します。アプリ内購入の例としては以下のようなものがあります：

* 広告の削除のためのアップグレード
* ゲームクレジット
* バーチャル通貨
* 追加のゲームレベル
* さらなる機能の解放

アプリ内購入とはみなされない購入の例としては以下のようなものがあります：

* 電子商取引アプリでの衣服やその他のアイテムの購入。
* Apple Payを使用して購入を完了する。

[Apple開発者ポータルのアプリ内購入](https://developer.apple.com/in-app-purchase/)について詳しく学びましょう。

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してアプリ内購入モジュールをインストールします。

### Swift Package Manager (推奨)

Tealium Swiftライブラリをインストールする推奨方法はSwift Package Managerです：

1. Xcodeプロジェクトで、**File &gt; Add Package Dependencies**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`。
1. バージョンルールを構成します。デフォルトの`&#34;Up to next major&#34;`が推奨されます。現在のTealium Swiftライブラリのバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットします。
1. インストールするモジュールのリストから`InAppPurchase`モジュールを選択します。Xcodeプロジェクトの**Frameworks and Libraries**の各アプリターゲットにモジュールを追加します。

iOSの[Swift Package Manager](https://docs.tealium.com/platforms/ios-swift/install/#swift-package-manager-recommended)インストールについて詳しく学びましょう。

### CocoaPods

CocoaPodsを使用してアプリ内購入モジュールをインストールするには、以下のpodをPodfileに追加します：

```perl
pod &#39;tealium-swift/InAppPurchase&#39;
```
iOSの[CocoaPods](https://docs.tealium.com/platforms/ios-swift/install/#cocoapods)インストールについて詳しく学びましょう。

### Carthage

Carthageを使用してアプリ内購入モジュールをインストールするには、以下の手順を実行します：

1. Xcodeでターゲットアプリの**General**構成ペインに移動します。
2. 次のフレームワークを**Embedded Binaries**セクションに追加します：
      ```swift
      TealiumInAppPurchase.xcframework
      ```
3. アプリ内購入ライブラリをインポートするには、プロジェクトに次のインポート文を追加します：
      ```swift
      import TealiumInAppPurchase
      ```

iOSの[Carthage](https://docs.tealium.com/platforms/ios-swift/install/#carthage)インストールについて詳しく学びましょう。

## 構成

アプリ内購入モジュールをインスタンス化するには、SDKを初期化する際に`TealiumConfig`オブジェクトで指定する必要があります：

```swift
import TealiumCore
import TealiumInAppPurchase

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           datasource: &#34;DATASOURCE&#34;)

config.collectors = [Collectors.InAppPurchase]
tealium = Tealium(config: config) { _ in }
```

必要なコレクターを正しく指定する方法については、[Collectors](/ja/platforms/ios-swift/modules/#collectors)のドキュメンテーションを参照してください。

## データレイヤー

アプリ内購入モジュールは、イベントで以下の属性を送信します：

| 変数                  | 説明                                                         | 例 |
|:---------------------|:--------------------------------------------------------------------|:--|
| `purchase_order_id`  | 購入の注文ID。                                       | &#34;1234567890&#34; |
| `purchase_timestamp` | ISO 8601形式の購入のタイムスタンプ。                   | &#34;2022-01-17T14:42:28Z&#34; |
| `purchase_quantity`  | 購入したアイテムの総数。                                | &#34;1&#34; |
| `purchase_skus`      | 購入した製品IDの配列。                              | [&#34;com.example.level1&#34;] |
| `autotracked`        | イベントが自動的に追跡されたことを示すために`true`に構成します。 | true |
| `tealium_event`      | イベントの名前。                                              | &#34;in_app_purchase&#34; |