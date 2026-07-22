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
2. このファイルに一時的な名前を付けます。例えば、"placeholder.m"などとします。後でこのファイルを削除するからです。
3. "Finish"をクリックすると、XCodeがブリッジングヘッダーの作成を促します（すでにプロジェクトにブリッジングヘッダーがある場合は促されません）。"Create Bridging Header"を押して続行し、Xcodeが自動的に新しいヘッダーファイルを作成します。
4. `placeholder.m`ファイルをプロジェクトから削除し、新しいファイル`<ProjectName>-Bridging-Header.h`が作成されたことに注意します。
5. 新しいブリッジングヘッダーに以下のインポート文を追加します：  
      ```objc
      @import TealiumIOS;
      ```

      次に、SwiftからObjective-Cのコードを呼び出すには：

      ```objc
      class TealiumHelper {
          func somefunc () {
              let tealConfig = TEALConfiguration.init(account: "ACCOUNT", profile: "PROFILE", environment: "ENVIRONMENT")
              let teal = Tealium.newInstance(forKey: "KEY", configuration: tealConfig)
              teal.trackView(withTitle: "SCREEN_NAME", dataSources: ["DATA":"VALUE"])
          }
      }
      ```
## Objective-CからSwiftを呼び出す

Swiftライブラリは、コードに必要な注釈が欠けているため、直接Objective-Cから呼び出すことはできません。また、多くの場合、モジュールはNSObjectから継承するのではなく、ネイティブのSwiftデータ型を使用します。
しかし、中間のヘルパークラスを使用することで、Objective-CからSwiftライブラリを呼び出すことが可能です。

### ヘルパークラス

1. Objective-Cプロジェクトで新しいSwiftファイルを作成します。まだブリッジングヘッダーを追加していない場合は、追加するように求められます。このプロンプトを受け入れます。新しいSwiftファイルに"TealiumHelper.swift"という名前を付けます。
2. 新しいヘルパーを呼び出す必要があるファイルに新しいSwiftヘッダー（`<ProjectName>-Swift.h`）をインポートします。  
      ```objc
      #import "ProjectName-Swift.h"
      ```

ヘルパーファイルのメソッドは、Objective-Cコードで使用できるようになります。ヘルパーをシングルトンにすることをお勧めします。

```objc
#import "TestSwiftBridge-Swift.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	// instantiate the helper singleton
    TealiumHelper * help = [TealiumHelper sharedInstance];
    // call the start method, which initializes the Tealium library
    [help start];
    // trigger a new event tracking call from objective-c
    [help track:@"this is from objective-c!" data:@{@"mydata":@"hello from obj-c"}];
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
    static let account = "tealiummobile"
    static let profile = "demo"
    static let environment = "dev"
    static let dataSourceKey = "abc123"
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
//        config.hostedDataLayerKeys = ["hdl-test": "product_id"]
// Optional - Only required if using Timed Events
//        config.timedEventTriggers = [TimedEventTrigger(start: "product_view", end: "order_complete"),
//                                     TimedEventTrigger(start: "start_game", end: "buy_coins")]

        #if os(iOS)
        // Add dispatchers
        config.dispatchers = [Dispatchers.TagManagement, Dispatchers.RemoteCommands, Dispatchers.Collect]
        #else
        config.dispatchers = [Dispatchers.Collect]
        #endif

        // Add collectors
        #if os(iOS) && targetEnvironment(macCatalyst)
        // Optional - Only required if using Visitor Service
        config.collectors = [Collectors.VisitorService]
        #elseif os(iOS) && !targetEnvironment(macCatalyst)
        config.collectors = [Collectors.Attribution, Collectors.VisitorService, Collectors.Location]

         // Batching:
         config.batchingEnabled = false // true to enable

        // Location - Geofence Monitoring:
//        config.geofenceUrl = "https://tags.tiqcdn.com/dle/tealiummobile/location/geofences.json"
//        config.useHighAccuracy = true
//        config.updateDistance = 200.0
        
        // SKAdNetwork event handling
        config.searchAdsEnabled = true
        config.skAdAttributionEnabled = true
        config.skAdConversionKeys = ["conversion_event": "conversion_value"]

        // Remote Commands:
        let remoteCommand = RemoteCommand(commandId: "hello", description: "world") { response in
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
            self.tealium?.dataLayer.add(data: ["somekey": "someval"], expiry: .afterCustom((.months, 1)))
            self.tealium?.dataLayer.add(key: "someotherkey", value: "someotherval", expiry: .forever)
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
