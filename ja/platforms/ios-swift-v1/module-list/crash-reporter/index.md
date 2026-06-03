---
title: CrashReporter モジュール
description: アプリのクラッシュを自動的に追跡します。モジュールが有効化され、対応するフレームワークがインストールされると、アプリでクラッシュが発生するとクラッシュイベントがトリガーされます。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/crash-reporter/
---
##  使用法
CrashReporter モジュールは、アプリのクラッシュを自動的に追跡します。モジュールが有効化され、対応するフレームワークがインストールされると、アプリでクラッシュが発生するとクラッシュイベントがトリガーされます。

このフレームワークの使用は、アプリのクラッシュに関する重要な情報を得るために推奨されます。

以下のプラットフォームがサポートされています：

* iOS

## 要件

* `TealiumCrashReporteriOS`


## インストール

CocoaPods、Carthage、または手動で CrashReporter モジュールをインストールします。

### CocoaPods

CocoaPodsでCrashReporterモジュールをインストールするには：

1. Podfileに以下のpodを追加します：  
    ```ruby
    pod &#39;tealium-swift/Crash&#39;
    ```

2. 外部の `TealiumCrashReporteriOS` 依存関係と `TealiumAppData`、`TealiumDeviceData`、`Core` モジュールを自動的にインストールするには、以下のコマンドを実行します：
    ```ruby
    pod install
    ```

フレームワークは自動的にインスタンス化されます。pods `TealiumCore` と `TealiumCrashReporteriOS` に依存しています。iOSのCocoaPodsインストールについては[こちら](/ja/platforms/ios-swift-v1/install/#cocoapods)を参照してください。


### Carthage

以下のビデオは、Carthageを使用してCrashReporterモジュールをセットアップする方法を示しています：



フレームワークは自動的にインスタンス化されます。ただし、アプリにコンパイルされている必要があります（&#34;Embedded Binaries&#34;に含まれている）。`TealiumCore` と `TealiumCrashReporteriOS`（外部依存関係）に依存します。

1. [Swift Carthage インストール](/ja/platforms/ios-swift-v1/install/#carthage)の手順に従います。

2. コマンド `carthage update --platform iOS` を実行し、結果として得られたフレームワークをアプリに含めます：  
      - `TealiumCore.framework` &#43; すべての標準的な Tealium フレームワーク
      - `TealiumCrash.framework`
      - `TealiumCrashReporteriOS.framework`

3. [Carthage Getting Started](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) ガイドの指示に従って、App Storeにアプリを提出するための関連するBuild Phasesスクリプトを追加します。

### 手動

1. Swift [手動インストール](/ja/platforms/ios-swift-v1/install/#manual)の手順に従います。
2. [`TealiumCrashReporteriOS.framework`](https://github.com/Tealium/plcrashreporter)をダウンロードします。
3. `Tealium` と `TealiumCrash` スキームをビルドします。
4. 以下をXcodeのEmbedded Binariesセクションにドラッグアンドドロップします：
      - `TealiumCore.framework`
      - `TealiumCrash.framework`
      - `TealiumAppData.framework`
      - `TealiumDeviceData.framework`
      - `TealiumCrashReporteriOS.framework`



## データレイヤー
モジュールが有効化されている間、以下の変数が各トラッキングコールと共に送信されます：

| 変数  | 説明 | 例 |
| :-- | :-- | :-- |
| `crash_uuid` | この特定のクラッシュの一意の識別子 | `&#34;CC2DA0E9-E544-429A-AC5E-A268FC62F02A&#34;` |
| `device_memory_usage*`     | クラッシュ時のデバイス上のアプリの現在のメモリ使用量| `&#34;143.57MB&#34; ` |
| `app_memory_usage`          | クラッシュ時のデバイス上のアプリの現在のメモリ使用量| `&#34;143.57MB&#34;`  |
| `device_memory_available*` | クラッシュ時のデバイスの空きメモリ                         | `&#34;1068.88MB&#34;` |
| `memory_free`               | クラッシュ時のデバイスの空きメモリ                       | `&#34;1068.88MB&#34;` |
| `device_os_build`           | 現在のOSビルド番号                                              | `&#34;15E217&#34;`    |
| `crash_process_id`          | クラッシュ時のアプリのPID                                      | `&#34;84351&#34;`     |
| `crash_process_path`        | アプリが実行されていたパス                                       | `&#34;/DemoApp.app/DemoApp&#34;` |
| `crash_parent_process`      | アプリを起動した親プロセス                                 | `&#34;launchd_sim&#34;` |
| `crash_parent_process_id`   | 親プロセスのPID                                                   | `&#34;83183&#34;`      |
| `crash_name`                | 利用可能な場合のクラッシュのフレンドリーな名前                             | `&#34;Crash Name&#34;` |
| `crash_cause`               | クラッシュの原因                                                   | `&#34;Crash Reason&#34;` |
| `crash_signal_code`         | クラッシュを引き起こしたシグナルコード                                        | `&#34;#0&#34;` |
| `crash_signal_name`         | クラッシュを引き起こしたシグナル名                                        | `&#34;SIGABRT&#34;`    |
| `crash_signal_address`      | クラッシュのシグナルアドレス                                          | `&#34;4572945982&#34;` |
| `crash_libraries`           | クラッシュ時にロードされていたライブラリのリスト                    | ```[{&#34;baseAddress&#34;: &#34;0xa3e0000&#34;, &#34;codeType&#34;: { &#34;arch&#34;: 64, &#34;typeEncoding&#34;: &#34;Mach&#34;}, &#34;imageName&#34;: &#34;/Applications/Xcode9.3.app/Contents/ Developer/Platforms/iPhoneOS.platform/ Developer/Library/CoreSimulator/Profiles /Runtimes/iOS.simruntime/Contents/ Resources/RuntimeRoot/usr/lib/dyld_sim&#34;, &#34;imageSize&#34;: 212992, &#34;imageUuid&#34;: &#34;4015e9b70bde&#34;}]``` |
| `crash_threads`              | クラッシュ時のすべてのアクティブスレッド                  |```{&#34;crashed&#34;: 1,&#34;registers&#34;: {&#34;cs&#34;: &#34;0x07&#34;},&#34;stack&#34;: {&#34;instructionPointer&#34;: 4572945982,&#34;symbolInfo&#34;: {&#34;symbolName&#34;: &#34;&#34;,&#34;symbolStartAddr&#34;: 0},&#34;threadId&#34;: &#34;&#34;}}``` |

* これらの変数は、以前のリリースとの後方互換性のために複製されています

## クラッシュの呼び出し
`TealiumCrashReporteriOS.framework`がプロジェクトに追加されると、追加の初期化手順は必要ありません。クラッシュモジュールが有効化され、Tealium SDKが初期化されている限り、アプリでクラッシュが発生すると、クラッシュデータは自動的にトラッキングコールの一部となります。


## API リファレンス

### `invokeCrash()`

CrashReporter モジュールのクラッシュを呼び出します。

```swift
TealiumCrashReporter.invokeCrash(name, reason)
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- |  --- |
| `name` | `String` | クラッシュの名前  | `&#34;TEST_CRASH_NAME&#34;` |
| `reason` | `String` | クラッシュの理由 | `&#34;TEST_CRASH_REASON&#34;` |
