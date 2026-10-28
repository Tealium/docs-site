---
title: TealiumDataモジュール
description: すべてのトラッキングイベントのデータレイヤーに、Tealium SDKのコアメタデータを追加します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/tealiumdata/
---
TealiumDataモジュールは、Tealium SDKのコア構成とメタデータをトラッキングデータへ自動的に追加するコレクターです。このモジュールは常に有効であり、無効にすることはできません。

## データレイヤー

各トラッキング呼び出しに、次の変数が追加されます。

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `tealium_account` | Tealiumアカウント識別子 | `"my_account"` |
| `tealium_profile` | Tealiumプロファイル識別子 | `"my_profile"` |
| `tealium_environment` | Tealium環境 | `"prod"` |
| `tealium_datasource` | 構成されている場合はデータソース識別子 | `"abc123"` |
| `tealium_library_name` | Tealiumライブラリの名前 | `"prism-swift"`, `"prism-kotlin"` |
| `tealium_library_version` | Tealiumライブラリのバージョン | `"0.7.0"` |
| `tealium_visitor_id` | 一意の訪問識別子 | `"612040730c8c11ed"` |
| `enabled_modules` | 有効なモジュールIDのリスト | `["AppData", "Lifecycle"]` |
| `enabled_modules_versions` | 有効なモジュールのバージョン | `["0.7.0", "0.7.0"]` |
| `tealium_random` | イベントの重複排除に使用するランダムな16桁の数値 | `"7715219888555792"` |

## インストール

TealiumDataモジュールは、Tealium PrismコアSDKの一部です。個別にインストールする必要はありません。



このモジュールは`prism-core`に含まれており、これは他のすべてのPrismモジュールの推移的依存関係です。


このモジュールは`TealiumPrismCore`に含まれています。リポジトリURL `https://github.com/Tealium/tealium-prism-swift`を使用してSwift Package Managerの依存関係として追加するか、CocoaPods用のPodfileに追加します。

```ruby
pod 'tealium-prism/Core'
```

代わりにPrismライブラリ全体をインストールするには、次のようにします。

```ruby
pod 'tealium-prism'
```



## 初期化

TealiumDataモジュールは自動的に初期化されます。


<blockquote>
このモジュールは常に有効であり、無効にすることはできません。`setEnabled(false)`を呼び出しても効果はありません。
</blockquote>
