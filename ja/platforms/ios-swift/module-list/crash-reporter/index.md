---
title: CrashReporterモジュール
description: このモジュールはアプリのクラッシュを自動的に追跡します。モジュールが有効になり、関連するフレームワークがインストールされた後、アプリがクラッシュするとクラッシュイベントがトリガーされます。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/crash-reporter/
---
##  使用方法

CrashReporterモジュールは、アプリのクラッシュを自動的に追跡します。モジュールが有効になり、関連するフレームワークがインストールされた後、アプリでクラッシュが発生するとクラッシュデータが追跡イベントに追加されます。

オプションとして、`sendCrashDataOnCrashDetected` 構成フラグを `true` に構成することで、追加の `crash` イベントを送信するようにSDKを構成できます。この構成を行うと、クラッシュデータはこの特定のイベントにのみ追加されます。

このフレームワークの使用は、アプリのクラッシュに関する重要な情報を得るために推奨されます。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* macOS

## インストール

Swift Package ManagerまたはCocoaPodsでCrashモジュールをインストールします。

### Swift Package Manager（推奨）

バージョン1.9.0以降でサポートされているSwift Package Managerは、Tealium Swiftライブラリをインストールするための推奨される最も簡単な方法です：

1. Xcodeプロジェクトで **File &gt; Add Package Dependencies** を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift-crash-reporter`
1. バージョンルールを構成します。通常、`&#34;Up to next major&#34;` が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. `TealiumCrashModule` を選択し、Xcodeプロジェクトのアプリターゲットの **Frameworks and Libraries** セクションに追加します。
1. [これらの指示](/ja/platforms/ios-swift/install/#swift-package-manager)に従って、`tealium-swift` ライブラリから他のモジュールを追加します。

### CocoaPods

CocoaPodsでCrashReporterモジュールをインストールするには：

1. Podfileに次のpodを追加します：
      ```perl
      pod &#39;TealiumCrashModule&#39;
      ```
      既に次の行がPodfileに含まれています：

      ```perl
      pod &#39;tealium-swift&#39;
      ```

2. 次のコマンドを実行します：
      ```perl
      pod install
      ```

### Carthage

CarthageでCrashReporterモジュールをインストールするには：

1. Cartfileに次の内容を追加します：

      ```bash
      github &#34;tealium/tealium-swift-crash-reporter&#34;
      ```

2. XcodeでアプリターゲットのGeneral構成ページに移動します。

3. **Embedded Binaries** セクションに次のフレームワークを追加します：
      ```perl
      TealiumCrashModule.framework
      CrashReporter.framework
      ```

[iOSのCarthageインストールについてもっと学ぶ](/ja/platforms/ios-swift/install/#carthage)。

## 構成

CrashReporterモジュールをインスタンス化するには、SDKを初期化する際に `TealiumConfig` オブジェクトで指定する必要があります：

```swift
import TealiumCore
import TealiumCrashModule

let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)

// 追加したいCollectorsを追加します
config.collectors = [Collectors.AppData, Collectors.Crash] // CrashReporterモジュールをインスタンス化します
config.sendCrashDataOnCrashDetected = true // オプション、trueの場合クラッシュが検出されたときに追加のクラッシュイベントを送信し、そのイベントにのみクラッシュデータを添付します
tealium = Tealium(config: config) { _ in }                               
```

[Collectors](/ja/platforms/ios-swift/modules/#collectors)のドキュメントを確認して、必要なコレクターを正しく指定する方法を理解してください。

## データレイヤー

モジュールが有効な間、各トラッキングコールで送信される変数は以下の通りです：

| 変数  | 説明 | 例 |
| :-- | :-- | :-- |
| `crash_uuid` | この特定のクラッシュのためのユニークな識別子 | `&#34;CC2DA0E9-E544-429A-AC5E-A268FC62F02A&#34;` |
| `device_memory_usage*`     | クラッシュ時のデバイス上のアプリの現在のメモリ使用量| `&#34;143.57MB&#34; ` |
| `app_memory_usage`          | クラッシュ時のデバイス上のアプリの現在のメモリ使用量| `&#34;143.57MB&#34;`  |
| `device_memory_available*` | クラッシュ時のデバイス上の空きメモリ                         | `&#34;1068.88MB&#34;` |
| `memory_free`               | クラッシュ時のデバイス上の空きメモリ                       | `&#34;1068.88MB&#34;` |
| `device_os_build`           | 現在のOSビルド番号                                              | `&#34;15E217&#34;`    |
| `crash_process_id`          | クラッシュ時のアプリのPID                                      | `&#34;84351&#34;`     |
| `crash_process_path`        | アプリが実行中だったパス                                       | `&#34;/DemoApp.app/DemoApp&#34;` |
| `crash_parent_process`      | アプリを起動した親プロセス                                 | `&#34;launchd_sim&#34;` |
| `crash_parent_process_id`   | 親プロセスのPID                                                   | `&#34;83183&#34;`      |
| `crash_name`                | 利用可能な場合、クラッシュのフレンドリー名                             | `&#34;Crash Name&#34;` |
| `crash_cause`               | クラッシュの原因                                                   | `&#34;Crash Reason&#34;` |
| `crash_signal_code`         | クラッシュを引き起こしたシグナルコード                                        | `&#34;#0&#34;` |
| `crash_signal_name`         | クラッシュを引き起こしたシグナル名                                        | `&#34;SIGABRT&#34;`    |
| `crash_signal_address`      | クラッシュのシグナルアドレス                                          | `&#34;4572945982&#34;` |
| `crash_libraries`           | クラッシュ時にロードされていたライブラリのリスト                    | ```[{&#34;baseAddress&#34;: &#34;0xa3e0000&#34;, &#34;codeType&#34;: { &#34;arch&#34;: 64, &#34;typeEncoding&#34;: &#34;Mach&#34;}, &#34;imageName&#34;: &#34;/Applications/Xcode9.3.app/Contents/ Developer/Platforms/iPhoneOS.platform/ Developer/Library/CoreSimulator/Profiles /Runtimes/iOS.simruntime/Contents/ Resources/RuntimeRoot/usr/lib/dyld_sim&#34;, &#34;imageSize&#34;: 212992, &#34;imageUuid&#34;: &#34;4015e9b70bde&#34;}]``` |
| `crash_threads`              | クラッシュ時のすべてのアクティブスレッド                  |```{&#34;crashed&#34;: 1,&#34;registers&#34;: {&#34;cs&#34;: &#34;0x07&#34;},&#34;stack&#34;: {&#34;instructionPointer&#34;: 4572945982,&#34;symbolInfo&#34;: {&#34;symbolName&#34;: &#34;&#34;,&#34;symbolStartAddr&#34;: 0},&#34;threadId&#34;: &#34;&#34;}}``` |

* これらの変数は以前のリリースとの後方互換性のために重複しています

## クラッシュの起動

`TealiumCrashReporteriOS.framework`がプロジェクトに追加された後、追加の初期化ステップは必要ありません。クラッシュモジュールが有効であり、Tealium SDKが初期化されている限り、アプリでクラッシュが発生すると、クラッシュデータは自動的にトラッキングコールの一部となります。

### テスト

ローカルテストでクラッシュを報告するには、アプリの実行スキームで **Debug executable** のチェックを外して intentionally crashing the app することで、アプリにデバッガがアタッチされていない状態でクラッシュします。アプリの実行プロセスにデバッガがアタッチされている場合、クラッシュレポーターはクラッシュをキャッチしません。

## APIリファレンス

### `invokeCrash()`

CrashReporterモジュールのためのクラッシュを起動します。

```swift
TealiumCrashReporter.invokeCrash(name: name, reason: reason)
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- |  --- |
| `name` | `String` | クラッシュの名前  | `&#34;TEST_CRASH_NAME&#34;` |
| `reason` | `String` | クラッシュの理由 | `&#34;TEST_CRASH_REASON&#34;` |