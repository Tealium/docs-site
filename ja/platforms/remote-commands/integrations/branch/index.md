---
title: リモートコマンド：Branch
description: AndroidおよびSwift/iOS向けのTealiumリモートコマンドによるBranch連携。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/branch/
---
## 要件

* [ダッシュボードから取得したBranchキー](https://dashboard.branch.io/settings/link)
* 次のいずれかのモバイルライブラリ：
  * [Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/)（1.0.0以降）
  * [Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/)（5.9.0以降）
  * [Tealium for iOS（Swift）](https://docs.tealium.com/ja/platforms/ios-swift/)（2.1.0以降）
* 次のいずれかのリモートコマンド連携：
  * [BranchリモートコマンドJSONファイル](https://docs.tealium.com/ja/platforms/remote-commands/integrations/branch/#json-template)
  * タグ管理の[Branchリモートコマンドタグ](https://docs.tealium.com/branch-mobile-remote-command-tag/)

## 仕組み

Branch連携では、次の3つの要素を使用します。

1. BranchネイティブSDK
2. Branchのメソッドをラップするリモートコマンドモジュール
3. イベントトラッキングをBranchのネイティブ呼び出しに変換する、JSON構成ファイルまたはリモートコマンドタグ

Branchリモートコマンドモジュールをアプリに追加すると、必要なBranchライブラリが自動的にインストールおよびビルドされるため、ベンダー固有のコードをアプリに追加する必要はありません。依存関係マネージャーを使用してインストールする場合、Branch SDKを別途インストールする必要はありません。

リモートコマンドには、JSON構成ファイルを使用する方法と、タグ管理を使用してマッピングを構成する方法の2つがあります。ベンダー連携では、リモートまたはアプリ内のローカルにホストしたJSON構成ファイルの使用を推奨します。タグ管理を使用する場合は、ベンダー連携用のリモートコマンドタグを追加します。[ベンダー連携](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)の詳細をご覧ください。

## インストール

### 依存関係マネージャー




1. Xcodeプロジェクトで、**File > Add Packages... > Add Package Dependency**を選択します。
2. リポジトリURLとして`https://github.com/tealium/tealium-ios-branch-remote-command`を入力します。
3. バージョンルールを構成します。通常は`Up to next major`を推奨します。現在の`TealiumBranch`バージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
4. インストールする`TealiumBranch`モジュールを選択し、そのモジュールをインストールするアプリターゲットを選択します。

プロジェクトに複数のアプリターゲットがあり、ほかのアプリターゲットでも`TealiumBranch`モジュールが必要な場合は、**Frameworks, Libraries, and Embedded Content**セクションで手動で追加する必要があります。

追加のアプリターゲットに`TealiumBranch`をインストールするには、次の手順を実行します。

1. **Project Navigator**でXcodeプロジェクトを選択します。
2. Xcodeプロジェクトの**TARGETS**セクションでアプリターゲットを選択します。
3. **General > Frameworks, Libraries & Embedded Content**に移動し、`TealiumBranch`モジュールを選択してアプリターゲットに追加します。

Tealium Swiftライブラリから追加のモジュールをインストールするには、[Swift Package Manager](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)の手順に従ってください。




1. Podfileに`tealium-swift`と`pod "Branch"`がすでに存在する場合は、それらを削除します。`tealium-swift`への依存関係は、すでに`TealiumBranch`フレームワークに含まれています。

2. 次の依存関係をPodfileに追加します。
      ```ruby
      pod "TealiumBranch"
      ```
      `TealiumBranch` Podには、次の`TealiumSwift`依存関係が含まれています。  
      ```bash
      'tealium-swift/Core'
      'tealium-swift/RemoteCommands'
      'tealium-swift/TagManagement'
      ```

3. `TealiumHelper`ファイル、および`Tealium`クラスまたはBranchリモートコマンドにアクセスするその他のファイルで、`TealiumSwift`モジュールと`TealiumBranch`モジュールをインポートします。




1. Cartfileから`tealium-swift`を削除します。`tealium-swift`への依存関係は、すでに`TealiumBranch`フレームワークに含まれています。

2. 次の依存関係をCartfileに追加します。  
      ```bash
      github "tealium/tealium-ios-branch-remote-command"
      ```


<blockquote>
Tealium for Swift SDK（バージョン1.6.5以降）では、インストールに`TealiumDelegate`モジュールを含める必要があります。
</blockquote>





1. まだインストールしていない場合は、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールします。

2. プロジェクトの最上位`build.gradle`ファイルにTealium Maven URLを追加します。

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

3. アプリプロジェクトの`build.gradle`ファイルに次の依存関係を追加して、Branch SDKとTealium-Branchリモートコマンドの両方をインポートします。  
      ```groovy
      dependencies {
            implementation 'com.tealium.remotecommands:branch:1.0.0'
      }
      ```





### 手動インストール




Branchリモートコマンドを手動でインストールするには、[Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/)ライブラリがインストールされている必要があります。iOSプロジェクトにBranchリモートコマンドをインストールするには、次の手順を実行します。

1. まだインストールしていない場合は、[Branch SDK](https://help.branch.io/developers-hub/docs/ios-basic-integration#via-manual-framework)をインストールします。

2. Tealium iOS Branchリモートコマンドのリポジトリをクローンし、`Sources`フォルダー内のファイルをプロジェクトにドラッグします。  
GitHubリポジトリ：[https://github.com/tealium/tealium-ios-branch-remote-command](https://github.com/tealium/tealium-ios-branch-remote-command)

3. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled)構成フラグを`true`に構成します。




Branchリモートコマンドを手動でインストールするには、[Tealium for Android（Kotlin）](https://docs.tealium.com/ja/platforms/android-kotlin/install/)または[Tealium for Android（Java）](https://docs.tealium.com/ja/platforms/android-java/install/)がインストールされている必要があります。

AndroidプロジェクトにBranchリモートコマンドをインストールするには、次の手順を実行します。

1. プロジェクトルートの`build.gradle`ファイルに`flatDir`を追加します。

      ```groovy
      allprojects {
            repositories {
              mavenCentral()
              flatDir {
                  dirs 'libs'
              }
            }
      }
      ```

2. `tealium-branch.aar`を`<PROJECT_ROOT>/<MODULE>/libs`に追加します。

3. `build.gradle`ファイルにTealiumライブラリの依存関係を追加します。

      ```groovy
      dependencies {
            implementation(name:'tealium-branch', ext:'aar')
      }
      ```



## 初期化

すべての Tealium ライブラリで、初期化時に Branch モバイルリモートコマンドを登録します。




JSON 構成ファイルまたは Remote Command タグを使用して、Tealium の iOS（Swift）ライブラリ用リモートコマンドを初期化します。
```swift
var tealium : Tealium?
let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "ENVIRONMENT",
                           dataSource: "DATASOURCE")
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true // Required to use Remote Commands

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }

    // Webview Tag
    let branch = BranchRemoteCommand() 

    // Local JSON
    //let branch = BranchRemoteCommand(type: .local(file: "branch")) 

    // Remote JSON
    //let branch = BranchRemoteCommand(type: .remote(url: "https://some.domain.com/branch.json")) 

    remoteCommands.add(branch)
}
```




JSON 構成ファイルまたは Remote Command タグを使用して、Tealium の Kotlin ライブラリ用リモートコマンドを初期化します。
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands, Dispatchers.TagManagement));
val branch = BranchRemoteCommand(application);

var tealium = Tealium.create(TEALIUM_MAIN, config) {

    // Webview Tag
    remoteCommands?.add(branch); 

    // Local JSON
    //remoteCommands?.add(branch, filename = "branch.json"); 

    // Remote JSON
    //remoteCommands?.add(branch, remoteUrl = "https://some.domain.com/branch.json"); 
}
```




Remote Command タグを使用して、Tealium の Android（Java）ライブラリ用リモートコマンドを初期化します。

```java
RemoteCommand branch = new BranchRemoteCommand(application);
teal.addRemoteCommand(branch);
```



## JSON テンプレート

[JSON 構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモートコマンドを構成する場合は、次のテンプレートを使用して開始してください。このテンプレートには、標準インストールで使用される一般的なマッピングが含まれています。必要に応じてマッピングを編集してください。

```json
{
  "config": {
    "settings": {
      "enable_logging": true,
      "branch_dev_key": "branch_key",
      "collect_device_id": true
    }
  },
  "mappings": {
    "tealium_event": "event.description",
    "description": "buo.description",
    "item_id": "buo.canonical_identifier",
    "title": "buo.title",
    "feature": "link.feature",
    "channel": "link.channel",
    "campaign": "link.campaign",
    "latitude": "metadata.latitude",
    "longitude": "metadata.longitude",
    "currency_code": "metadata.currency_type",
    "customer_id": "event.user_id",
    "coupon": "metadata.coupon",
    "product_brand": "metadata.product_brand",
    "product_category": "metadata.product_category",
    "product_id": "metadata.sku",
    "product_name": "metadata.product_name",
    "product_variant": "metadata.product_variant",
    "product_unit_price": "metadata.price",
    "product_quantity": "event.quantity",
    "currency_type": "event.currency",
    "order_tax": "event.tax"
  },
  "commands": {
    "launch": "initialize",
    "user_login": "login,setuserid",
    "user_register": "completeregistration",
    "show_offers": "clickad",
    "cart_add": "addtocart",
    "wishlist_add": "addtowishlist",
    "payment": "addpaymentinfo",
    "level_up": "achievelevel",
    "email_signup": "subscribe",
    "product": "viewitem",
    "share": "share",
    "rate": "rate",
    "search": "search",
    "invite": "invite",
    "order": "initiatepurchase",
    "record_score": "record_score",
    "teal_custom_event": "teal_custom_event"
  }
}
```

## サポートされているメソッド

各 Branch メソッドにコマンドをマッピングします。Branch メソッドをトリガーするには、対応するコマンドを指定された形式で渡します。

#### iOS リモートコマンド

| iOS リモートコマンド | Branch メソッド |
| :-- | :-- |
| `initialize` | `initSession()` |
| `setuserid` | `setIdentity()` |
| `logout` | `logout()` |
| その他 | `logEvent()` |

#### Android リモートコマンド

| Android リモートコマンド | Branch メソッド |
| :-- | :-- |
| `initialize` | `initSession()` |
| `setuserid` | `setIdentity()` |
| `logout` | `logout()` |
| `createdeeplink` | `generateShortUrl()` |
| その他 | `logEvent()` |

### 標準イベント名

`logEvent` メソッドでは、次の標準イベントコマンド名がサポートされています。コマンドが送信され、そのイベントに必要なすべての変数がマッピングおよび定義されている場合、Branch SDK でコマンドが自動的にトリガーされます。

| リモートコマンド | Branch イベント名（iOS）| Branch イベント名（Android）|
| :-- | :-- | :-- |
|`achievelevel`| `BranchStandardEvent.achieveLevel`| `BRANCH_STANDARD_EVENT.ACHIEVE_LEVEL` |
|`addpaymentinfo`| `BranchStandardEvent.addPaymentInfo`| `BRANCH_STANDARD_EVENT.ADD_PAYMENT_INFO`|
|`addtocart`| `BranchStandardEvent.addToCart`| `BRANCH_STANDARD_EVENT.ADD_TO_CART` |
|`addtowishlist`| `BranchStandardEvent.addToWishlist`| `BRANCH_STANDARD_EVENT.ADD_TO_WISHLIST` |
|`clickad`| `BranchStandardEvent.clickAd`| `BRANCH_STANDARD_EVENT.CLICK_AD` |
|`completetutorial`| `BranchStandardEvent.completeTutorial`| `BRANCH_STANDARD_EVENT.COMPLETE_TUTORIAL`|
|`completeregistration`| `BranchStandardEvent.completeRegistration`| `BRANCH_STANDARD_EVENT.COMPLETE_REGISTRATION` |
|`completestream`| カスタムイベント `BranchEvent(eventName)`| `BRANCH_STANDARD_EVENT.COMPLETE_STREAM` |
|`initiatepurchase`| `BranchStandardEvent.initiatePurchase`| `BRANCH_STANDARD_EVENT.INITIATE_PURCHASE` |
|`initiatestream`| カスタムイベント `BranchEvent(eventName)`| `BRANCH_STANDARD_EVENT.INITIATE_STREAM` |
|`invite`| `BranchStandardEvent.invite`| `BRANCH_STANDARD_EVENT.INVITE` |
|`login`| `BranchStandardEvent.login`| `BRANCH_STANDARD_EVENT.LOGIN` |
|`purchase`| `BranchStandardEvent.purchase`| `BRANCH_STANDARD_EVENT.PURCHASE` |
|`rate`| `BranchStandardEvent.rate`| `BRANCH_STANDARD_EVENT.RATE` |
|`reserve`| `BranchStandardEvent.reserve`| `BRANCH_STANDARD_EVENT.RESERVE` |
|`search`| `BranchStandardEvent.search`| `BRANCH_STANDARD_EVENT.SEARCH` |
|`share`| `BranchStandardEvent.share`| `BRANCH_STANDARD_EVENT.SHARE` |
|`spendcredits`| `BranchStandardEvent.spendCredits`| `BRANCH_STANDARD_EVENT.SPEND_CREDITS` |
|`starttrial`| `BranchStandardEvent.startTrial`| `BRANCH_STANDARD_EVENT.START_TRIAL` |
|`subscribe`| `BranchStandardEvent.subscribe`| `BRANCH_STANDARD_EVENT.SUBSCRIBE` |
|`unlockachievement`| `BranchStandardEvent.unlockAchievement`| `BRANCH_STANDARD_EVENT.UNLOCK_ACHIEVEMENT` |
|`viewad`| `BranchStandardEvent.viewAd`| `BRANCH_STANDARD_EVENT.VIEW_AD` |
|`viewcart`| `BranchStandardEvent.viewCart`| `BRANCH_STANDARD_EVENT.VIEW_CART` |
|`viewitem`| `BranchStandardEvent.viewItem`| `BRANCH_STANDARD_EVENT.VIEW_ITEM` |
|`viewitems`| `BranchStandardEvent.viewItems`| `BRANCH_STANDARD_EVENT.VIEW_ITEMS` |
|`custom`| `BranchEvent(eventString)` | `BranchEvent(eventString)` |

### SDK のセットアップ

Branch SDK のセットアップについて詳しくは、次を参照してください。

  - [Branch iOS SDK](https://help.branch.io/developers-hub/docs/ios-basic-integration)
  - [Branch Android SDK](https://help.branch.io/developers-hub/docs/android-basic-integration)

#### 初期化

Branch SDK は起動時に自動的に初期化されます。Branch Key は Info.plist、または JSON 構成ファイル内の `branch_dev_key` に構成します。

| リモートコマンド | Branch メソッド |
|---|---|
| `initialize`  | `initSession()` |

Branch Remote Command タグでは、いくつかの構成オプションを使用できます。起動時に以下のいずれかが構成されている場合、その構成は `configure()` メソッドの実行時に送信されます。

##### 構成オプション

| 名前 | TiQ 変数マッピング | 説明 | 型 |
|---|---|---|---|
| ロギングを有効化 | `enable_logging` | Branch イベントをコンソールに記録します | `Bool` |
| Branch Key | `branch_dev_key` | Branch アプリケーションのキーです。 | `String` |
#### IDリンクの送信

| リモートコマンド | Branchメソッド |
|---|---|
| `setIdentity` | `setIdentity()` |

| パラメータ | 型 |
|---|---|
| `id`（必須） | 文字列 |