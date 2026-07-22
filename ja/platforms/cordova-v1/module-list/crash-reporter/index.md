---
title: クラッシュレポーターモジュール
description: Android用のネイティブクラッシュレポーターモジュールのCordovaラッパーを提供します（現時点ではiOSはサポートされていません）。
url: https://docs.tealium.com/ja/platforms/cordova-v1/module-list/crash-reporter/
---
## インストール

クラッシュレポーターモジュールをインストールするには：

1. ターミナルウィンドウでCordovaアプリのディレクトリに移動します。

2. 次のコマンドを実行します：
      ```bash
      cordova plugin add tealium-cordova-crashreporter
      ```

## 初期化

クラッシュレポーターモジュールの明示的な初期化は必要ありません。

`isCrashReporterEnabled` パラメータが構成オブジェクトに構成されている場合、Tealiumのコアプラグインによってインスタンス化されます。以下の例を参照してください：

```javascript
function tealiumInit(account, profile, environment, instance) {
    tealium.init({
       account : account,
       profile : profile,
       environment : environment,
       instance : instance,
       isLifecycleEnabled: "true",
       isCrashReporterEnabled: "true"
    });
}
```

## テスト

JavaScript APIはクラッシュを強制的にトリガーするメソッドを公開しています。本番環境でのクラッシュの誤発動を避けるため、このメソッドは以下の条件が満たされた場合にのみ機能するようにハードコーディングされています：

*   環境が `dev` に構成されている
*   クラッシュレポーターモジュールがインストールされている
*   クラッシュレポーターモジュールが正常に初期化されている
*   データレイヤーに `forceCrash` 変数が存在する

上記の条件が満たされている場合、[`trackView()`](https://docs.tealium.com/ja/platforms/cordova-v1/api/#trackview) メソッドを使用して `forceCrash` 変数を含むトラッキングコールを発行してクラッシュをトリガーします：

```javascript
tealium.trackView({"forceCrash":"true"});
```

## アンインストール

クラッシュレポーターモジュールをアンインストールするには：

1. 次のコマンドを実行します：
      ```bash
      cordova plugin rm tealium-cordova-crashreporter
      ```  

2. Tealiumのメインプラグインを初期化する際、構成オブジェクトから `isCrashReporterEnabled` フラグを削除します。