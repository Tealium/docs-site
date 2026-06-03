---
title: Objective-Cの使用方法
description: Objective-CとSwiftの間でブリッジングヘッダーを作成する方法について学びます。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/with-objective-c/
---これはiOS（Swift）用Tealiumの以前のバージョン（1.x）です。最新バージョンは[iOS（Swift）用Tealium 2.x](/ja/platforms/ios-swift/)を参照してください。

私たちはネイティブのSwiftライブラリの使用を推奨していますが、Objective-Cライブラリを使用する必要がある場合、このドキュメントが役立ちます。

## SwiftからObjective-Cを呼び出す
プロジェクトにブリッジングヘッダーを追加し、適切なヘッダーをインポートすることで、SwiftコードからObjective-Cライブラリを呼び出します。

### ブリッジングヘッダーの作成
ブリッジングヘッダーを作成するには：

1. Swiftプロジェクトで新しいファイルを作成します。ファイルタイプを選択するように求められたら、Objective-Cファイルを選択します。
2. このファイルに一時的な名前を付けます。例えば「placeholder.m」とします。後でこのファイルを削除するためです。
3. 「Finish」をクリックすると、XCodeがブリッジングヘッダーの作成を促します（すでにプロジェクトにブリッジングヘッダーがある場合は表示されないかもしれません）。続行するには「Create Bridging Header」を押します。Xcodeが自動的に新しいヘッダーファイルを作成します。
4. プロジェクトから`placeholder.m`ファイルを削除し、`&lt;ProjectName&gt;-Bridging-Header.h`という新しいファイルが作成されたことに注意してください。
5. 新しいブリッジングヘッダーに次のインポート文を追加します：
      ```objc
      @import TealiumIOS;
      ```

      次に、SwiftからObjective-Cコードを呼び出すには：

      ```objc
      class TealiumHelper {
          func somefunc () {
              let tealConfig = TEALConfiguration.init(account: &#34;ACCOUNT&#34;, profile: &#34;PROFILE&#34;, environment: &#34;ENVIRONMENT&#34;)
              let teal = Tealium.newInstance(forKey: &#34;KEY&#34;, configuration: tealConfig)
              teal.trackView(withTitle: &#34;SCREEN_NAME&#34;, dataSources: [&#34;DATA&#34;:&#34;VALUE&#34;])
          }
      }
      ```
## Objective-CからSwiftを呼び出す

Swiftライブラリは、コードに必要なアノテーションが欠けているため、Objective-Cから直接呼び出すことはできません。また、多くの場合、モジュールはNSObjectから継承されず、ネイティブのSwiftデータタイプを使用します。
しかし、中間ヘルパークラスを使用することで、Objective-CからSwiftライブラリを呼び出すことが可能です。

### ヘルパークラス

1. Objective-Cプロジェクトで新しいSwiftファイルを作成します。ブリッジングヘッダーがまだない場合は、このプロンプトを受け入れます。新しいSwiftファイルに「TealiumHelper.swift」と名前を付けます。
2. 新しいSwiftヘッダー（`&lt;ProjectName&gt;-Swift.h`）を、新しいヘルパーを呼び出す必要があるファイルにインポートします。
      ```objc
      #import &#34;ProjectName-Swift.h&#34;
      ```

ヘルパーファイルのメソッドは、Objective-Cコードで使用することができます。ヘルパーをシングルトンにすることをお勧めします。

```objc
#import &#34;TestSwiftBridge-Swift.h&#34;

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	// ヘルパーシングルトンをインスタンス化
    TealiumHelper * help = [TealiumHelper sharedInstance];
    // Tealiumライブラリを初期化するstartメソッドを呼び出す
    [help start];
    // Objective-Cから新しいイベントトラッキングコールをトリガーする
    [help track:@&#34;this is from objective-c!&#34; data:@{@&#34;mydata&#34;:@&#34;hello from obj-c&#34;}];
    return YES;
}
```

### リンク

- [TealiumHelperファイル（Objective-C互換）](https://raw.githubusercontent.com/Tealium/tealium-swift/master/samples/TealiumHelper.swift)