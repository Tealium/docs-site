---
title: データソース
description: データソースとは、Tealium にデータを送信する任意のシステムです。これらのシステムには、Web サイト、ネイティブモバイルアプリ、イベントデータを送信できる任意のカスタムアプリケーションが含まれます。
url: https://docs.tealium.com/ja/server-side/getting-started/tutorials/event-data-activation/data-sources/
---
データソースはプラットフォーム固有であり、インストールを完了するために必要なコードと手順を提供します。

データソースの種類の例：

* Web 用 JavaScript（タグ管理）
* iOS（Swift）
* Android
* Apple TV
* Roku
* サーバーサイドアプリ（Python、Java）
* HTTP API

Web サイトまたはアプリに Tealium を追加するには、まずデータソースを作成し、インストールを完了するためのコードと手順を取得します。各データソースには、インストール先のプラットフォームを一意に識別する名前、説明、およびデータソースキーがあります。

## 仕組み

データソースを使用すると、アカウントにデータを送信するサイトやアプリを簡単に識別し、追跡できます。

仕組みは次のとおりです。

1. Swift（iOS）、Android、Web 用 JavaScript など、インストール先のプラットフォームを選択し、`mydomain.com` や `MyBrandApp` などの名前を付けます。
1. インストール手順からサンプルコードとデータソースキーをコピーします。データソースキーは、作成したデータソースを一意に識別します。
1. データソースキーを含むコードをインストールしたら、**ライブイベント**に移動し、そのデータソースから送信されるイベントを確認します。

データソースの例：

![](https://docs.tealium.com/images/tutorials/eventstream-getting-started-data-source-key.png)

インストールコードの例：

```swift
var tealConfig = TealiumConfig(
    account: "your_account",
    profile: "your_profile",
    environment: "prod",
    datasource: "abc123")

let tealium = Tealium(config: tealConfig)
```

次のチュートリアルでは、アカウントにデータソースを追加する方法を説明します。