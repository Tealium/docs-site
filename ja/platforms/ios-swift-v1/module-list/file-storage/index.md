---
title: FileStorageモジュール
description: FileManager/NSKeyedArchiver APIによって支えられた永続的なデータストレージを提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/file-storage/
---
## 使用法


<blockquote>
Swift 1.8.0+を使用している場合、このモジュールはすでにCoreに含まれており、インストールする必要はありません。それ以前のバージョンでは、このガイドに従ってモジュールをインストールしてください。
</blockquote>


FileStorageモジュールは、`FileManager`/`NSKeyedArchiver` APIによって支えられた永続的なデータストレージを提供します。このモジュールは、Swiftモジュール：[PersistentData](https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/persistent-data/)と一緒に使用する必要があります。

Persistent Dataモジュールを使用している場合（推奨）、データをアプリの起動間で永続化するために、File StorageモジュールまたはDefaults Storageモジュールのいずれかを使用する必要があります。Defaults StorageをFile Storageより選ぶかどうかは個人の選択です。FileStorageとDefaultsStorageの両方が含まれており、有効になっている場合、FileStorageが優先され、DefaultsStorageは実質的に非アクティブになります。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* watchOS
* macOS

## インストール

CocoaPodsまたはCarthageでFileStorageモジュールをインストールします。

### CocoaPods

CocoaPodsでFileStorageモジュールをインストールするには、以下のpodをPodfileに追加します：  
```ruby
pod 'tealium-swift/TealiumFileStorage'
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podに依存しています。また、PersistentDataモジュールもバンドルしています。iOSのCocoaPodsインストールについて[詳しくはこちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)をご覧ください。


### Carthage

CarthageでFileStorageモジュールをインストールするには、以下の手順を実行します：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 以下のフレームワークを**Embedded Binaries**セクションに追加します：  
      ```ruby
      TealiumFileStorage.framework
      ```
3. `Tealium`インスタンス上のPersistentData APIにアクセスするために、プロジェクトに以下の必要なインポート文を追加します：   
      ```swift
      import TealiumFileStorage
      ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存しています。また、PersistentDataモジュールもバンドルしています。追加のインポート文は必要ありません。iOSのCarthageインストールについて[詳しくはこちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)をご覧ください。


## データレイヤー
このモジュールによって追加の変数は導入されません。

## APIリファレンス
このモジュールには公開APIメソッドはありません。成功と失敗はDelegateモジュールを通じて監視することができます。

## リリースノート

ビルド1.4.0

* パーミッションエラーによりデータがディスクに永続化されないバグを修正

