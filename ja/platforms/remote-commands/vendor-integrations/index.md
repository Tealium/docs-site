---
title: ベンダー統合
description: ベンダー統合は、ベンダーのSDKをインストールし、ベンダーのAPIのネイティブコードハンドラを定義する事前に構築されたリモートコマンドモジュールです。
url: https://docs.tealium.com/ja/platforms/remote-commands/vendor-integrations/
---
## 要件

ベンダー統合を実装するには、以下が必要です：

* **ベンダーのリモートコマンドモジュール**  
アプリのビルドスクリプトで、ベンダーのSDKをTealiumのリモートコマンドモジュールに置き換えます。リモートコマンドモジュールは、ベンダーのSDKのインストールとセットアップを処理します。
[リモートコマンドベンダー統合のリスト](/ja/platforms/remote-commands/integrations/)を参照してください。

* **構成** (以下のいずれかを選択)
  * **JSONファイル**  
  ベンダーの構成、データマッピング、イベントトリガーを含むJSONファイル。ローカルにロードするか、リモートでホストすることができます。[JSONファイル仕様](/ja/platforms/remote-commands/json-file/)を参照してください。
  * **リモートコマンドタグ**  
  iQタグ管理にあるタグ。ベンダーのAPIの構成オプションを提供します（タグ管理モジュールと共に使用）。

## 仕組み

以下の図は、ベンダー統合とカスタムリモートコマンドがネイティブアプリの機能をどのようにトリガーするかを示しています。アプリで追跡された訪問の購入から始まり、Tealium SDKはFirebase、Facebook、または独自のカスタムリモートコマンドのようなアプリでリモートコマンドをトリガーします。リモートコマンドは、Firebaseでの購入のログ記録、Facebook App Eventsでのイベント追跡、またはアプリでのカスタム通知の表示など、SDKで利用可能な任意のネイティブメソッドをトリガーすることができます。

![](/images/platforms/remote-commands/remote_commands_data_flow_diagram.png)
