---
title: TealiumData モジュール
description: すべてのトラッキングイベントについて、Tealium SDK のコアメタデータをデータレイヤーに追加します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/tealiumdata/
---
TealiumData モジュールは、Tealium SDK のコア構成とメタデータを使用してトラッキングデータを自動的に拡充するコレクターです。このモジュールは常に有効であり、無効にすることはできません。

## データレイヤー

各トラッキング呼び出しに、次の変数が追加されます。

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `tealium_account` | Tealium アカウント識別子 | `"my_account"` |
| `tealium_profile` | Tealium プロファイル識別子 | `"my_profile"` |
| `tealium_environment` | Tealium 環境 | `"prod"` |
| `tealium_datasource` | 構成されている場合のデータソース識別子 | `"abc123"` |
| `tealium_library_name` | Tealium ライブラリの名前 | `"prism-swift"`, `"prism-kotlin"` |
| `tealium_library_version` | Tealium ライブラリのバージョン | `"0.7.0"` |
| `tealium_visitor_id` | 一意の訪問識別子 | `"612040730c8c11ed"` |
| `enabled_modules` | 有効なモジュール ID のリスト | `["AppData", "Lifecycle"]` |
| `enabled_modules_versions` | 有効なモジュールのバージョン | `["0.7.0", "0.7.0"]` |
| `tealium_random` | イベントの重複排除に使用するランダムな16桁の数値 | `"7715219888555792"` |

## インストール

TealiumData モジュールは、Tealium Prism コア SDK の一部です。個別にインストールする必要はありません。



このモジュールは `prism-core` に含まれています。`prism-core` は、他のすべての Prism モジュールの推移的依存関係です。


このモジュールは `TealiumPrismCore` に含まれています。リポジトリ URL `https://github.com/Tealium/tealium-prism-swift` を使用して Swift Package Manager の依存関係として追加するか、CocoaPods 用の Podfile に追加します。

```ruby
pod 'tealium-prism/Core'
```

代わりに Prism ライブラリ全体をインストールするには、次を使用します。

```ruby
pod 'tealium-prism'
```



## 初期化

TealiumData モジュールは自動的に初期化されます。


<blockquote>
このモジュールは常に有効であり、無効にすることはできません。`setEnabled(false)` を呼び出しても効果はありません。
</blockquote>
