---
title: リモート コマンド: Branch
description: Android および Swift/iOS における Branch の Tealium リモート コマンド統合です。
url: https://docs.tealium.com/ja/platforms/remote-commands/integrations/branch/
---
## 要件

- [Dashboard からの Branch Key](https://dashboard.branch.io/settings/link)
- これらのモバイル ライブラリのうちのいずれか:
  - [Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/) (1.0.0 以降)
  - [Tealium for Android (Java)](/ja/platforms/android-java/) (5.9.0 以降)
  - [Tealium for iOS (Swift)](/ja/platforms/ios-swift/) (2.1.0 以降)
- これらのリモート コマンド統合のいずれか:
  - [Branch Remote Command JSON File](/ja/platforms/remote-commands/integrations/branch/#json-template)
  - [Branch Remote Command タグ](https://community.tealiumiq.com/t5/Client-Side-Tags/Branch-Mobile-Remote-Command-Tag-Setup-Guide/ta-p/36694) (Tealium iQ タグ管理)

## 仕組み

Branch 統合は、これらのアイテムを使用します:

1. Branch ネイティブ SDK
2. Branch メソッドをラップするリモート コマンド モジュール
3. イベント トラッキングをネイティブ Branch コールに翻訳する、JSON 構成ファイルまたは Remote Command タグのいずれか

Branch リモート コマンド モジュールをアプリに追加すると、必要な Branch ライブラリが自動的にインストールされ、ビルドされます。この際、ベンダー固有のコードをアプリに追加する必要はありません。依存関係マネージャのインストールを使用している場合、Branch SDK を個別にインストールする必要はありません。

リモート コマンド オプションは、次の 2 つがあります: A JSON 構成ファイル、または、マッピングを構成するための iQ タグ管理の使用。A JSON 構成ファイルは、リモートでホスティングするか、またはアプリ内でローカルでホスティングするかのいずれでも、ベンダー統合の推奨オプションです。iQ タグ管理を使用する場合は、ベンダー統合用のリモート コマンド タグを追加します。[ベンダー統合](/ja/platforms/remote-commands/how-it-works/#vendor-integrations)の詳細は、こちらから参照してください。

## インストール

### 依存関係マネージャ

次の依存関係マネージャのいずれかをインストールに使用することをお勧めします。

Tealium iOS（Objective-C）ライブラリを使用している場合は、手動インストール方法を使用してください。CocoaPodsおよびCarthageオプションは、Tealium iOS（Swift）ライブラリを使用している場合にのみ使用可能です。




CocoaPods を使用して iOS の Branch リモート コマンドをインストールするには:

1. `tealium-swift` と `pod &#34;Branch&#34;` が Podfile に既に存在する場合は削除します。`tealium-swift` の依存関係は `TealiumBranch` フレームワークに既に含まれています。

2. 次の依存関係をPodfileに追加します。
```ruby
pod &#34;TealiumBranch&#34;
```
`TealiumBranch` ポッドには以下の `TealiumSwift` 依存関係が含まれています。
```bash
&#39;tealium-swift/Core&#39;
&#39;tealium-swift/RemoteCommands&#39;
&#39;tealium-swift/TagManagement&#39;
```

3. モジュール `TealiumSwift` および `TealiumBranch` を、 `TealiumHelper` ファイル、 `Tealium` クラスにアクセスするその他のファイル、または Branch リモート コマンドにインポートします。




Carthage を使用して iOS の Branch リモート コマンドをインストールするには:

1. `tealium-swift`をCartfileから削除します。`tealium-swift` の依存関係は `TealiumBranch` フレームワークに既に含まれています。

2. 次の依存関係をCartfileに追加します。
```bash
github &#34;tealium/tealium-ios-branch-remote-command&#34;
```

Tealium for Swift SDK（バージョン1.6.5以降）では、`TealiumDelegate`モジュールがインストールに含まれている必要があります。




Maven を使用して Android の Branch リモート コマンドをインストールするには:

1. [Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/) または [Tealium for Android (Java)](/ja/platforms/android-java/install/)をインストールします (まだ済んでいない場合)。

2. Tealium Maven の URL を、プロジェクトの最上位にある `build.gradle` ファイルに追加します。

    ```groovy
    allprojects {
      repositories {
        mavenCentral()
        maven {
          url &#34;https://maven.tealiumiq.com/android/releases/&#34;
        }
      }
    }
    ```

3. アプリ プロジェクトの `build.gradle` ファイルに次の依存関係を追加して、Branch SDK と Tealium-Branch の両方のリモート コマンドをインポートします。
```groovy
dependencies {
      implementation &#39;com.tealium.remotecommands:branch:1.0.0&#39;
}
```





### 手動による手順（iOS）

Brahch リモート コマンドを手動でインストールするには、 [Tealium for Swift](/ja/platforms/ios-swift/) ライブラリがインストールされている必要があります。iOS プロジェクトの Branch リモート コマンドをインストールするには:

1. [Branch SDK](https://help.branch.io/developers-hub/docs/ios-basic-integration#via-manual-framework) をまだインストールしていない場合はインストールします。

2. Tealium iOS Branch リモート コマンド レポジトリをクローンして、 `Sources` フォルダ内のファイルをプロジェクトにドラッグします。
GitHub リポジトリ: [https://github.com/tealium/tealium-ios-branch-remote-command](https://github.com/tealium/tealium-ios-branch-remote-command)

3. [`remoteAPIEnabled`](/ja/platforms/ios-swift/api/tealium-config/#remoteapienabled) 構成フラッグを `true`に構成します。

### 手動（Android）

Branch リモート コマンドを手動でインストールするには、 [Tealium for Android (Kotlin)](/ja/platforms/android-kotlin/install/) または [Tealium for Android (Java)](/ja/platforms/android-java/install/) がインストールされている必要があります。

Android プロジェクトの Branch リモート コマンドをインストールするには:

1. `flatDir`をプロジェクトのルートにある`build.gradle`ファイルに追加します。

```groovy
allprojects {
      repositories {
         mavenCentral()
         flatDir {
             dirs &#39;libs&#39;
         }
      }
}
```

2. `tealium-branch.aar` を `&lt;PROJECT_ROOT&gt;/&lt;MODULE&gt;/libs`に追加します。

3. Tealiumライブラリの依存関係を`build.gradle`ファイルに追加します。

```groovy
dependencies {
      implementation(name:&#39;tealium-branch&#39;, ext:&#39;aar&#39;)
}
```

## 初期化

すべての Tealium ライブラリについて、初期化時に Branch モバイル リモート コマンドを登録します。

### Android (Kotlin)

Tealium の Kotlin ライブラリ用の JSON 構成ファイルまたはリモート コマンド タグを用いてリモート コマンドを初期化します。




以下のコードは、ローカル ファイル オプションを使用して、JSON Remote Command 機能とともに用いるために設計されています。
```kotlin
val config = TealiumConfig(application,
      &#34;ACCOUNT&#34;,
      &#34;PROFILE&#34;,
      Environment.DEV,
      dispatchers = mutableSetOf(Dispatchers.RemoteCommands));

var tealium = Tealium.create(TEALIUM_MAIN, config) {
    val branch = BranchRemoteCommand(application);
    remoteCommands?.add(branch, filename = &#34;branch.json&#34;);
}
```




以下のコードは、Remote Command タグ機能とともに用いるために設計されています。
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;,
        &#34;PROFILE&#34;,
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
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;)
config.remoteAPIEnabled = true

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
    let branch = BranchRemoteCommand(type: .local(file: &#34;branch&#34;))
    remoteCommands.add(branch)
}
```




以下のコードは、Remote Command タグ機能とともに用いるために設計されています。
```swift
var tealium : Tealium?
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                           profile: &#34;PROFILE&#34;,
                           environment: &#34;ENVIRONMENT&#34;,
                           dataSource: &#34;DATASOURCE&#34;)
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

[JSON 構成ファイル](/ja/platforms/remote-commands/how-it-works/#json-configuration-file)を使用してリモート コマンドを構成しようとする場合は、まず、以下のテンプレートを参照します。テンプレートには、標準的なインストールに用いられる共通マッピングが含まれいます。必要に応じて、マッピングを編集します。


```json
{
  &#34;config&#34;: {
    &#34;settings&#34;: {
      &#34;enable_logging&#34;: true,
      &#34;branch_dev_key&#34;: &#34;branch_key&#34;,
      &#34;collect_device_id&#34;: true
    }
  },
  &#34;mappings&#34;: {
    &#34;tealium_event&#34;: &#34;event.description&#34;,
    &#34;description&#34;: &#34;buo.description&#34;,
    &#34;item_id&#34;: &#34;buo.canonical_identifier&#34;,
    &#34;title&#34;: &#34;buo.title&#34;,
    &#34;feature&#34;: &#34;link.feature&#34;,
    &#34;channel&#34;: &#34;link.channel&#34;,
    &#34;campaign&#34;: &#34;link.campaign&#34;,
    &#34;latitude&#34;: &#34;metadata.latitude&#34;,
    &#34;longitude&#34;: &#34;metadata.longitude&#34;,
    &#34;currency_code&#34;: &#34;metadata.currency_type&#34;,
    &#34;customer_id&#34;: &#34;event.user_id&#34;,
    &#34;coupon&#34;: &#34;metadata.coupon&#34;,
    &#34;product_brand&#34;: &#34;metadata.product_brand&#34;,
    &#34;product_category&#34;: &#34;metadata.product_category&#34;,
    &#34;product_id&#34;: &#34;metadata.sku&#34;,
    &#34;product_name&#34;: &#34;metadata.product_name&#34;,
    &#34;product_variant&#34;: &#34;metadata.product_variant&#34;,
    &#34;product_unit_price&#34;: &#34;metadata.price&#34;,
    &#34;product_quantity&#34;: &#34;event.quantity&#34;,
    &#34;currency_type&#34;: &#34;event.currency&#34;,
    &#34;order_tax&#34;: &#34;event.tax&#34;
  },
  &#34;commands&#34;: {
    &#34;launch&#34;: &#34;initialize&#34;,
    &#34;user_login&#34;: &#34;login,setuserid&#34;,
    &#34;user_register&#34;: &#34;completeregistration&#34;,
    &#34;show_offers&#34;: &#34;clickad&#34;,
    &#34;cart_add&#34;: &#34;addtocart&#34;,
    &#34;wishlist_add&#34;: &#34;addtowishlist&#34;,
    &#34;payment&#34;: &#34;addpaymentinfo&#34;,
    &#34;level_up&#34;: &#34;achievelevel&#34;,
    &#34;email_signup&#34;: &#34;subscribe&#34;,
    &#34;product&#34;: &#34;viewitem&#34;,
    &#34;share&#34;: &#34;share&#34;,
    &#34;rate&#34;: &#34;rate&#34;,
    &#34;search&#34;: &#34;search&#34;,
    &#34;invite&#34;: &#34;invite&#34;,
    &#34;order&#34;: &#34;initiatepurchase&#34;,
    &#34;record_score&#34;: &#34;record_score&#34;,
    &#34;teal_custom_event&#34;: &#34;teal_custom_event&#34;
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
