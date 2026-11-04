---
title: ベンダー統合
description: ベンダー統合は、ベンダーSDKをインストールし、ベンダーAPI用のネイティブコードハンドラーを定義する、構築済みのリモートコマンドモジュールです。
url: https://docs.tealium.com/ja/platforms/remote-commands/vendor-integrations/
---
## 要件

ベンダー統合を実装するには、以下が必要です。

* **ベンダーのリモートコマンドモジュール**  
アプリのビルドスクリプトで、ベンダーSDKをTealiumリモートコマンドモジュールに置き換えます。リモートコマンドモジュールが、ベンダーSDKのインストールとセットアップを処理します。
[リモートコマンドのベンダー統合一覧](https://docs.tealium.com/ja/platforms/remote-commands/integrations/)を参照してください。

* **構成**（以下のいずれかを選択）
  * **JSONファイル**  
  ローカルから読み込むか、リモートでホストされるJSONファイルで、ベンダー構成、データマッピング、イベントトリガーが含まれます。[JSONファイル仕様](https://docs.tealium.com/ja/platforms/remote-commands/json-file/)を参照してください。
  * **リモートコマンドタグ**  
  ベンダーAPIの構成オプションを提供するタグ管理内のタグです（タグ管理モジュールで使用）。

## 仕組み

以下の図は、ベンダー統合とカスタムリモートコマンドが、ネイティブアプリ内の機能をトリガーする仕組みを示しています。アプリ内で追跡された訪問の購入を起点として、Tealium SDKはFirebase、Facebook、または独自のカスタムリモートコマンドなどのアプリでリモートコマンドをトリガーします。リモートコマンドは、Firebaseでの購入の記録、Facebook App Eventsでのイベントの追跡、アプリ内でのカスタム通知の表示など、SDKで利用可能な任意のネイティブメソッドをトリガーできます。

![](https://docs.tealium.com/images/platforms/remote-commands/remote_commands_data_flow_diagram.png)