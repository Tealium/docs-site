---
title: データソース
description: データソースとは、Tealium EventStreamにデータを送信する任意のシステムを指します。これらのシステムには、ウェブサイト、ネイティブモバイルアプリ、またはイベントデータを報告できる任意のカスタムアプリケーションが含まれます。
url: https://docs.tealium.com/ja/server-side/getting-started/eventstream-api-hub/data-sources/
---
データソースはプラットフォーム固有であり、インストールを完了するための必要なコードと指示を提供します。

データソースの例：

* ウェブ用JavaScript（Tealium iQタグ管理）
* iOS（Swift）
* Android
* Apple TV
* Roku
* サーバーサイドアプリ（Python、Java）
* HTTP API

ウェブサイトやアプリにTealiumを追加するには、まずデータソースを作成してインストールを完了するためのコードと指示を取得します。各データソースには、それがインストールされているプラットフォームを一意に識別する名前、説明、およびデータソースキーがあります。

## 仕組み

データソースは、アカウントにデータを送信するサイトやアプリを簡単に識別し、追跡するために使用されます。

以下にその仕組みを説明します：

1. Swift（iOS）、Android、またはWeb用JavaScriptなど、インストールしたいプラットフォームを選択し、`mydomain.com`や`MyBrandApp`のような名前を付けます。
1. インストール手順からサンプルコードとデータソースキーをコピーします。データソースキーは、作成したばかりのデータソースを一意に識別します。
1. コードがデータソースキーとともにインストールされた後、**Live Events**に移動して、そのデータソースから来るイベントを表示します。

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

次のチュートリアルでは、アカウントにデータソースを追加する方法を示します。

