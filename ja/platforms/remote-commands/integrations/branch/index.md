---
title: リモート コマンド: Branch
description: Android および Swift/iOS における Branch の Tealium リモート コマンド統合です。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/branch/
---
## 要件

- [Dashboard からの Branch Key](https://dashboard.branch.io/settings/link)
- これらのモバイル ライブラリのうちのいずれか:
  - [Tealium for Android (Kotlin)](https://docs.tealium.com/ja/platforms/android-kotlin/) (1.0.0 以降)
  - [Tealium for Android (Java)](https://docs.tealium.com/ja/platforms/android-java/) (5.9.0 以降)
  - [Tealium for iOS (Swift)](https://docs.tealium.com/ja/platforms/ios-swift/) (2.1.0 以降)
- これらのリモート コマンド統合のいずれか:
  - [Branch Remote Command JSON File](https://docs.tealium.com/ja/platforms/remote-commands/integrations/branch/#json-template)
  - [Branch Remote Command タグ](https://community.tealiumiq.com/t5/Client-Side-Tags/Branch-Mobile-Remote-Command-Tag-Setup-Guide/ta-p/36694) (Tealium iQ タグ管理)

## 仕組み

Branch 統合は、これらのアイテムを使用します:

1. Branch ネイティブ SDK
2. Branch メソッドをラップするリモート コマンド モジュール
3. イベント トラッキングをネイティブ Branch コールに翻訳する、JSON 構成ファイルまたは Remote Command タグのいずれか

Branch リモート コマンド モジュールをアプリに追加すると、必要な Branch ライブラリが自動的にインストールされ、ビルドされます。この際、ベンダー固有のコードをアプリに追加する必要はありません。依存関係マネージャのインストールを使用している場合、Branch SDK を個別にインストールする必要はありません。

リモート コマンド オプションは、次の 2 つがあります: A JSON 構成ファイル、または、マッピングを構成するための iQ タグ管理の使用。A JSON 構成ファイルは、リモートでホスティングするか、またはアプリ内でローカルでホスティングするかのいずれでも、ベンダー統合の推奨オプションです。iQ タグ管理を使用する場合は、ベンダー統合用のリモート コマンド タグを追加します。[ベンダー統合](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-integrations)の詳細は、こちらから参照してください。

## インストール

### 依存関係マネージャ

次の依存関係マネージャのいずれかをインストールに使用することをお勧めします。


<blockquote>
Tealium iOS（Objective-C）ライブラリを使用している場合は、手動インストール方法を使用してください。CocoaPodsおよびCarthageオプションは、Tealium iOS（Swift）ライブラリを使用している場合にのみ使用可能です。
</blockquote>





CocoaPods を使用して iOS の Branch リモート コマンドをインストールするには:

1. `tealium-swift` と `pod "Branch"` が Podfile に既に存在する場合は削除します。`tealium-swift` の依存関係は `TealiumBranch` フレームワークに既に含まれています。

2. 次の依存関係をPodfileに追加します。
```ruby
pod "TealiumBranch"
```
`TealiumBranch` ポッドには以下の `TealiumSwift` 依存関係が含まれています。
```bash
'tealium-swift/Core'
'tealium-swift/RemoteCommands'
'tealium-swift/TagManagement'
```

3. モジュール `TealiumSwift` および `TealiumBranch` を、 `TealiumHelper` ファイル、 `Tealium` クラスにアクセスするその他のファイル、または Branch リモート コマンドにインポートします。




Carthage を使用して iOS の Branch リモート コマンドをインストールするには:

1. `tealium-swift`をCartfileから削除します。`tealium-swift` の依存関係は `TealiumBranch` フレームワークに既に含まれています。

2. 次の依存関係をCartfileに追加します。
```bash
github "tealium/tealium-ios-branch-remote-command"
```


<blockquote>
Tealium for Swift SDK（バージョン1.6.5以降）では、`TealiumDelegate`モジュールがインストールに含まれている必要があります。
</blockquote>





Maven を使用して Android の Branch リモート コマンドをインストールするには:

1. [Tealium for Android (Kotlin)](https://docs.tealium.com/ja/platforms/android-kotlin/install/) または [Tealium for Android (Java)](https://docs.tealium.com/ja/platforms/android-java/install/)をインストールします (まだ済んでいない場合)。

2. Tealium Maven の URL を、プロジェクトの最上位にある `build.gradle` ファイルに追加します。

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

3. アプリ プロジェクトの `build.gradle` ファイルに次の依存関係を追加して、Branch SDK と Tealium-Branch の両方のリモート コマンドをインポートします。
```groovy
dependencies {
      implementation 'com.tealium.remotecommands:branch:1.0.0'
}
```





### 手動による手順（iOS）

Brahch リモート コマンドを手動でインストールするには、 [Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/) ライブラリがインストールされている必要があります。iOS プロジェクトの Branch リモート コマンドをインストールするには:

1. [Branch SDK](https://help.branch.io/developers-hub/docs/ios-basic-integration#via-manual-framework) をまだインストールしていない場合はインストールします。

2. Tealium iOS Branch リモート コマンド レポジトリをクローンして、 `Sources` フォルダ内のファイルをプロジェクトにドラッグします。
GitHub リポジトリ: [https://github.com/tealium/tealium-ios-branch-remote-command](https://github.com/tealium/tealium-ios-branch-remote-command)

3. [`remoteAPIEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled) 構成フラッグを `true`に構成します。

### 手動（Android）

Branch リモート コマンドを手動でインストールするには、 [Tealium for Android (Kotlin)](https://docs.tealium.com/ja/platforms/android-kotlin/install/) または [Tealium for Android (Java)](https://docs.tealium.com/ja/platforms/android-java/install/) がインストールされている必要があります。

Android プロジェクトの Branch リモート コマンドをインストールするには:

1. `flatDir`をプロジェクトのルートにある`build.gradle`ファイルに追加します。

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

2. `tealium-branch.aar` を `<PROJECT_ROOT>/<MODULE>/libs`に追加します。

3. Tealiumライブラリの依存関係を`build.gradle`ファイルに追加します。

```groovy
dependencies {
      implementation(name:'tealium-branch', ext:'aar')
}
```

## 初期化

すべての Tealium ライブラリについて、初期化時に Branch モバイル リモート コマンドを登録します。

### Android (Kotlin)

Tealium の Kotlin ライブラリ用の JSON 構成ファイルまたはリモート コマンド タグを用いてリモート コマンドを初期化します。




以下のコードは、ローカル ファイル オプションを使用して、JSON Remote Command 機能とともに用いるために設計されています。
```kotlin
val config = TealiumConfig(application,
      "ACCOUNT",
      "PROFILE",
      Environment.DEV,
      dispatchers = mutableSetOf(Dispatchers.RemoteCommands));

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    val branch = BranchRemoteCommand(application);
    remoteCommands?.add(branch, filename = "branch.json");
}
```




以下のコードは、Remote Command タグ機能とともに用いるために設計されています。
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT",
        "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    val branch = BranchRemoteCommand(application);
    remoteCommands?.add(branch);
}
```




### Android (Java)

Tealium の Android (Java) ライブラリ用のリモート コマンド タグを用いてリモート コマンドを初期化します。




Android 向けの JSON Remote Command ファイル機能は、Kotlin SDK でのみ利用できます。



以下のコードは、Remote Command タグ機能とともに用いるために設計されています。

```java
RemoteCommand branch = new BranchRemoteCommand(application);
teal.addRemoteCommand(branch);
```



### iOS (Swift)

Tealium の iOS (Swift) ライブラリ用の JSON 構成ファイルまたはリモート コマンド タグを用いてリモート コマンドを初期化します。




以下のコードは、ローカル ファイル オプションを使用して、JSON Remote Commands 機能とともに用いるために設計されています。
```swift
var tealium : Tealium?
let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "ENVIRONMENT",
                           dataSource: "DATASOURCE")
config.remoteAPIEnabled = true

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
    let branch = BranchRemoteCommand(type: .local(file: "branch"))
    remoteCommands.add(branch)
}
```




以下のコードは、Remote Command タグ機能とともに用いるために設計されています。
```swift
var tealium : Tealium?
let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "ENVIRONMENT",
                           dataSource: "DATASOURCE")
config.remoteAPIEnabled = true

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
    let branch = BranchRemoteCommand()
    remoteCommands.add(branch)
}

```





## JSON テンプレート

[JSON 構成ファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモート コマンドを構成しようとする場合は、まず、以下のテンプレートを参照します。テンプレートには、標準的なインストールに用いられる共通マッピングが含まれいます。必要に応じて、マッピングを編集します。


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

以下の Branch メソッドは、以下の Tealium コマンドを使用し、Branch リモート コマンド タグのデータ マッピングを使用してトリガーされます。

#### iOS Remote Commands リモート コマンド

| iOS リモートコマンド | Branch メソッド|
| :-- | :--|
| `initialize` | `initSession()` |
| `setuserid` | `setIdentity()` |
| `logout` | `logout()` |
| Any other | `logEvent()` |

#### Android Remote Commands リモート コマンド

| Android リモートコマンド | Branch メソッド|
| :-- | :--|
| `initialize` | `initSession()` |
| `setuserid` | `setIdentity()` |
| `logout` | `logout()` |
| `createdeeplink` | `generateShortUrl()` |
| Any other | `logEvent()` |

### 標準イベント名

以下の標準イベント コマンド名は、 `logEvent` メソッドでサポートされています。コマンドが送信され、イベントに関してすべての必要な変数がマッピングされ、定義されたときは、Branch SDK でコマンドが自動的にトリガーされます。

| リモートコマンド | Branch イベント名 (iOS)| Branch イベント名 (Andriod)
| :-- | :--| :--|
|`achievelevel`| `BranchStandardEvent.achieveLevel`| `BRANCH_STANDARD_EVENT.ACHIEVE_LEVEL` |
|`addpaymentinfo`| `BranchStandardEvent.addPaymentInfo`| `BRANCH_STANDARD_EVENT.ADD_PAYMENT_INFO`|
|`addtocart`| `BranchStandardEvent.addToCart`| `BRANCH_STANDARD_EVENT.ADD_TO_CART` |
|`addtowishlist`| `BranchStandardEvent.addToWishlist`| `BRANCH_STANDARD_EVENT.ADD_TO_WISHLIST` |
|`clickad`| `BranchStandardEvent.clickAd`| `BRANCH_STANDARD_EVENT.CLICK_AD` |
|`completetutorial`| `BranchStandardEvent.completeTutorial`| `BRANCH_STANDARD_EVENT.COMPLETE_TUTORIAL`|
|`completeregistration`| `BranchStandardEvent.completeRegistration`| `BRANCH_STANDARD_EVENT.COMPLETE_REGISTRATION` |
|`completestream`| カスタム イベント `BranchEvent(eventName)`| `BRANCH_STANDARD_EVENT.COMPLETE_STREAM` |
|`initiatepurchase`| `BranchStandardEvent.initiatePurchase`| `BRANCH_STANDARD_EVENT.INITIATE_PURCHASE` |
|`initiatestream`| カスタム イベント `BranchEvent(eventName)`| `BRANCH_STANDARD_EVENT.INITIATE_STREAM` |
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


### SDKのセットアップ

Branch SDK の詳細は、こちらから参照してください:

  - [Branch iOS SDK](https://help.branch.io/developers-hub/docs/ios-basic-integration)
  - [Branch Android SDK](https://help.branch.io/developers-hub/docs/android-basic-integration)

#### 初期化

Branch SDK は起動時に自動的に初期化されます。Branch Key は、JSON 構成ファイル内の、Info.plist または `branch_dev_key` に構成されます。

| リモートコマンド | Branch メソッド|
|---|---|
| `initialize`  | `initSession()` |

Branch リモート コマンド タグに利用できる構成オプションは若干あります。以下のいずれかが起動時に構成された場合は、 `configure()` メソッドの実行中に送信されます。

##### 構成オプション

| Name | TiQ 変数マッピング| 説明| 型|
|---|---|---|---|
| Enable Logging  | `enable_logging` | Branch イベントのコンソールでの記録| `Bool` |
| Branch Key | `branch_dev_key`  | branch アプリケーションのキー。| `String` |


#### アイデンティティ リンクの送信

|  リモートコマンド | Branch メソッド|
|---|---|
| `setIdentity`  | `setIdentity()` |

|  パラメータ | 型|
|---|---|
|  `id` (required) | 文字列|
