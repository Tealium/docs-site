---
title: DefaultStorage モジュール
description: UserDefaultsをバックエンドに持つ永続的なデータストレージを提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/defaults-storage/
---
## 使用法


<blockquote>
Swift 1.8.0+を使用している場合、このモジュールはすでにCoreに含まれており、インストールする必要はありません。それ以前のバージョンでは、このガイドに従ってモジュールをインストールしてください。
</blockquote>


DefaultStorage モジュールは、UserDefaultsをバックエンドに持つ永続的なデータストレージを提供します。このモジュールは、Swift モジュール：[PersistentData](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/persistent-data/)と一緒に使用する必要があります。

Persistent Data モジュールを使用している場合（推奨）、データをアプリの起動間で永続化するために、Defaults Storage モジュールまたは File Storage モジュールのいずれかを使用する必要があります。Defaults Storage を File Storage に選ぶかどうかは個人の選択です。FileStorage と DefaultsStorage の両方が含まれており、有効になっている場合、FileStorage が優先され、DefaultsStorage は実質的に非アクティブになります。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* watchOS
* macOS

## インストール

CocoaPods または Carthage を使用して DefaultStorage モジュールをインストールします。

### CocoaPods

CocoaPods を使用して DefaultStorage モジュールをインストールするには、以下の pod を Podfile に追加します：  
```ruby
pod 'tealium-swift/TealiumDefaultsStorage'
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` pod に依存しています。また、PersistentData モジュールもバンドルしています。iOSのCocoaPodsインストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)をご覧ください。


### Carthage

Carthage を使用して DefaultStorage モジュールをインストールするには、以下の手順を実行します：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 以下のフレームワークを **Embedded Binaries** セクションに追加します：  
      ```ruby
      TealiumDefaultsStorage.framework
      ```
3. `Tealium` インスタンス上の persistentData API にアクセスするために、プロジェクトに以下の必要なインポート文を追加します：   
      ```swift
      import TealiumDefaultsStorage
      ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存しています。また、PersistentData モジュールもバンドルしています。追加のインポート文は必要ありません。iOSのCarthageインストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)をご覧ください。



## データレイヤー

このモジュールによって追加の変数は導入されません。

## API リファレンス

このモジュールには公開APIメソッドはありません。成功と失敗はDelegateモジュールを通じて監視することができます。

## リリースノート

ビルド 1

* 初回リリース

