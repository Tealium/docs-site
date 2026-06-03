---
title: Install Referrerモジュールのインストール
description: ネイティブAndroid Install ReferrerモジュールのCordovaラッパーを提供します。
url: https://docs.tealium.com/ja/platforms/cordova-v1/module-list/install-referrer/
---
## インストール

この機能は別のNPMパッケージとして利用できます。

Install Referrerモジュールをインストールするには：

1. ターミナルウィンドウでCordovaアプリのディレクトリに移動します。

2. 次のコマンドを実行します：
      ```bash
      cordova plugin add tealium-cordova-installreferrer
      ```

## 初期化

Install Referrerモジュールを初期化するには：

1. メインのTealiumプラグインをインスタンス化するJavaScriptファイルを編集し、[`tealium.init()`](/ja/platforms/cordova-v1/api/#init)メソッドを呼び出した後で行います。

2. 次のコードを追加します：  
      ```javascript
      function tealiumInit(account, profile, environment, instance){
      var ir;
      tealium.init({...});
      // check if installreferrer is installed and available
      ir = window.tealiumInstallReferrer;
      if (ir) {
            // init install referrer and store any received values as persistent data
            ir.setPersistent(instance);
      }
      }
      ```

## テスト

プラグインがインストールされたら、システムブロードキャストを手動でトリガーしてテストします。

`com.tealium.sample`をあなたのアプリのRDNSバンドル識別子に置き換えます（Tealiumのサンプルアプリでテストする場合を除く）。

```bash
adb shell
am broadcast -a com.android.vending.INSTALL_REFERRER -n &#34;com.tealium.sample/com.tealium.installreferrer.InstallReferrerReceiver&#34; --es &#34;referrer&#34; &#34;utm_source=mysource&amp;utm_medium=mymedium&amp;utm_term=myterm&amp;utm_content=46b25e284dc36d5a7ef8f0e6b393febe3fcc8327&amp;utm_campaign=mycampname&#34;
```

## アンインストール

Install Referrerモジュールをアンインストールするには：

1. 次のコマンドを実行します：
      ```bash
      cordova plugin rm tealium-cordova-installreferrer
      ```

2. Install Referrerデータを永続保存から削除します：
      ```javascript
      tealium.removePersistent(&#34;install_referrer&#34;, &lt;your tealium instance name&gt;);
      ```
