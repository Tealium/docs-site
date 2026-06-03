---
title: Objective-Cとの連携
description: Objective-CとSwiftの間で動作するブリッジヘッダーの作成について学びます。
url: https://docs.tealium.com/ja/platforms/ios-swift/with-objective-c/
---私たちは、Objective-Cのプロジェクトであっても、ネイティブのSwiftライブラリを使用することをお勧めしますが、それでもObjective-Cライブラリを使用する必要がある場合は、このドキュメントが役立ちます。

## SwiftからObjective-Cを呼び出す
プロジェクトにブリッジングヘッダーを追加し、適切なヘッダーをインポートすることで、SwiftコードからObjective-Cライブラリを簡単に呼び出すことができます。

### ブリッジングヘッダー
ブリッジングヘッダーを作成するには：

1. Swiftプロジェクトで新しいファイルを作成します。ファイルタイプを選択するように求められたら、Objective-Cファイルを選択します。
2. このファイルに一時的な名前を付けます。例えば、&#34;placeholder.m&#34;などとします。後でこのファイルを削除するからです。
3. &#34;Finish&#34;をクリックすると、XCodeがブリッジングヘッダーの作成を促します（すでにプロジェクトにブリッジングヘッダーがある場合は促されません）。&#34;Create Bridging Header&#34;を押して続行し、Xcodeが自動的に新しいヘッダーファイルを作成します。
4. `placeholder.m`ファイルをプロジェクトから削除し、新しいファイル`&lt;ProjectName&gt;-Bridging-Header.h`が作成されたことに注意します。
5. 新しいブリッジングヘッダーに以下のインポート文を追加します：  
      ```objc
      @import TealiumIOS;
      ```

      次に、SwiftからObjective-Cのコードを呼び出すには：

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

Swiftライブラリは、コードに必要な注釈が欠けているため、直接Objective-Cから呼び出すことはできません。また、多くの場合、モジュールはNSObjectから継承するのではなく、ネイティブのSwiftデータ型を使用します。
しかし、中間のヘルパークラスを使用することで、Objective-CからSwiftライブラリを呼び出すことが可能です。

### ヘルパークラス

1. Objective-Cプロジェクトで新しいSwiftファイルを作成します。まだブリッジングヘッダーを追加していない場合は、追加するように求められます。このプロンプトを受け入れます。新しいSwiftファイルに&#34;TealiumHelper.swift&#34;という名前を付けます。
2. 新しいヘルパーを呼び出す必要があるファイルに新しいSwiftヘッダー（`&lt;ProjectName&gt;-Swift.h`）をインポートします。  
      ```objc
      #import &#34;ProjectName-Swift.h&#34;
      ```

ヘルパーファイルのメソッドは、Objective-Cコードで使用できるようになります。ヘルパーをシングルトンにすることをお勧めします。

```objc
#import &#34;TestSwiftBridge-Swift.h&#34;

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	// instantiate the helper singleton
    TealiumHelper * help = [TealiumHelper sharedInstance];
    // call the start method, which initializes the Tealium library
    [help start];
    // trigger a new event tracking call from objective-c
    [help track:@&#34;this is from objective-c!&#34; data:@{@&#34;mydata&#34;:@&#34;hello from obj-c&#34;}];
    return YES;
}
```

### サンプルTealiumHelperファイル

