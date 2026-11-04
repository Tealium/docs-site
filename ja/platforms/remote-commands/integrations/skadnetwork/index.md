---
title: リモートコマンド：SKAdNetwork
description: AppleのSwift向けSKAdNetwork用Tealiumリモートコマンド連携。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/skadnetwork/
---
[SKAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork)は、ユーザーのプライバシーを保護しながら、広告主が広告キャンペーンの成果を測定できるようにするAppleのSDKです。

## 要件

* [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/)（2.9.0以降）
* [SKAdNetworkリモートコマンドJSONファイル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/skadnetwork/#json-template)

## 仕組み

SKAdNetwork連携では、次の2つの項目を使用します。

1. SKAdNetworkのコンバージョン値を送信するリモートコマンドモジュール
2. イベントトラッキングをコンバージョン値に変換するJSON構成ファイルまたはリモートコマンドタグ

この連携では、アプリ内にローカルで配置するか、リモートでホストしたJSON構成ファイルを使用することを推奨します。タグ管理を使用している場合は、ベンダー連携用のリモートコマンドタグを追加します。[ベンダー連携](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)の詳細をご覧ください。

## インストール

### 依存関係マネージャー




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリURLとして`https://github.com/tealium/tealium-ios-skadnetwork-remote-command`を入力します。
3. バージョンルールを構成します。通常は`Up to next major`を推奨します。現在の`TealiumSKAdNetwork`バージョンが一覧に表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
4. インストールする`TealiumSKAdNetwork`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。
5. Tealium Swiftライブラリの追加モジュールを使用する場合は、[Swift Package Managerの手順](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)に従って追加します。

プロジェクトに複数のアプリターゲットがあり、複数のターゲットで`TealiumSKAdNetwork`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumSKAdNetwork`をインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトの**TARGETS**セクションでアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumSKAdNetwork`モジュールを選択してアプリターゲットに追加します。




1. Podfileに`pod "tealium-swift"`および`pod "SKAdNetwork"`が存在する場合は削除します。`tealium-swift`の依存関係は、すでに`TealiumSKAdNetwork`フレームワークに含まれています。

2. 次の依存関係をPodfileに追加します。  
      ```ruby
      pod "TealiumSKAdNetwork"
      ```  
      `TealiumSKAdNetwork` Podには、次の`TealiumSwift`依存関係が含まれています。  
      ```bash
      "tealium-swift/Core"
      "tealium-swift/RemoteCommands"
      ```

3. `tealium-swift/Collect`または`tealium-swift/TagManagement`のいずれかのディスパッチャーPodをインストールに含め、その他の個別のサブモジュールもPodfileに追加します。例：  
      ```ruby
      pod "TealiumSKAdNetwork"
      pod "tealium-swift/Collect"
      pod "tealium-swift/Lifecycle"
      pod "tealium-swift/Attribution"
      ```

4. `TealiumHelper`ファイル、および`Tealium`クラスまたはAdjustリモートコマンドにアクセスするその他のファイルで、`TealiumSwift`モジュールと`TealiumSKAdNetwork`モジュールをインポートします。




1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係は、すでに`TealiumSKAdNetwork`フレームワークに含まれています。

2. Cartfileに次の行が存在する場合は削除します。  
      ```bash
      github "skadnetwork/ios_sdk"
      ```

3. 次の依存関係をCartfileに追加します。  
      ```bash
      github "tealium/tealium-ios-skadnetwork-remote-command"
      ```




### 手動インストール

SKAdNetworkリモートコマンドを手動でインストールするには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトにSKAdNetworkリモートコマンドをインストールするには、次の手順を実行します。

1. まだインストールしていない場合は、[SKAdNetwork SDK](https://github.com/skadnetwork/ios_sdk)をインストールします。

2. [Tealium iOS SKAdNetworkリモートコマンド](https://github.com/tealium/tealium-ios-skadnetwork-remote-command)リポジトリをクローンし、`Sources`フォルダー内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。

## 初期化

JSON構成ファイルまたはTealiumのiOS（Swift）ライブラリ用リモートコマンドタグを使用して、リモートコマンドを初期化します。

次のコードは、ローカルファイルオプションを使用するJSONリモートコマンド機能向けに設計されています。  
```swift
var tealium : Tealium?
let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "ENVIRONMENT",
                           dataSource: "DATASOURCE",
                           optionalData: nil)

config.remoteAPIEnabled = true // Required to use Remote Commands
config.dispatchers = [Dispatchers.RemoteCommands, Dispatchers.Collect]

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

    // Webview Tag
    let skadnetwork = SKAdNetworkRemoteCommand(delegate: self)

    // Local JSON
    //let skadnetwork = SKAdNetworkRemoteCommand(type: .local(file: "skadnetwork"), delegate: self)

    // Remote JSON
    //let skadnetwork = SKAdNetworkRemoteCommand(type: .remote(url: "https://some.domain.com/skadnetwork.json"), delegate: self)

	remoteCommands.add(skadnetwork)
}
```

### デリゲート

デリゲートは省略可能なパラメータです。コンバージョンの更新および完了コールを受信し、デバッグ、エラー処理、必要に応じたトラッキングに使用できます。

```swift
    /// When we detect that a new conversion value needs to be sent
    func onConversionUpdate(conversionData: ConversionData, lockWindow: Bool)
    /// When the new conversion value was sent and completed, optionally with an error
    func onConversionUpdateCompleted(error: Error?)
}
```
### JSONテンプレート

[JSON構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、以下のテンプレートを参照してください。必要に応じてマッピングを編集します。




このテンプレートには、単純値アトリビューション戦略で一般的に使用されるマッピングが含まれています。一部のイベントで送信する詳細値と粗い値をマッピングします。

```json
{
    "config": {
      "send_higher_value": true
    },
    "mappings": {
        "fine_value":"fine_value",
        "coarse_value":"coarse_value"
    },
    "commands": {
        "launch": "initialize,registerappforattribution,setconversionvalue",
        "register": "setconversionvalue",
        "login": "setconversionvalue",
        "tutorial": "setconversionvalue",
        "addtocart": "setconversionvalue",
        "purchase": "setconversionvalue",
        "user_type:premium,subscribe": "setconversionvalue"
    },
    "statics": {
        "launch": {
            "fine_value": 0,
            "coarse_value": "low"
        }
}
```




このテンプレートには、標準的なイベントベースのアトリビューション戦略で一般的に使用されるマッピングが含まれています。各イベントは、コンバージョン値を構成する6ビットのいずれかにマッピングされます。

```json
{
    "config": {
      "send_higher_value": true
    },
    "mappings": {
        "bit_number":"bit_number",
        "fine_value":"fine_value",
        "coarse_value":"coarse_value"
    },
    "commands": {
        "launch": "initialize,registerappforattribution,setconversionvalue",
        "register": "setconversionbit",
        "login": "setconversionbit",
        "tutorial": "setconversionbit",
        "addtocart": "setconversionbit",
        "purchase": "setconversionbit",
        "user_type:premium,subscribe": "setconversionbit"
    },
    "statics": {
        "launch": {
            "fine_value": 0,
            "coarse_value": "low"
        },
        "register": {
            "bit_number": 0,
            "coarse_value": "low"
        },
        "login": {
            "bit_number": 1,
            "coarse_value": "low"
        },
        "tutorial": {
            "bit_number": 2,
            "coarse_value": "low"
        },
        "addtocart": {
            "bit_number": 3,
            "coarse_value": "medium"
        },
        "purchase": {
            "bit_number": 4,
            "coarse_value": "high"
        },
        "user_type:premium,subscribe": {
            "bit_number": 5,
            "coarse_value": "high"
        },
    }
}
```





このテンプレートには、混合アトリビューション戦略で一般的に使用されるマッピングが含まれています。6ビットのうち2ビットは値の保存に使用され、4ビットはイベントのエンコードに使用されます。

```json
{
    "config": {
      "send_higher_value": true
    },
    "mappings": {
        "bit_number":"bit_number",
        "fine_value":"fine_value",
        "coarse_value":"coarse_value",
        "limit_to_highest_n_bits": "limit_to_highest_n_bits",
        "limit_to_lowest_n_bits": "limit_to_lowest_n_bits"
    },
    "commands": {
        "launch": "initialize,registerappforattribution,setconversionvalue",
        "register": "setconversionbit",
        "login": "setconversionbit",
        "tutorial": "setconversionbit",
        "addtocart": "setconversionbit",
        "purchase": "setconversionbit",
        "subscribe": "setconversionvalue"
    },
    "statics": {
        "launch": {
            "fine_value": 0,
            "coarse_value": "low"
        },
        "register": {
            "bit_number": 0,
            "coarse_value": "low"
        },
        "login": {
            "bit_number": 1,
            "coarse_value": "low"
        },
        "tutorial": {
            "bit_number": 2,
            "coarse_value": "low"
        },
        "addtocart": {
            "bit_number": 3,
            "coarse_value": "medium"
        },
        "purchase": {
            "bit_number": 4,
            "coarse_value": "high"
        },
        "user_type:common,subscribe": {
            "limit_to_highest_n_bits": 2,
            "fine_value": 1,
            "coarse_value": "low"
        },
        "user_type:premium,subscribe": {
            "limit_to_highest_n_bits": 2,
            "fine_value": 2,
            "coarse_value": "medium"
        },
        "user_type:premium_plus,subscribe": {
            "limit_to_highest_n_bits": 2,
            "fine_value": 3,
            "coarse_value": "high"
        }
    }
}
```





## サポートされるメソッド

各SKAdNetworkメソッドにコマンドをマッピングします。SKAdNetworkメソッドをトリガーするには、対応するコマンドを指定された形式で渡します。

| リモートコマンド | SKAdNetworkメソッド |
| :-- | :-- |
| `initialize` | `configure()` |
| `registerappforattribution` | `registerAppForAdNetworkAttribution()` |
| `setconversionbit` | `setConversionBit()` |
| `resetconversionbit` | `resetConversionBit()` |
| `setconversionvalue` | `setConversionValue()` |
| `resetconversionvalue` | `resetConversionValue()` |

これらのメソッドはすべてコンバージョン値に影響し、SKAdNetwork APIのコンバージョン値を更新します。

### 初期化

`send_higher_value`フラグをtrueに構成すると、低い値を除外し、高い値のみを送信できます。

| リモートコマンド | SKAdNetworkメソッド |
|---|---|
| `initialize`  | `configure()` |

| パラメーター | 型 |
|---|---|
| `send_higher_value` | `Bool` |

### アトリビューションへのアプリの登録

これはiOS 14未満で使用されていた古いメソッドです。iOS 14より古いバージョンをサポートする場合、コンバージョン値は報告できませんが、このメソッドを使用してインストールが発生したことを報告できます。
古いOSバージョンをサポートする場合、このメソッドは起動時に送信することを推奨します。

| リモートコマンド | SKAdNetworkメソッド |
|---|---|
| `registerappforattribution` | `registerAppForAdNetworkAttribution()` |

### コンバージョンビットの構成

コンバージョン値で立てるビットを指定できます。ビットがすでに立っている場合、詳細値は変更されないことに注意してください。

| リモートコマンド | SKAdNetworkメソッド |
|---|---|
| `setconversionbit` | `setConversionBit()` |

| パラメーター | 型 | 説明 |
|---|---|---|
| `bit_number` | `Int` | 0～5の数値 |
| `coarse_value` | `String` | このインストールの粗い値（low、medium、high） |
| `lock_window` | `Bool` | 現在のウィンドウ内でコンバージョン値を再度更新しない場合はtrue |

### コンバージョンビットのリセット

コンバージョン値でリセットするビットを指定できます。ビットをリセットするとコンバージョン値も自動的に低下するため、この処理は`send_higher_value`がfalseに構成されている場合にのみ実行されることに注意してください。

| リモートコマンド | SKAdNetworkメソッド |
|---|---|
| `resetconversionbit` | `resetConversionBit()` |

| パラメーター | 型 | 説明 |
|---|---|---|
| `bit_number` | `Int` | 0～5の数値 |
| `coarse_value` | `String` | このインストールの粗い値（low、medium、high） |
| `lock_window` | `Bool` | 現在のウィンドウ内でコンバージョン値を再度更新しない場合はtrue |

### コンバージョン値の構成

コンバージョン値を指定できます。`send_higher_value`がtrueの場合は、より高い値のみが採用されます。

| リモートコマンド | SKAdNetworkメソッド |
|---|---|
| `setconversionvalue` | `setConversionValue()` |

| パラメーター | 型 | 説明 |
|---|---|---|
| `fine_value` | `Int` | 0～63の数値。 |
| `coarse_value` | `String` | このインストールの粗い値（low、medium、high）。 |
| `lock_window` | `Bool` | 現在のウィンドウ内でコンバージョン値を再度更新しない場合はtrue。 |
| `limit_to_highest_n_bits` | `Int` | この値の表現に使用するビット数を上位ビットから指定する1～5の数値。デフォルトは6です。 |
| `limit_to_lowest_n_bits` | `Int` | この値の表現に使用するビット数を下位ビットから指定する1～5の数値。デフォルトは6です。 |

上位ビットまたは下位ビットのどちらか一方を起点とする制限のみを指定でき、両方を同時に指定することはできません。
### コンバージョン値のリセット

構成内の `send_higher_value` フラグを無視し、コンバージョン値を初期状態（詳細値 = 0、粗粒度値 = nil）にリセットします。

| リモートコマンド | SKAdNetwork メソッド |
|---|---|
| `resetconversionvalue` | `resetConversionValue()` |