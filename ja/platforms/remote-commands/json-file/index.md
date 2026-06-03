---
title: JSONファイル
description: JSONファイルを使用してリモートコマンドを構成します。
url: https://docs.tealium.com/ja/platforms/remote-commands/json-file/
---
## 要件

* [Tealium for Android-Kotlin](/ja/platforms/android-kotlin/) (1.0.0&#43;)
* [Tealium for Android-Java](/ja/platforms/android-java/) (5.9.0&#43;)
* [Tealium for iOS-Swift](/ja/platforms/ios-swift/) (2.0.0&#43;)

静的マッピングと複合コマンドキーには、ライブラリのより高いバージョンが必要です。

* [Tealium Remote Commands for Android-Kotlin](/ja/platforms/android-kotlin/module-list/remote-commands) (1.3.0&#43;)
* [Tealium for iOS-Swift](/ja/platforms/ios-swift/) (2.9.0&#43;)

## JSONファイル

JSONファイルを使用してベンダー統合を構成します。

このファイルをアプリ内でローカルにロードするか、リモートホストされたURLからロードします。
ファイルをローカルにロードする場合、アプリケーションにバンドルする必要があり、その名前をコード内のリモートコマンドに渡す必要があります。

各ベンダー統合用の[JSONテンプレートファイル](/ja/platforms/remote-commands/how-it-works/#vendor-templates)が用意されています。各JSONテンプレートファイルには、`config`、`mappings`、`commands`の3つの主要セクションと、オプションの`statics`セクションがあります。

クロスプラットフォームフレームワークでは、JSONファイルを各プラットフォーム固有のディレクトリに配置します。Androidの場合は`&lt;project&gt;/app/src/main/assets`にファイルを配置します。iOSの場合はトップレベルにファイルを配置します。

### 構成マッピング

`config`セクションは、クライアントID、APIキー、またはログレベルなどのベンダーSDK初期化オプションを構成します。例えば、以下はアプリケーションIDを構成します：
```json
{
    &#34;config&#34;: {
        &#34;applicationid&#34;: &#34;appid123&#34;
    }
}
```

### データマッピング

`mappings`セクションはデータマッピングを定義します。以下のマッピングは、データレイヤー変数`product_id`をベンダーパラメータ`param_item_id`に割り当てます。

```json
{
    &#34;mappings&#34;: {
        &#34;product_id&#34;: &#34;param_item_id&#34;
    }
}```

ベンダーパラメータは、ペイロード内の特定のオブジェクトにマッピングをスコープするためにドット表記でプレフィックスを使用する場合があります。プレフィックスはオブジェクトを定義し、`.`の右側の値はオブジェクトのプロパティになります。例えば、以下のマッピングは`product_id`を`event`オブジェクトの`param_item_id`変数に割り当てます。リモートコマンドパーサーは`param_item_id`をプロパティの1つとして`event`オブジェクトを作成します。

```json
{
    &#34;mappings&#34;: {
        &#34;product_id&#34;: &#34;event.param_item_id&#34;
    }
}
```

オブジェクトプレフィックスは通常`event.`、`product.`、または`purchase.`ですが、任意のカスタムオブジェクト名を使用することができます。ベンダー統合に使用されるオブジェクトプレフィックスを確認するには、[JSONテンプレートファイル](/ja/platforms/remote-commands/how-it-works/#vendor-templates)を参照してください。


### コマンド

`commands`セクションはTealiumのイベント名をベンダーのイベントにマッピングします。基本的な実装では、キーはTealiumのイベント名であり、右の値はベンダーの方法のTealiumラッパーです。次の例では、Tealiumイベント`cart_add`がベンダーメソッド`logevent`にマッピングされています：

```json
{
    &#34;commands&#34;: {
        &#34;cart_add&#34;: &#34;logevent&#34;
    }
}
```

#### すべてのイベント - すべてのビュー

特定のコマンドにすべてのイベントやすべてのビューをマッピングしたい場合は、コマンドキーとして`all_events`または`all_views`を指定します：

```json
{
    &#34;commands&#34;: {
        &#34;all_events&#34;: &#34;logevent&#34;,
        &#34;all_views&#34;: &#34;logevent&#34;
    }
}
```

### 複合キー

Swiftライブラリのバージョン2.9.0およびKotlinリモートコマンドモジュールのバージョン1.3.0から、他のDataLayer変数が特定の値と一致する場合にもコマンドをトリガーすることができます。

これを行うには、データレイヤーキーとデータレイヤー値を`:`で区切って複合キーを作成する必要があります。

例えば：

```json
{
    &#34;commands&#34;: {
        &#34;screen_view:cart_view&#34;: &#34;logevent&#34;
    }
}
```

この場合、リモートコマンドはデータレイヤーで`screen_view`を探し、見つかった場合、その値が文字列`cart_view`と比較されます。
それらが同一であれば、リモートコマンドは`logevent`コマンドをトリガーします。

互換性を保つため、および使用を容易にするために、データレイヤーキーが指定されていない場合は、`tealium_event`が暗黙のうちに指定されます。したがって、これらの2つのコマンドは完全に同一です：

```json
{
    &#34;commands&#34;: {
        &#34;cart_add&#34;: &#34;logevent&#34;,
        &#34;tealium_event:cart_add&#34;: &#34;logevent&#34;
    }
}
```

場合によっては、コマンドをトリガーするために複数の条件を持ちたい場合がありますので、カンマで区切って`dataLayerKey:dataLayerValue`のリストを作成します。

例えば：

```json
{
    &#34;commands&#34;: {
        &#34;screen_view:cart_view,cart_is_empty:false&#34;: &#34;logevent&#34;
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
    &#34;config&#34;: {
        &#34;keys_equality_delimiter&#34;: &#34;==&#34;,
        &#34;keys_separation_delimiter&#34;: &#34;&amp;&amp;&#34;
        ...
    },
    &#34;commands&#34;: {
        &#34;screen_view==cart_view&amp;&amp;cart_is_empty==false&#34;: &#34;logevent&#34;
    }
}
```

### 静的マッピング

複合キーを使用するもう一つの機能は静的マッピングです。これにはSwift 2.9.0&#43;とKotlin 1.3.0&#43;が必要です。

静的マッピングを使用すると、リモートコマンドが使用するデータレイヤーに静的値を追加することができます。

他のマッピングやコマンドがそれらの値を使用して他のコマンドをトリガーしたり、パラメータを追加したりすることができます。

例えば：

```json
{
    &#34;statics&#34;: {
        &#34;screen_view:cart_view,cart_is_empty:false&#34;: {
            &#34;possible_buyer&#34;: true,
            &#34;apply_discount_percentage&#34;:  20.0
        }
    }
}
```

これにより、複合キーの条件が一致した場合、コマンドのペイロードに`possible_buyer`と`apply_discount_percentage`の2つのキーとそれぞれの値（trueおよび20.0）が追加されます。

### 例

以下はJSON構成の例です：
```json
{
    &#34;config&#34;: {
        &#34;analytics_enabled&#34;: &#34;true&#34;,
        &#34;session_timeout_seconds&#34;: &#34;30&#34;,
        &#34;log_level&#34;: &#34;max&#34;,
        &#34;minimum_seconds&#34;: &#34;100&#34;,
        ...
    },
    &#34;mappings&#34;: {
        &#34;event_title&#34;: &#34;event_name&#34;,
        &#34;product_brand&#34;: &#34;event.param_item_brand&#34;,
        &#34;product_category&#34;: &#34;event.param_item_category&#34;,
        &#34;product_id&#34;: &#34;event.param_item_id&#34;,
        &#34;product_list&#34;: &#34;event.param_item_list&#34;,
        &#34;product_location_id&#34;: &#34;event.param_item_location_id&#34;,
        &#34;product_name&#34;: &#34;event.param_item_name&#34;,
        &#34;product_variant&#34;: &#34;event.param_item_variant&#34;,
        &#34;purchase_type&#34;: &#34;event.purchase_type&#34;,
        ...
    },
    &#34;commands&#34;: {
        &#34;launch&#34;: &#34;config&#34;,
        &#34;cart_add&#34;: &#34;logevent&#34;,
        &#34;screen_view:homepage&#34;: &#34;logview&#34;
        ...
    },
    &#34;statics&#34;: {
        &#34;screen_view:homepage,tealium_event:cart_add&#34;: {
            &#34;purchase_type&#34;: &#34;fast&#34;
        },
        &#34;screen_view:product_detail,tealium_event:cart_add&#34;: {
            &#34;purchase_type&#34;: &#34;slow&#34;
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
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
        profile: &#34;PROFILE&#34;,
        environment: &#34;ENVIRONMENT&#34;)
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
  	let facebook = FacebookRemoteCommand(type: .local(file: &#34;facebook&#34;)) // または同等に &#34;facebook.json&#34; TealiumSwift 2.13.0&#43;で
	remoteCommands.add(facebook)
}
```




Android（Kotlin）アプリでローカル構成ファイルを使用するには：    
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;, &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val facebook = FacebookRemoteCommand(this);
  remoteCommands?.add(facebook, filename = &#34;facebook.json&#34;); // または同等に &#34;facebook&#34; TealiumKotlin RemoteCommandDispatcher 1.4.0&#43;で
}
```





#### リモートURLコマンド

構成ファイルをURLとしてホストし、[ホストされたデータレイヤー]()を使用してアクセス可能にします。

TealiumSwift 2.13.0およびTealiumKotlin RemoteCommandDispatcher 1.4.0から、URL RemoteCommandsについても、JSON構成がダウンロードできない場合（またはダウンロード中の場合）、またはすでにキャッシュされていない場合に使用されるバックアップローカルリモートコマンドを提供できます。

そのためには、ローカルコマンド用のJSONファイルをバンドルします。バックアップとして、AndroidおよびiOSプラットフォームは、追加するRemote Commandの`commandId`で名付けられた構成ファイルを探します。オプションとして、Androidでファイル名が利用可能な場合は、バンドルと共にファイル名を渡すと、`commandId`の代わりにファイル名が使用されます。




iOS（Swift）アプリでホストされた構成ファイルを使用するには：  
```swift
let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
        profile: &#34;PROFILE&#34;,
        environment: &#34;ENVIRONMENT&#34;)
config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands]
config.remoteAPIEnabled = true

tealium = Tealium(config: config) { _ in
    guard let remoteCommands = self.tealium?.remoteCommands else {
        return
    }
  	let facebook = FacebookRemoteCommand(type: .remote(url: &#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/facebook.json&#34;))
	remoteCommands.add(facebook)
}
```



Android（Kotlin）アプリでホストされた構成ファイルを使用するには：    
```kotlin
val config = TealiumConfig(application,
        &#34;ACCOUNT&#34;, &#34;PROFILE&#34;,
        Environment.DEV,
        dispatchers = mutableSetOf(Dispatchers.RemoteCommands));
var tealium = Tealium.create(TEALIUM_MAIN, config) {
  val facebook = FacebookRemoteCommand(this);
  remoteCommands?.add(facebook, remoteUrl = &#34;https://tags.tiqcdn.com/dle/ACCOUNT/PROFILE/facebook.json&#34;);
}
```


