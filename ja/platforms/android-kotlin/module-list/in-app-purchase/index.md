---
title: アプリ内購入モジュール
description: アプリ内購入モジュールは、アプリに自動的にアプリ内購入の追跡を追加します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/in-app-purchase/
--- 

## アプリ内購入とは何ですか？

アプリ内購入とは、アプリ内で購入する追加のコンテンツ、サービス、またはサブスクリプションのことを指します。アプリ内購入の例には以下のようなものがあります：

* 広告の削除のためのアップグレード
* ゲームクレジット
* バーチャル通貨
* 追加のゲームレベル
* さらなる機能の解放

アプリ内購入とはみなされない購入の例には以下のようなものがあります：

* 電子商取引アプリでの衣服やその他のアイテムの購入。
* Google Payを使用して購入を完了する。

## インストール

Maven（推奨）または手動でアプリ内購入モジュールをインストールします。

### Maven

Mavenを使用してモジュールをインストールするには：

1. プロジェクトのトップレベルの `build.gradle` ファイルに、次のMavenリポジトリを追加します：
      ```groovy
          allprojects {
            repositories {
              mavenCentral()
              maven {
                url "https://maven.tealiumiq.com/android/releases/"
              }
            }
          }
      ```
2. プロジェクトモジュールの `build.gradle` ファイルに、次のMaven依存関係を追加します：
      ```groovy
      dependencies {
            implementation 'com.tealium:kotlin-core:1.6.0'
            implementation 'com.tealium:kotlin-inapp-purchase:1.0.2'
      }
      ```

最新バージョンのkotlin-coreを使用していることを確認してください。

### 手動

アプリ内購入モジュールを手動でインストールするには：

1. Tealiumの[アプリ内購入](https://github.com/Tealium/tealium-kotlin/tree/main/inapppurchase)モジュールをダウンロードします。

2. ファイル `tealium-kotlin.inapppurchase-1.0.2.aar` をプロジェクトの `<PROJECT_ROOT>/<MODULE>/libs` ディレクトリにコピーします。

3. プロジェクトモジュールの `build.gradle` ファイルにTealiumライブラリの依存関係を追加します：
      ```groovy
      dependencies {
            implementation(name:'tealium-kotlin.inapppurchase-1.0.2', ext:'aar')
      }
      ```

## 初期化

以下の例のように、アプリ内購入モジュールを初期化します：

```kotlin
val config = TealiumConfig(application,
              "ACCOUNT",
              "PROFILE",
              ENVIRONMENT,
              modules = mutableSetOf(Modules.InAppPurchase),
              dispatchers = mutableSetOf(
                Dispatchers.Collect,
                Dispatchers.RemoteCommands)
)
```

## データレイヤー

アプリ内購入モジュールは、イベントで以下の属性を送信します：

| 変数                    | 説明                                                         | 例 |
|:----------------------------|:--------------------------------------------------------------------|:--|
| `purchase_order_id`         | 購入の注文ID。                                       | "1234567890" |
| `purchase_timestamp`        | ISO 8601形式の購入のタイムスタンプ。                   | "2022-01-17T14:42:28Z" |
| `purchase_quantity`         | 購入したアイテムの総数。                                | "2" |
| `purchase_skus`             | 購入した製品IDの配列。                              | ["premium_upgrade", "sub"] |
| `purchase_state`            | 1 = 購入済み, 2 = 保留中, 0 = 未指定 ([Android Developers: Purchase.PurchaseState](https://developer.android.com/reference/com/android/billingclient/api/Purchase.PurchaseState)を参照してこの属性について詳しく学びましょう。) | "1" |
| `purchase_is_auto_renewing` | サブスクリプションが自動更新される場合は `true` を構成します。                  | true |
| `autotracked`               | イベントが自動的に追跡されたことを示すために `true` を構成します。 | true |
| `tealium_event`             | イベントの名前。                                              | "in_app_purchase" |

