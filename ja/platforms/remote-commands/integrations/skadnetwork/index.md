---
title: リモートコマンド：SKAdNetwork
description: Swift向けのAppleのSKAdNetworkのTealiumリモートコマンド統合。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/skadnetwork/
---
[SKAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork)は、広告主が広告キャンペーンの成功を測定するために使用するAppleのSDKであり、ユーザーのプライバシーを保護します。

## 必要条件

  - [Tealium for iOS-Swift](/ja/platforms/ios-swift/) (2.9.0&#43;)
  - [SKAdNetworkリモートコマンドJSONファイル](/ja/platforms/remote-commands/integrations/skadnetwork/#json-template)

## 動作方法

SKAdNetwork統合には2つのアイテムが使用されます。

1. SKAdNetwork変換値を送信するリモートコマンドモジュール
2. イベントトラッキングを変換値に変換するためのJSON構成ファイルまたはリモートコマンドタグ

JSON構成ファイルは、この統合の推奨オプションであり、アプリ内またはリモートでホストされます。iQ Tag Managementを使用している場合は、ベンダー統合のためにリモートコマンドタグを追加します。[ベンダー統合](/ja/platforms/remote-commands/how-it-works/#vendor-integrations)について詳しくは、こちらをご覧ください。

## インストール

### 依存関係マネージャー




1. Xcodeプロジェクトで、「**ファイル &gt; パッケージの追加... &gt; パッケージの依存関係を追加**」を選択します。
2. リポジトリのURL `https://github.com/tealium/tealium-ios-skadnetwork-remote-command` を入力します。
3. バージョンルールを構成します。通常は「次のメジャーバージョンまで」が推奨されます。現在の`TealiumSKAdNetwork`バージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットします。
4. インストールする`TealiumSKAdNetwork`モジュールを選択し、モジュールをインストールするアプリのターゲットを選択します。
5. プロジェクトに複数のアプリターゲットがある場合で、`TealiumSKAdNetwork`モジュールを他のアプリターゲットに追加する必要がある場合は、**フレームワーク、ライブラリ、および埋め込みコンテンツ**セクションに手動で追加する必要があります。

追加のアプリターゲットに`TealiumSKAdNetwork`をインストールするには:

1. **プロジェクトナビゲーター**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトで、**TARGETS**セクションのアプリターゲットを選択します。
3. **一般 &gt; フレームワーク、ライブラリ、および埋め込みコンテンツ**に移動し、`TealiumSKAdNetwork`モジュールをアプリターゲットに追加します。




1. Podfileに`pod &#34;tealium-swift&#34;`と`pod &#34;SKAdNetwork&#34;`が存在する場合は、削除します。`tealium-swift`の依存関係は、すでに`TealiumSKAdNetwork`フレームワークに含まれています。

2. Podfileに次の依存関係を追加します:
      ```ruby
      pod &#34;TealiumSKAdNetwork&#34;
      ```  
      `TealiumSKAdNetwork`ポッドには、次の`TealiumSwift`の依存関係が含まれています:  
      ```bash
      &#34;tealium-swift/Core&#34;
      &#34;tealium-swift/RemoteCommands&#34;
      ```

3. インストール時にディスパッチャーポッドを含める必要があります。`tealium-swift/Collect`または`tealium-swift/TagManagement`のいずれかを選択し、他の個別のサブモジュールもPodfileに含めます。例:
      ```ruby
      pod &#34;TealiumSKAdNetwork&#34;
      pod &#34;tealium-swift/Collect&#34;
      pod &#34;tealium-swift/Lifecycle&#34;
      pod &#34;tealium-swift/Attribution&#34;
      ```

4. `TealiumSwift`モジュールと`TealiumSKAdNetwork`モジュールを`TealiumHelper`ファイルと、`Tealium`クラスにアクセスする他のファイルにインポートします。




1. Cartfileから`tealium-swift`を削除します。`tealium-swift`の依存関係は、すでに`TealiumSKAdNetwork`フレームワークに含まれています。

2. Cartfileに次の行が存在する場合は、削除します:  
      ```bash
      github &#34;skadnetwork/ios_sdk&#34;
      ```

3. Cartfileに次の依存関係を追加します:  
      ```bash
      github &#34;tealium/tealium-ios-skadnetwork-remote-command&#34;
      ```




### 手動インストール

SKAdNetworkリモートコマンドの手動インストールには、[Tealium for Swift](/ja/platforms/ios-swift/)ライブラリのインストールが必要です。iOSプロジェクトにSKAdNetworkリモートコマンドをインストールするには、次の手順を実行します。

1. [SKAdNetwork SDK](https://github.com/skadnetwork/ios_sdk)をインストールします（まだインストールしていない場合）。

2. [Tealium iOS SKAdNetworkリモートコマンド](https://github.com/tealium/tealium-ios-skadnetwork-remote-command)リポジトリをクローンし、`Sources`フォルダ内のファイルをプロジェクトにドラッグします。

3. [`remoteAPIEnabled`](/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。

## 初期化

JSON構成ファイルまたはTealiumのiOS（Swift）ライブラリのリモートコマンドタグを使用して、リモートコマンドを初期化します。

以下のコードは、ローカルファイルオプションを使用したJSONリモートコマンド機能に対応するように設計されています:  
```swift
var tealium : Tealium?
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;,
                           optionalData: nil)

config.remoteAPIEnabled = true // リモートコマンドを使用するために必要
config.dispatchers = [Dispatchers.RemoteCommands, Dispatchers.Collect]

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

    // Webviewタグ
    let skadnetwork = SKAdNetworkRemoteCommand(delegate: self)

    // ローカルJSON
    //let skadnetwork = SKAdNetworkRemoteCommand(type: .local(file: &#34;skadnetwork&#34;), delegate: self)

    // リモートJSON
    //let skadnetwork = SKAdNetworkRemoteCommand(type: .remote(url: &#34;https://some.domain.com/skadnetwork.json&#34;), delegate: self)

	remoteCommands.add(skadnetwork)
}
```

### デリゲート

デリゲートはオプションのパラメータであり、変換の更新と完了時の呼び出しを受け取るために使用され、エラーのデバッグと処理、およびトラッキングも行うことができます。

```swift
    /// 新しい変換値を送信する必要があると検出した場合
    func onConversionUpdate(conversionData: ConversionData, lockWindow: Bool)
    /// 新しい変換値が送信され、完了した場合、オプションでエラーも含まれます
    func onConversionUpdateCompleted(error: Error?)
}
```

### JSONテンプレート

リモートコマンドを構成する場合は、[JSON構成ファイル](/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用する場合、次のテンプレートを参照して開始します。必要に応じてマッピングを編集します。




テンプレートには、シンプルな値の帰属戦略の共通マッピングが含まれています。いくつかのイベントで送信する細かい値と粗い値をマッピングしています。

```json
{
    &#34;config&#34;: {
      &#34;send_higher_value&#34;: true
    },
    &#34;mappings&#34;: {
        &#34;fine_value&#34;:&#34;fine_value&#34;,
        &#34;coarse_value&#34;:&#34;coarse_value&#34;
    },
    &#34;commands&#34;: {
        &#34;launch&#34;: &#34;initialize,registerappforattribution,setconversionvalue&#34;,
        &#34;register&#34;: &#34;setconversionvalue&#34;,
        &#34;login&#34;: &#34;setconversionvalue&#34;,
        &#34;tutorial&#34;: &#34;setconversionvalue&#34;,
        &#34;addtocart&#34;: &#34;setconversionvalue&#34;,
        &#34;purchase&#34;: &#34;setconversionvalue&#34;,
        &#34;user_type:premium,subscribe&#34;: &#34;setconversionvalue&#34;
    },
    &#34;statics&#34;: {
        &#34;launch&#34;: {
            &#34;fine_value&#34;: 0,
            &#34;coarse_value&#34;: &#34;low&#34;
        }
}
```




テンプレートには、標準のイベントベースの帰属戦略の共通マッピングが含まれています。各イベントは、変換値の6ビットのうちの1つにマップされます。

```json
{
    &#34;config&#34;: {
      &#34;send_higher_value&#34;: true
    },
    &#34;mappings&#34;: {
        &#34;bit_number&#34;:&#34;bit_number&#34;,
        &#34;fine_value&#34;:&#34;fine_value&#34;,
        &#34;coarse_value&#34;:&#34;coarse_value&#34;
    },
    &#34;commands&#34;: {
        &#34;launch&#34;: &#34;initialize,registerappforattribution,setconversionvalue&#34;,
        &#34;register&#34;: &#34;setconversionbit&#34;,
        &#34;login&#34;: &#34;setconversionbit&#34;,
        &#34;tutorial&#34;: &#34;setconversionbit&#34;,
        &#34;addtocart&#34;: &#34;setconversionbit&#34;,
        &#34;purchase&#34;: &#34;setconversionbit&#34;,
        &#34;user_type:premium,subscribe&#34;: &#34;setconversionbit&#34;
    },
    &#34;statics&#34;: {
        &#34;launch&#34;: {
            &#34;fine_value&#34;: 0,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;register&#34;: {
            &#34;bit_number&#34;: 0,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;login&#34;: {
            &#34;bit_number&#34;: 1,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;tutorial&#34;: {
            &#34;bit_number&#34;: 2,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;addtocart&#34;: {
            &#34;bit_number&#34;: 3,
            &#34;coarse_value&#34;: &#34;medium&#34;
        },
        &#34;purchase&#34;: {
            &#34;bit_number&#34;: 4,
            &#34;coarse_value&#34;: &#34;high&#34;
        },
        &#34;user_type:premium,subscribe&#34;: {
            &#34;bit_number&#34;: 5,
            &#34;coarse_value&#34;: &#34;high&#34;
        },
    }
}
```





テンプレートには、混合帰属戦略の共通マッピングが含まれています。6つのビットのうち2つを値の格納に使用し、4つのビットをイベントのエンコードに使用します。

```json
{
    &#34;config&#34;: {
      &#34;send_higher_value&#34;: true
    },
    &#34;mappings&#34;: {
        &#34;bit_number&#34;:&#34;bit_number&#34;,
        &#34;fine_value&#34;:&#34;fine_value&#34;,
        &#34;coarse_value&#34;:&#34;coarse_value&#34;,
        &#34;limit_to_highest_n_bits&#34;: &#34;limit_to_highest_n_bits&#34;,
        &#34;limit_to_lowest_n_bits&#34;: &#34;limit_to_lowest_n_bits&#34;
    },
    &#34;commands&#34;: {
        &#34;launch&#34;: &#34;initialize,registerappforattribution,setconversionvalue&#34;,
        &#34;register&#34;: &#34;setconversionbit&#34;,
        &#34;login&#34;: &#34;setconversionbit&#34;,
        &#34;tutorial&#34;: &#34;setconversionbit&#34;,
        &#34;addtocart&#34;: &#34;setconversionbit&#34;,
        &#34;purchase&#34;: &#34;setconversionbit&#34;,
        &#34;subscribe&#34;: &#34;setconversionvalue&#34;
    },
    &#34;statics&#34;: {
        &#34;launch&#34;: {
            &#34;fine_value&#34;: 0,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;register&#34;: {
            &#34;bit_number&#34;: 0,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;login&#34;: {
            &#34;bit_number&#34;: 1,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;tutorial&#34;: {
            &#34;bit_number&#34;: 2,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;addtocart&#34;: {
            &#34;bit_number&#34;: 3,
            &#34;coarse_value&#34;: &#34;medium&#34;
        },
        &#34;purchase&#34;: {
            &#34;bit_number&#34;: 4,
            &#34;coarse_value&#34;: &#34;high&#34;
        },
        &#34;user_type:common,subscribe&#34;: {
            &#34;limit_to_highest_n_bits&#34;: 2,
            &#34;fine_value&#34;: 1,
            &#34;coarse_value&#34;: &#34;low&#34;
        },
        &#34;user_type:premium,subscribe&#34;: {
            &#34;limit_to_highest_n_bits&#34;: 2,
            &#34;fine_value&#34;: 2,
            &#34;coarse_value&#34;: &#34;medium&#34;
        },
        &#34;user_type:premium_plus,subscribe&#34;: {
            &#34;limit_to_highest_n_bits&#34;: 2,
            &#34;fine_value&#34;: 3,
            &#34;coarse_value&#34;: &#34;high&#34;
        }
    }
}
```





## サポートされているメソッド

以下のメソッドは、変換値を変更するために使用され、これらのコマンドからのデータマッピングをトリガーとします。

| リモートコマンド | SKAdNetworkメソッド |
| :-- | :-- |
| `initialize` | `configure()` |
| `registerappforattribution` | `registerAppForAdNetworkAttribution()` |
| `setconversionbit` | `setConversionBit()` |
| `resetconversionbit` | `resetConversionBit()` |
| `setconversionvalue` | `setConversionValue()` |
| `resetconversionvalue` | `resetConversionValue()` |

これらのメソッドはすべて変換値に影響を与え、SKAdNetwork APIの変換値の更新を引き起こします。

### Initialize

`send_higher_value`フラグをtrueに構成して、低い値をフィルタリングし、高い値のみを送信することができます。

| リモートコマンド | SKAdNetworkメソッド |
|---|---|
| `initialize`  | `configure()` |

|  パラメーター | 型 |
|---|---|
|  `send_higher_value` | `Bool` |

### Register App For Attribution

これは、iOS &lt; 14向けの古いメソッドです。iOSバージョン14より古いバージョンをサポートしている場合、変換値を報告することはできませんが、このメソッドを使用してインストールが行われたことを報告することはできます。
このメソッドは、おそらく古いOSバージョンをサポートしている場合に、起動時に送信する必要があります。

| リモートコマンド | SKAdNetworkメソッド |
|---|---|
| `registerappforattribution` | `registerAppForAdNetworkAttribution()` |

### Set Conversion Bit

変換値で上げるビットを指定することができます。ただし、ビットがすでに上げられている場合、細かい値は変更されません。

| リモートコマンド | SKAdNetworkメソッド |
|---|---|
| `setconversionbit` | `setConversionBit()` |

|  パラメーター | 型 | 説明 |
|---|---|---|
| `bit_number` | `Int` | 0から5までの数値 |
| `coarse_value` | `String` | このインストールの粗い値（low-medium-high） |
| `lock_window` | `Bool` | 現在のウィンドウで変換値を再度更新したくない場合はtrue |

### Reset Conversion Bit

変換値でリセットするビットを指定することができます。ただし、これは`send_higher_value`がfalseに構成されている場合にのみ発生します。ビットをリセットすると、変換値が自動的に低下するためです。

| リモートコマンド | SKAdNetworkメソッド |
|---|---|
| `resetconversionbit` | `resetConversionBit()` |

|  パラメーター | 型 | 説明 |
|---|---|---|
| `bit_number` | `Int` | 0から5までの数値 |
| `coarse_value` | `String` | このインストールの粗い値（low-medium-high） |
| `lock_window` | `Bool` | 現在のウィンドウで変換値を再度更新したくない場合はtrue |

### Set Conversion Value

変換値を指定することができます。`send_higher_value`がtrueの場合、高い値のみが取得されます。

| リモートコマンド | SKAdNetworkメソッド |
|---|---|
| `setconversionvalue` | `setConversionValue()` |

|  パラメーター | 型 | 説明 |
|---|---|---|
| `fine_value` | `Int` | 0から63までの数値 |
| `coarse_value` | `String` | このインストールの粗い値（low-medium-high） |
| `lock_window` | `Bool` | 現在のウィンドウで変換値を再度更新したくない場合はtrue |
| `limit_to_highest_n_bits` | `Int` | 1から5までの数値で、この値を表すために使用するビット数を指定します。デフォルトは6です。 |
| `limit_to_lowest_n_bits` | `Int` | 1から5までの数値で、この値を表すために使用するビット数を指定します。デフォルトは6です。 |

最上位ビットまたは最下位ビットのどちらかから制限を指定できますが、両方を指定することはできません。

### Reset Conversion Value

構成の`send_higher_value`フラグを無視し、変換値を開始状態（fine value = 0、coarse value = nil）にリセットします。

| リモートコマンド | SKAdNetworkメソッド |
|---|---|
| `resetconversionvalue` | `resetConversionValue()` |