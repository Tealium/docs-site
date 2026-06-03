---
title: VolatileData モジュール
description: データ変数を主メモリ（RAM）に保存します。データは保存され、アプリが再起動されるまですべてのディスパッチ/トラッキングコールに追加されます。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/volatile-data/
---
## 使用法

VolatileData モジュールを使用すると、データ変数を主メモリ（RAM）に保存できます。データは保存され、アプリが再起動されるまですべてのディスパッチ/トラッキングコールに追加されます。

このモジュールの使用は必須です。実装しないと、トラッキングコールから重要な変数が欠落します。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* watchOS
* macOS

## インストール

CocoaPods または Carthage を使用して VolatileData モジュールをインストールします。

### CocoaPods

CocoaPods を使用して VolatileData モジュールをインストールするには、以下の pod を Podfile に追加します：  

```ruby
pod &#39;tealium-swift/TealiumVolatileData&#39;
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` pod に依存性があります。iOS の CocoaPods インストールについては[こちら](/ja/platforms/ios-swift-v1/install/#cocoapods)をご覧ください。

### Carthage

Carthage を使用して VolatileData モジュールをインストールするには、以下の手順を実行します：

1. Xcode のアプリターゲットの一般構成ページに移動します。

2. 以下のフレームワークを **Embedded Binaries** セクションに追加します：  
      ```ruby
      TealiumVolatileData.framework
      ```
3. VolatileData API を通じて揮発性データを保存するには、プロジェクトに以下の必要なインポート文を追加します：  
      ```swift
      import TealiumVolatileData
      ```

フレームワークは自動的にインスタンス化されます。`TealiumCore` に依存性があります。追加のインポート文は必要ありません。iOS の Carthage インストールについては[こちら](/ja/platforms/ios-swift-v1/install/#carthage)をご覧ください。

## 含まれる変数
| 変数              | 説明                                             | 例    | サポートされるプラットフォーム       |
|---------------------------|---------------------------------------------------------|------------------|---------------------------|
| `tealium_random`          | ランダムな数値                                           | `&#34;8449989974958830&#34;` | iOS, tvOS, watchOS, macOS |
| `tealium_session_id`      | Tealium セッション ID                                      | `&#34;1511262829677&#34;` | iOS, tvOS, watchOS, macOS |
| `tealium_timestamp_epoch` | 現在の Unix タイムスタンプ（1970 エポック）を秒単位で表示                    | `&#34;1511262829&#34;` | iOS, tvOS, watchOS, macOS |
| `tealium_account`         | 現在の Tealium アカウント（TealiumConfig オブジェクトから）     | `&#34;tealium&#34;`          | iOS, tvOS, watchOS, macOS |
| `tealium_profile`         | 現在の Tealium プロファイル（TealiumConfig オブジェクトから）     | `&#34;mobile&#34;`           | iOS, tvOS, watchOS, macOS |
| `tealium_environment`     | 現在の Tealium 環境（TealiumConfig オブジェクトから） | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`]              | iOS, tvOS, watchOS, macOS |
| `tealium_library_name`    | Tealium ライブラリ名                                    | `&#34;swift&#34;`            | iOS, tvOS, watchOS, macOS |
| `tealium_library_version` | Tealium ライブラリバージョン                                 | `&#34;1.4.0&#34;`            | iOS, tvOS, watchOS, macOS |
| `event_timestamp_iso* `                  | イベントタイムスタンプを ISO 8601（UTC）、UTCで表示                                                   | `&#34;2017-11-20T14:48:00Z&#34;`      | iOS, tvOS, watchOS, macOS |
| `timestamp`                   | イベントタイムスタンプを ISO 8601（UTC）、UTCで表示                                                   | `&#34;2017-11-20T14:48:00Z&#34;`      | iOS, tvOS, watchOS, macOS |
| `event_timestamp_local_iso*`            | イベントタイムスタンプを ISO 8601 のローカルタイムゾーンで表示                                        | `&#34;2017-11-20T06:48:00&#34;`       | iOS, tvOS, watchOS, macOS |
| `timestamp_local`            | イベントタイムスタンプを ISO 8601 のローカルタイムゾーンで表示                                        | `&#34;2017-11-20T06:48:00&#34;`       | iOS, tvOS, watchOS, macOS |
| `event_timestamp_offset_hours*`           | UTC からの現在のオフセットを時間単位で表示                                    | `-8`                        | iOS, tvOS, watchOS, macOS |
| `timestamp_offset`           | UTC からの現在のオフセットを時間単位で表示                                                 | `-8`                        | iOS, tvOS, watchOS, macOS |
| `event_timestamp_unix_millis*`            | 現在の Unix タイムスタンプ（1970 エポック）をミリ秒単位で表示                 | `1511189280337`             | iOS, tvOS, watchOS, macOS |
| `timestamp_unix_milliseconds`             | 現在の Unix タイムスタンプ（1970 エポック）をミリ秒単位で表示                 | `1511189280337`             | iOS, tvOS, watchOS, macOS |
| `event_timestamp_unix*`             | 現在の Unix タイムスタンプ（1970 エポック）を秒単位で表示                            | `1511189280`             | iOS, tvOS, watchOS, macOS |
| `timestamp_unix`             | 現在の Unix タイムスタンプ（1970 エポック）を秒単位で表示                                   | `1511189280`             | iOS, tvOS, watchOS, macOS |

## API リファレンス

iOS（Swift）API の [`TealiumVolatileData`](/ja/platforms/ios-swift-v1/api/tealium-volatile-data/) クラスを参照してください。
