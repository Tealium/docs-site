---
title: ConnectivityDataモジュール
description: ネットワーク接続を監視し、すべてのトラッキングイベントに接続情報を追加します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/connectivitydata/
---
ConnectivityDataモジュールはネットワーク接続を監視し、各トラッキングイベントに現在の接続タイプを追加します。

## データレイヤー

このモジュールが有効な間、以下の変数が各トラッキングコールに追加されます：

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `connection_type` | 現在のネットワーク接続タイプのリスト。<br>可能な値: `wifi`, `cellular`, `ethernet`, `none` | `["wifi", "cellular"]` |

## インストール



ConnectivityDataモジュールは`TealiumPrismCore`に含まれています。リポジトリURL `https://github.com/Tealium/tealium-prism-swift` を使用してSwift Package Managerの依存関係として追加するか、CocoaPodsのPodfileに追加してください：

```ruby
pod 'tealium-prism/Core'
```



## 初期化



`TealiumConfig`のmodulesパラメータに追加することでプログラム的にモジュールを構成します。

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
                              // 他のモジュール...
                          ])
```

