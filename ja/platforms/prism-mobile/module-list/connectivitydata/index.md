---
title: ConnectivityData モジュール
description: ネットワーク接続を監視し、すべてのトラッキングイベントに接続情報を追加します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/connectivitydata/
---
ConnectivityData モジュールはネットワーク接続を監視し、現在の接続タイプをすべてのトラッキングイベントに追加します。

## データレイヤー

モジュールが有効になっている間、各トラッキング呼び出しに次の変数が追加されます。

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `connection_type` | 現在のネットワーク接続タイプ。<br>指定可能な値：`wifi`、`cellular`、`ethernet`、`none`、`unknown` | `"wifi"` |

## インストール



ConnectivityData モジュールは `TealiumPrismCore` に含まれています。リポジトリURL `https://github.com/Tealium/tealium-prism-swift` を使用してSwift Package Managerの依存関係として追加するか、CocoaPods用のPodfileに追加します。

```ruby
pod 'tealium-prism/Core'
```



## 初期化



`TealiumConfig` のmodulesパラメータにモジュールを追加して、プログラムで構成します。

モジュール構成の詳細については、[`ModuleSettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/ModuleSettingsBuilder.html)を参照してください。

```swift
let config = TealiumConfig(account: "ACCOUNT",
                          profile: "PROFILE", 
                          environment: "dev",
                          modules: [
                              Modules.connectivityData(forcingSettings: { builder in
                                  builder.setEnabled(true)
                                         .setOrder(1)
                                         .setRules(.and(["rule_id_from_settings"]))
                              }),
                              // other modules...
                          ])
```

