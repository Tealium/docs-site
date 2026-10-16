---
title: TealiumDataモジュール
description: 各トラッキングイベントに対して、Tealium SDKのコアメタデータをデータレイヤーに追加します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/tealiumdata/
---
TealiumDataモジュールは、トラッキングデータをTealium SDKのコア構成とメタデータで自動的にエンリッチするコレクターです。このモジュールは常にアクティブであり、無効にすることはできません。

## データレイヤー

以下の変数が各トラッキングコールに追加されます：

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `tealium_account` | Tealiumアカウント識別子 | `"my_account"` |
| `tealium_profile` | Tealiumプロファイル識別子 | `"my_profile"` |
| `tealium_environment` | Tealium環境 | `"prod"` |
| `tealium_datasource` | データソース識別子（構成されている場合） | `"abc123"` |
| `tealium_library_name` | Tealiumライブラリの名前 | `"tealium-prism-swift"` |
| `tealium_library_version` | Tealiumライブラリのバージョン | `"0.4.0"` |
| `tealium_visitor_id` | ユニークな訪問識別子 | `"612040730c8c11ed"` |
| `enabled_modules` | 有効なモジュールIDのリスト | `["AppData", "Lifecycle"]` |
| `enabled_modules_versions` | 有効なモジュールのバージョン | `["1.0.0", "1.0.0"]` |
| `tealium_random` | イベント重複排除用のランダム16桁の数値 | `"7715219888555792"` |

## インストール

TealiumDataモジュールはTealium PrismコアSDKの一部です。別途インストールは必要ありません。



このモジュールは`prism-core`に含まれており、他のすべてのPrismモジュールの推移的依存関係です。


このモジュールは`TealiumPrismCore`に含まれています。リポジトリURL `https://github.com/Tealium/tealium-prism-swift` を使用してSwift Package Managerの依存関係として追加するか、CocoaPodsのためにPodfileに追加してください：

```ruby
pod 'tealium-prism/Core'
```

代わりに全てのPrismライブラリをインストールする場合：

```ruby
pod 'tealium-prism'
```



## 初期化

TealiumDataモジュールは自動的に初期化されます。


<blockquote>
このモジュールは常にアクティブであり、無効にすることはできません。`setEnabled(false)`を呼び出しても効果はありません。
</blockquote>