```swift
// 
// TealiumHelper.swift
//
//  Copyright © 2021 Tealium, Inc. All rights reserved.
//

import TealiumCollect
import TealiumCore
import TealiumLifecycle
import TealiumVisitorService
#if os(iOS)
import TealiumAttribution
import TealiumLocation
import TealiumRemoteCommands
import TealiumTagManagement
#endif

enum TealiumConfiguration {
    static let account = &#34;tealiummobile&#34;
    static let profile = &#34;demo&#34;
    static let environment = &#34;dev&#34;
    static let dataSourceKey = &#34;abc123&#34;
}

// Change this to false to disable all the Tealium logs
let enableHelperLogs = true

@objc
class TealiumHelper: NSObject {
    
    @objc
    static let shared = TealiumHelper()

    let config = TealiumConfig(account: TealiumConfiguration.account,
                               profile: TealiumConfiguration.profile,
                               environment: TealiumConfiguration.environment,
                               dataSource: TealiumConfiguration.dataSourceKey)

    var tealium: Tealium?

    // MARK: Tealium Initilization
    private override init() {
        super.init()
        // Optional Config Settings
        if enableHelperLogs { config.logLevel = .info }

// Optional - Only required if using Visitor Service
//        config.visitorServiceDelegate = self

// Optional - Only required if using Consent Manager
//        config.consentLoggingEnabled = true
//        config.consentPolicy = .ccpa

// Optional - Only required if using Hosted Data Layer
//        config.hostedDataLayerKeys = [&#34;hdl-test&#34;: &#34;product_id&#34;]
// Optional - Only required if using Timed Events
//        config.timedEventTriggers = [TimedEventTrigger(start: &#34;product_view&#34;, end: &#34;order_complete&#34;),
//                                     TimedEventTrigger(start: &#34;start_game&#34;, end: &#34;buy_coins&#34;)]

        #if os(iOS)
        // Add dispatchers
        config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands, Dispatchers.Collect]
        #else
        config.dispatchers = [Dispatchers.Collect]
        #endif

        // Add collectors
        #if os(iOS) &amp;&amp; targetEnvironment(macCatalyst)
        // Optional - Only required if using Visitor Service
        config.collectors = [Collectors.VisitorService]
        #elseif os(iOS) &amp;&amp; !targetEnvironment(macCatalyst)
        config.collectors = [Collectors.Attribution, Collectors.VisitorService, Collectors.Location]

         // Batching:
         config.batchingEnabled = false // true to enable

        // Location - Geofence Monitoring:
//        config.geofenceUrl = &#34;https://tags.tiqcdn.com/dle/tealiummobile/location/geofences.json&#34;
//        config.useHighAccuracy = true
//        config.updateDistance = 200.0
        
        // SKAdNetwork event handling
        config.searchAdsEnabled = true
        config.skAdAttributionEnabled = true
        config.skAdConversionKeys = [&#34;conversion_event&#34;: &#34;conversion_value&#34;]

        // Remote Commands:
        let remoteCommand = RemoteCommand(commandId: &#34;hello&#34;, description: &#34;world&#34;) { response in
            guard let payload = response.payload else {
                return
            }
            // Do something w/remote command payload
            if enableHelperLogs {
                print(payload)
            }
        }
        config.addRemoteCommand(remoteCommand)
        #endif

        tealium = Tealium(config: config) { _ in
            // Optional post init processing
            self.tealium?.dataLayer.add(data: [&#34;somekey&#34;: &#34;someval&#34;], expiry: .afterCustom((.months, 1)))
            self.tealium?.dataLayer.add(key: &#34;someotherkey&#34;, value: &#34;someotherval&#34;, expiry: .forever)
        }
    }
    
    @objc
    public func start() {
        _ = TealiumHelper.shared
    }
    
    @objc
    func resetConsentPreferences() {
        tealium?.consentManager?.resetUserConsentPreferences()
    }
    
    @objc
    func track(title: String, data: [String: Any]?) {
        let dispatch = TealiumEvent(title, dataLayer: data)
        tealium?.track(dispatch)
    }

    @objc
    func trackView(title: String, data: [String: Any]?) {
        let dispatch = TealiumView(title, dataLayer: data)
        tealium?.track(dispatch)
    }

    @objc
    func joinTrace(_ traceID: String) {
        tealium?.joinTrace(id: traceID)
    }

    @objc
    func leaveTrace() {
        tealium?.leaveTrace()
    }
}
```
