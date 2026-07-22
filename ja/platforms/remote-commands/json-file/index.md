---
title: JSONファイル
description: JSONファイルを使用してリモートコマンドを構成します。
url: https://docs.tealium.com/ja/platforms/remote-commands/json-file/
---
## 要件

* [Tealium for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/) (1.0.0+)
* [Tealium for Android-Java](https://docs.tealium.com/ja/platforms/android-java/) (5.9.0+)
* [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/) (2.0.0+)

静的マッピングと複合コマンドキーには、ライブラリのより高いバージョンが必要です。

* [Tealium Remote Commands for Android-Kotlin](https://docs.tealium.com/ja/platforms/android-kotlin/module-list/remote-commands) (1.3.0+)
* [Tealium for iOS-Swift](https://docs.tealium.com/ja/platforms/ios-swift/) (2.9.0+)

## JSONファイル

JSONファイルを使用してベンダー統合を構成します。

このファイルをアプリ内でローカルにロードするか、リモートホストされたURLからロードします。
ファイルをローカルにロードする場合、アプリケーションにバンドルする必要があり、その名前をコード内のリモートコマンドに渡す必要があります。

各ベンダー統合用の[JSONテンプレートファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-templates)が用意されています。各JSONテンプレートファイルには、`config`、`mappings`、`commands`の3つの主要セクションと、オプションの`statics`セクションがあります。


<blockquote>
クロスプラットフォームフレームワークでは、JSONファイルを各プラットフォーム固有のディレクトリに配置します。Androidの場合は`<project>/app/src/main/assets`にファイルを配置します。iOSの場合はトップレベルにファイルを配置します。
</blockquote>


### 構成マッピング

`config`セクションは、クライアントID、APIキー、またはログレベルなどのベンダーSDK初期化オプションを構成します。例えば、以下はアプリケーションIDを構成します：
```json
{
    "config": {
        "applicationid": "appid123"
    }
}
```

### データマッピング

`mappings`セクションはデータマッピングを定義します。以下のマッピングは、データレイヤー変数`product_id`をベンダーパラメータ`param_item_id`に割り当てます。

```json
{
    "mappings": {
        "product_id": "param_item_id"
    }
}```

ベンダーパラメータは、ペイロード内の特定のオブジェクトにマッピングをスコープするためにドット表記でプレフィックスを使用する場合があります。プレフィックスはオブジェクトを定義し、`.`の右側の値はオブジェクトのプロパティになります。例えば、以下のマッピングは`product_id`を`event`オブジェクトの`param_item_id`変数に割り当てます。リモートコマンドパーサーは`param_item_id`をプロパティの1つとして`event`オブジェクトを作成します。

```json
{
    "mappings": {
        "product_id": "event.param_item_id"
    }
}
```


<blockquote>
オブジェクトプレフィックスは通常`event.`、`product.`、または`purchase.`ですが、任意のカスタムオブジェクト名を使用することができます。ベンダー統合に使用されるオブジェクトプレフィックスを確認するには、[JSONテンプレートファイル](https://docs.tealium.com/ja/platforms/remote-commands/how-it-works/#vendor-templates)を参照してください。
</blockquote>



### コマンド

`commands`セクションはTealiumのイベント名をベンダーのイベントにマッピングします。基本的な実装では、キーはTealiumのイベント名であり、右の値はベンダーの方法のTealiumラッパーです。次の例では、Tealiumイベント`cart_add`がベンダーメソッド`logevent`にマッピングされています：

```json
{
    "commands": {
        "cart_add": "logevent"
    }
}
```

#### すべてのイベント - すべてのビュー

特定のコマンドにすべてのイベントやすべてのビューをマッピングしたい場合は、コマンドキーとして`all_events`または`all_views`を指定します：

```json
{
    "commands": {
        "all_events": "logevent",
        "all_views": "logevent"
    }
}
```

### 複合キー

Swiftライブラリのバージョン2.9.0およびKotlinリモートコマンドモジュールのバージョン1.3.0から、他のDataLayer変数が特定の値と一致する場合にもコマンドをトリガーすることができます。

これを行うには、データレイヤーキーとデータレイヤー値を`:`で区切って複合キーを作成する必要があります。

例えば：

```json
{
    "commands": {
        "screen_view:cart_view": "logevent"
    }
}
```

この場合、リモートコマンドはデータレイヤーで`screen_view`を探し、見つかった場合、その値が文字列`cart_view`と比較されます。
それらが同一であれば、リモートコマンドは`logevent`コマンドをトリガーします。

互換性を保つため、および使用を容易にするために、データレイヤーキーが指定されていない場合は、`tealium_event`が暗黙のうちに指定されます。したがって、これらの2つのコマンドは完全に同一です：

```json
{
    "commands": {
        "cart_add": "logevent",
        "tealium_event:cart_add": "logevent"
    }
}
```

場合によっては、コマンドをトリガーするために複数の条件を持ちたい場合がありますので、カンマで区切って`dataLayerKey:dataLayerValue`のリストを作成します。

例えば：

```json
{
    "commands": {
        "screen_view:cart_view,cart_is_empty:false": "logevent"
    }
}
```

この場合、`logevent`コマンドは`screen_view==cart_view`と`cart_is_empty==false`の両方が真の場合にのみトリガーされます。

#### 区切り文字の上書き

Swift SDKのバージョン2.9.1から、データレイヤー値にカンマやコロンが含まれている場合に備えて、デフォルトの区切り文字を独自の文字列に上書きすることができます。

区切り文字`:`と`,`をお好みの文字列に上書きするには、JSONの構成部分に`keys_equality_delimiter`と`keys_separation_delimiter`のキーを追加します。

もちろん、区切り文字を上書きした場合は、複合キーでそれらを使用する必要があります。

```json
{
    "config": {
        "keys_equality_delimiter": "==",
        "keys_separation_delimiter": "&&"
        ...
    },
    "commands": {
        "screen_view==cart_view&&cart_is_empty==false": "logevent"
    }
}
```

### 静的マッピング

複合キーを使用するもう一つの機能は静的マッピングです。これにはSwift 2.9.0+とKotlin 1.3.0+が必要です。

静的マッピングを使用すると、リモートコマンドが使用するデータレイヤーに静的値を追加することができます。

他のマッピングやコマンドがそれらの値を使用して他のコマンドをトリガーしたり、パラメータを追加したりすることができます。

例えば：

```json
{
    "statics": {
        "screen_view:cart_view,cart_is_empty:false": {
            "possible_buyer": true,
            "apply_discount_percentage":  20.0
        }
    }
}
```

これにより、複合キーの条件が一致した場合、コマンドのペイロードに`possible_buyer`と`apply_discount_percentage`の2つのキーとそれぞれの値（trueおよび20.0）が追加されます。

### 例

以下はJSON構成の例です：
```json
{
    "config": {
        "analytics_enabled": "true",
        "session_timeout_seconds": "30",
        "log_level": "max",
        "minimum_seconds": "100",
        ...
    },
    "mappings": {
        "event_title": "event_name",
        "product_brand": "event.param_item_brand",
        "product_category": "event.param_item_category",
        "product_id": "event.param_item_id",
        "product_list": "event.param_item_list",
        "product_location_id": "event.param_item_location_id",
        "product_name": "event.param_item_name",
        "product_variant": "event.param_item_variant",
        "purchase_type": "event.purchase_type",
        ...
    },
    "commands": {
        "launch": "config",
        "cart_add": "logevent",
        "screen_view:homepage": "logview"
        ...
    },
    "statics": {
        "screen_view:homepage,tealium_event:cart_add": {
            "purchase_type": "fast"
        },
        "screen_view:product_detail,tealium_event:cart_add": {
            "purchase_type": "slow"
        }
        ...
    }
}
```

### ロードオプション

JSON構成ファイルをロードするには2つのオプションがあります：ローカルファイルとして、またはホストされたURLからです。
#### ローカルファイルコマンド

アプリケーション内にリモートコマンド構成JSONをバンドルし、その名前をRemoteCommand初期化メソッドに渡します。

TealiumSwift 2.13.0およびTealiumKotlin RemoteCommandDispatcher 1.4.0から、ローカルRemoteCommandsについては、拡張子があるかないかにかかわらず名前を受け付けます。

これらのライブラリの以前のバージョンを使用している場合は、iOSでは拡張子なしの名前を、Kotlinでは拡張子付きの名前を渡す必要があります。

この状況は、ターゲットとする具体的なネイティブTealiumライブラリに依存するすべてのクロスプラットフォームライブラリにも当てはまります。





iOS（Swift）アプリでローカル構成ファイルを使用するには：  
```swift
let config = TealiumConfig(account: "ACCOUNT",
        profile: "PROFILE",
        environment: "ENVIRONMENT")
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
  	let facebook = FacebookRemoteCommand(type: .local(file: "facebook")) // または同等に "facebook.json" TealiumSwift 2.13.0+で
	remoteCommands.add(facebook)
}
```




Android（Kotlin）アプリでローカル構成ファイルを使用するには：    
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT", "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val facebook = FacebookRemoteCommand(this);
  remoteCommands?.add(facebook, filename = "facebook.json"); // または同等に "facebook" TealiumKotlin RemoteCommandDispatcher 1.4.0+で
}
```





#### リモートURLコマンド

構成ファイルをURLとしてホストし、[ホストされたデータレイヤー](https://docs.tealium.com/use-case-supplementing-product-data/)を使用してアクセス可能にします。

TealiumSwift 2.13.0およびTealiumKotlin RemoteCommandDispatcher 1.4.0から、URL RemoteCommandsについても、JSON構成がダウンロードできない場合（またはダウンロード中の場合）、またはすでにキャッシュされていない場合に使用されるバックアップローカルリモートコマンドを提供できます。

そのためには、ローカルコマンド用のJSONファイルをバンドルします。バックアップとして、AndroidおよびiOSプラットフォームは、追加するRemote Commandの`commandId`で名付けられた構成ファイルを探します。オプションとして、Androidでファイル名が利用可能な場合は、バンドルと共にファイル名を渡すと、`commandId`の代わりにファイル名が使用されます。




iOS（Swift）アプリでホストされた構成ファイルを使用するには：  
```swift
let config = TealiumConfig(account: "ACCOUNT",
        profile: "PROFILE",
        environment: "ENVIRONMENT")
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
  	let facebook = FacebookRemoteCommand(type: .remote(url: "https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/facebook.json"))
	remoteCommands.add(facebook)
}
```



Android（Kotlin）アプリでホストされた構成ファイルを使用するには：    
```kotlin
val config = TealiumConfig(application,
        "ACCOUNT", "PROFILE",
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val facebook = FacebookRemoteCommand(this);
  remoteCommands?.add(facebook, remoteUrl = "https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/facebook.json");
}
```


