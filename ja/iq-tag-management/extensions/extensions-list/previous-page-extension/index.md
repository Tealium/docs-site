---
title: 前のページ拡張
description: 前のページ拡張は、前のページの名前を次のページで使用するために保持するために使用されます。
url: https://docs.tealium.com/ja/iq-tag-management/extensions/extensions-list/previous-page-extension/
---
## 前提条件

* utag v4.38以降。`utag.js`テンプレートの更新についての詳細は、当社のナレッジベースの記事[utag.jsの最新バージョンへの更新のベストプラクティス](https://support.tealiumiq.com/en/support/solutions/articles/36000363470)を参照してください。
* [拡張機能の動作方法]()

## 動作方法

前のページ拡張は、データレイヤーに`previous_page_name`という名前の変数を追加します。この変数の値は、前のページのデータレイヤー変数の値に構成されます。ページ名として使用するデータレイヤー変数を指定し、拡張機能はこの値をクッキーに保存して、次のページで使用できるようにします。

ここに`page_name`が使用される簡単な例を示します。訪問が一連のページを通過する際に`previous_page_name`で期待する値を示しています。`previous_page_name`はセッションの最初のページでは構成されていないことに注意してください。

|**ページ**| `page_name` | `previous_page_name`|
|---| ---| ---|
|ホームページ| `Home - Welcome` | (構成なし)|
|検索ページ| `Search for iPhone` | `Home - Welcome` |
|製品ページ| `iPhone 10 Product Details` | `Search for iPhone` |

## 拡張機能の使用

拡張機能が追加されると、次の構成オプションが利用可能になります：

* **ページ値**：ページの名前を含むデータレイヤー変数を選択します。

拡張機能は自動的にこの変数の値を保存し、次のページビューで`previous_page_name`に構成します。
