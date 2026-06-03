---
title: 広告識別子モジュール
description: ネイティブのAndroid Ad IdentifierモジュールとiOS Advertising Identifier (IDFA)のCordovaラッパーを提供します。
url: https://docs.tealium.com/ja/platforms/cordova-v1/module-list/adid/
---
## インストール

広告識別子モジュールをインストールするには：

1. ターミナルウィンドウでCordovaアプリのディレクトリに移動します

2. 次のコマンドを実行します：
      ```bash
      cordova plugin add tealium-cordova-adidentifier
      ```

広告識別子モジュールはGoogle Play Services Adsモジュールに依存しています。アプリが起動時にクラッシュするのを防ぐために、[AdMob App ID](https://developers.google.com/admob/android/quick-start)をアプリの`AndroidManifest.xml`ファイルに追加してください。

## 初期化

広告識別子モジュールを初期化するには：

1. `tealium.init`を呼び出した後、メインのTealiumプラグインをインスタンス化するJavaScriptファイルを編集します。

2. 次のコードを追加します：  
      ```javascript
      function tealiumInit(account, profile, environment, instance){
      var ai;
      tealium.init({...});
      // installreferrerがインストールされ利用可能かどうかを確認

      ai = window.tealiumAdIdentifier;
      if (ai) {
            ai.setPersistent(instance);
      }
      }
      ```

## データレイヤー
広告識別子モジュールは以下の変数をデータレイヤーに追加します：

**Android**
* `google_adid`

**iOS**
* `device_advertising_id`
* `device_advertising_vendor_id`
*  `device_advertising_enabled`

## アンインストール

広告識別子モジュールをアンインストールするには：

1. 次のコマンドを実行します：
      ```bash
      cordova plugin rm tealium-cordova-adidentifier
      ```

2. 永続保存から広告識別子データを削除します：
      ```javascript
      // android only
      tealium.removePersistent(&#34;google_adid&#34;, &lt;your tealium instance name&gt;);

      // ios only
      tealium.removePersistent(&#34;device_advertising_id&#34;, &lt;your tealium instance name&gt;);
      tealium.removePersistent(&#34;device_advertising_vendor_id&#34;, &lt;your tealium instance name&gt;);
      tealium.removePersistent(&#34;device_advertising_enabled&#34;, &lt;your tealium instance name&gt;);
      ```
