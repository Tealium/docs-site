---
title: インストール
description: C#用Tealiumのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/csharp/install/
---## 要件

* [Tealium Customer Data Hubアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)
* Visual Studioまたは他のC#対応IDE

## サンプルアプリ

Tealiumライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れるために、C#用Tealiumの[サンプルアプリ](https://github.com/Tealium/tealium-c-sharp/tree/master/tealiumcsharp/Sample)を探索してください。

## インストール

C#用のTealiumライブラリをインストールするには：

1. [Tealium C# Library](https://github.com/Tealium/tealium-c-sharp)のコードをダウンロードします。

2. `TealiumCSharp`フォルダをソリューションにインポートします：

      ```csharp
      using TealiumCSharp;
      ```

## 初期化

Tealiumを初期化するには：  

1. 次の例に示すように、[`Config()`](https://docs.tealium.com/ja/platforms/csharp/api/#config)コンストラクタメソッドを使用して`Config`クラスのインスタンスを作成します：

      ```csharp
      Config config = new Config(
                  "ACCOUNT",
                        "PROFILE",
                        "ENVIRONMENT",
                        "VISITOR_ID",
                        new string[] {
                                    AppDataModule.Name,
                                    CollectModule.Name,
                                    LoggerModule.Name
                        },
                        null,
                        null);
      ```

2. 次の例に示すように、`Config`インスタンスを引数として[`Tealium()`](https://docs.tealium.com/ja/platforms/csharp/api/#tealium)コンストラクタメソッドを使用して`Tealium`クラスのインスタンスを作成します：

      ```csharp
      Tealium tealium = new Tealium(config);
      ```

## Xamarinモバイルアプリケーション

Xamarinでモバイルアプリケーションを作成している場合は、[iOS](https://docs.tealium.com/ja/platforms/ios-swift/)と[Android](https://docs.tealium.com/ja/platforms/android-java/) SDKへの事前に組み込まれたバインディングを持つ[Xamarin integration](https://docs.tealium.com/ja/platforms/xamarin/)を利用してください。
