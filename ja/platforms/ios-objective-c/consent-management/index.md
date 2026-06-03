---
title: 同意管理
description: iOS（Objective-C）で同意管理を実装する方法を学びます。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/consent-management/
---
## 使用法

このモジュールの使用をお勧めします。なぜなら、CocoaPodsフレームワークビルドに自動的に含まれ、有効になるからです。

サポートされるプラットフォームには、iOS、macOS、tvOS、およびwatchOSがあります。

同意管理に関する詳細については、を参照してください。

## サンプルアプリ

Tealium Consent Managementを有効にする方法に慣れるために、次のサンプルアプリをダウンロードすることをお勧めします。

*   [Objective-Cサンプルアプリ](https://github.com/Tealium/tealium-ios/tree/master/Samples/ConsentManagerDemo_ObjC)
*   [Swiftサンプルアプリ](https://github.com/Tealium/tealium-ios/tree/master/Samples/ConsentManagerDemo_Swift)


## データレイヤー

同意管理が有効になっている場合、次の変数が各トラッキングコールと共に送信されます。

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `policy` | 同意が収集されたポリシー（デフォルト：`gdpr`）| `gdpr` |
| `consent_status` | ユーザーの現在の同意ステータス | [`&#34;同意済み&#34;`, `&#34;同意していない&#34;`] |
| `consent_categories` | ユーザーが同意している現在のカテゴリー | `@[@&#34;analytics&#34;]` |


## ユースケース

### ユースケース：シンプルなオプトイン

```objc
[_tealium.consentManager setUserConsentStatus:Consented];
```

この例では、ユーザーにシンプルな「オプトイン/オプトアウト」オプションを提供する方法を示しています。ユーザーが同意すると、すべてのトラッキングカテゴリーに自動的にオプトインされます。同意を取り消すと、カテゴリーはアクティブにならず、トラッキングコールは送信されません。

Tealiumヘルパークラスで、アプリのユーザーがトラッキングを同意または拒否したときに、次のメソッドを定義して呼び出します。ユーザーがトラッキングに同意すると、同意マネージャーは自動的にすべてのトラッキングカテゴリーにオプトインします。

![](/images/platforms/ios/consent-simple-optin.gif)

### ユースケース：グループ化されたオプトイン

```objc
[_tealium.consentManager setUserConsentStatus:Consented withUserConsentCategories:@[@&#34;analytics&#34;, @&#34;monitoring&#34;, @&#34;big_data&#34;, @&#34;mobile&#34;, @&#34;crm&#34;]];
```

この例では、カテゴリベースの同意モデルを示しています。トラッキングカテゴリーは、ユーザーが選択するためのフルリストではなく、あなたが定義するより少ない数の上位カテゴリーにグループ化されます。たとえば、Tealiumの同意カテゴリ`&#34;analytics&#34;`、`&#34;monitoring&#34;`、`&#34;big_data&#34;`、`&#34;mobile&#34;`、`&#34;crm&#34;`を`&#34;performance&#34;`という単一のカテゴリーの下にグループ化することを選択することができます。これは、ユーザーにとってフルリストから選択するよりも簡単な場合があります。これをスライダーインターフェースで表現し、最も制限の少ないものから最も制限の多いもの（すべてのカテゴリー）までの範囲とすることもできます。

![](/images/platforms/ios/consent-group-optin.gif)

### ユースケース：カテゴリベースのオプトイン

```objc
[_tealium.consentManager setUserConsentStatus:Consented withUserConsentCategories:@[@&#34;analytics&#34;, @&#34;personalization&#34;]];
```

この例では、カテゴリベースの同意モデルを示しています。ユーザーは、すべてのカテゴリーのフルリストから各カテゴリーを明示的に選択する必要があります。同意マネージャーのデフォルトの状態は「不明」であり、ユーザーが同意を提供するまでヒットがキューに入れられます。ユーザーがいずれかのカテゴリーに同意すると、イベントがキューから取り出され、同意されたカテゴリーデータが各トラッキングコールに追加されます。

![](/images/platforms/ios/consent-category-optin.gif)

## APIリファレンス

### `consentManager`
このコードは、Tealiumの初期化時に同意管理を有効にする方法を示しています。

```objc
// TealiumHelper.h

@import TealiumIOS;
@interface TealiumHelper : NSObject&lt;TealiumDelegate, TEALConsentManagerDelegate&gt;
@property (nonatomic, strong) Tealium *tealium;
@end

// TealiumHelper.m

@implementation TealiumHelper

&#43; (instancetype _Nonnull)sharedInstance {
  static TealiumHelper *tealiumHelper = nil;
  static dispatch_once_t onceToken;
  dispatch_once(&amp;onceToken, ^{
  tealiumHelper = [[self alloc] init];
  });

  return tealiumHelper;
}

- (instancetype)init {
  if (self = [super init]) {
    TEALConfiguration *configuration = [TEALConfiguration configurationWithAccount:@&#34;ACCOUNT&#34; profile:@&#34;PROFILE&#34; environment:@&#34;ENVIRONMENT&#34;];
    [configuration setLogLevel: TEALLogLevelDev];

    // 同意マネージャーを有効にする
    [configuration setEnableConsentManager:YES];

    _tealium = [Tealium newInstanceForKey:@&#34;INSTANCE&#34; configuration:configuration];
    _tealium.delegate = self;

    // オプションの同意マネージャーデリゲートを設定する
    _tealium.consentManagerDelegate = self;
    NSLog(@&#34;%s, %@&#34;, __FUNCTION__, [TEALConsentManager consentStatusString:_tealium.consentManager.userConsentStatus]);
  }

  return self;
}

@end
```

**`enable`**  
同意マネージャーを有効にします。このメソッドは、Tealiumの初期化後に同意マネージャーを後から有効にします。

```objc
[_tealium.consentManager enable];
```

同意マネージャーをTealiumの初期化時に有効にすることが推奨されます。

**`isEnabled`**  
同意マネージャーが有効かどうかを確認します。

```objc
[_tealium.consentManager isEnabled];
```

**`disable`**  
同意マネージャーを無効にします。このメソッドは、Tealiumが完全に初期化された後に同意マネージャーを無効にします。

```objc
[_tealium.consentManager disable];
```

**`isDisabled`**  
同意マネージャーが無効かどうかを確認します。

```objc
[_tealium.consentManager isDisabled];
```

**`consentManagerDelegate`**  
TEALConsentManagerDelegateプロトコルに準拠する特定のクラスを登録します。

```objc
[_tealium setConsentManagerDelegate:(id&lt;TEALConsentManagerDelegate&gt;)];
```

**`setUserConsentStatus`**  
ユーザーの同意ステータスを設定します。アプリの同意管理設定画面から呼び出すことを想定しています。

```objc
[_tealium.consentManager setUserConsentStatus:Consented];
```

同意マネージャーは常に、ステータスが`Consented`の場合には、すべての利用可能な同意カテゴリーを含む同意済みカテゴリーリストを設定します。このメソッドでは、カテゴリーを選択的に設定することはできません。

| パラメーター | 説明 | 例 |
| --- | --- | --- |
| `TEALConsentStatus` | TEALConsentStatus列挙型の値 | [`Consented`, `NotConsented`, `Disabled`] |

**`setUserConsentCategories`**  
ユーザーの同意カテゴリーを設定します。アプリの同意管理設定画面から呼び出すことを想定しています。

```objc
[_tealium.consentManager setUserConsentCategories:@[@&#34;analytics&#34;]];
```

カテゴリーが設定されている場合、常に同意ステータスを`Consented`に設定します。

| パラメーター | 説明 | 例 |
| --- | --- | --- |
| `NSArray` | プリセットされたNSStringカテゴリーの配列 | `@[@&#34;analytics&#34;, @&#34;big_data&#34;]` |

**`setUserConsentStatus:withUserConsentCategories`**  
ユーザーの同意ステータスと同意カテゴリーを1つのメソッドで設定します。

```objc
[_tealium.consentManager setUserConsentStatus:Consented withUserConsentCategories:@[@&#34;analytics&#34;]];
```

| パラメーター | 説明 | 例の値 |
| --- | --- | --- |
| TEALConsentStatus | TEALConsentStatus列挙型の値 | [`Consented`, `NotConsented`] |
| NSArray | プリセットされたNSStringカテゴリーの配列 | `@[@&#34;analytics&#34;, @&#34;big_data&#34;]` |

**`userConsentStatus`**  
ユーザーの現在の同意ステータスを返します。

```objc
[_tealium.consentManager userConsentStatus];
```

**`userConsentCategories`**  
ユーザーの現在の同意カテゴリーを返します。

```objc
[_tealium.consentManager userConsentCategories];
```

**`isConsented`**  
ユーザーが同意しているかどうかを判断するための便利なメソッドです。

```objc
[_tealium.consentManager isConsented];
```

**`consentStatusString`**  
TEALConsentStatus列挙型の人間が読める文字列のための便利なメソッドです。
```objc
[TEALConsentManager consentStatusString:_tealium.consentManager.userConsentStatus];
```

**`resetUserConsentPreferences`**  
現在保存されているすべての同意設定をリセットします。同意ステータスは「不明」に戻り、カテゴリーはありません。
```objc
[_tealium.consentManager resetUserConsentPreferences];
```

**`setConsentLoggingEnabled`**  
[同意ログ]()機能を有効にし、同意ステータスの変更を監査目的でTealium Customer Data Hubに送信します。

```objc
[_tealium.consentManager setConsentLoggingEnabled:YES];
```

| パラメーター | 説明 | 例の値 |
| --- | --- | --- |
| `TEALConsentLoggingEnabled` | 同意ログの有効化または無効化 | [`YES`, `NO`] |

**`isConsentLoggingEnabled`**  
同意ログ機能の現在の状態を返します。
```objc
[_tealium.consentManager isConsentLoggingEnabled];
```

**`allCategories`**  
サポートされているすべての同意カテゴリーの完全なリストを返します。
```objc
[_tealium.consentManager allCategories];
```

### `TEALConfiguration`

**`enableConsentManager`**  
ライブラリが初めて起動されたときに、ユーザーの初期同意ステータスを設定します。保存された設定がある場合、それらは構成オブジェクトに渡された設定を上書きします。
```objc
self.configuration.enableConsentManager = YES;
```

同意マネージャーは常に、ステータスが`Consented`の場合には、すべての利用可能な同意カテゴリーを含む同意済みカテゴリーリストを設定します。このメソッドでは、カテゴリーを選択的に設定することはできません。

**`userConsentStatus`**  
ライブラリが初めて起動されたときに、ユーザーの初期同意ステータスを設定します。保存された設定がある場合、それらは構成オブジェクトに渡された設定を上書きします。
```objc
self.configuration.userConsentStatus = Consented;
```

| パラメーター | 説明 | 例の値 |
| --- | --- | --- |
| `TEALConsentStatus` | TEALConsentStatus列挙型の値 | [`Consented`, `NotConsented`, `Disabled`] |

**`userConsentCategories`**  
ライブラリが初めて起動されたときに、ユーザーの初期同意カテゴリーを設定します。保存された設定がある場合、それらは構成オブジェクトに渡された設定を上書きします。
```objc
self.configuration.userConsentCategories = @[@&#34;analytics&#34;, @&#34;retargeting&#34;];
```

| パラメーター | 説明 | 例の値 |
| --- | --- | --- |
| `NSArray` | プリセットされたNSStringカテゴリーの配列 | `@[@&#34;analytics&#34;, @&#34;big_data&#34;]` |


### `TEALConsentManagerDelegate`

**`consentManagerDidChangeWithState`**  
同意マネージャーのユーザー同意ステータスが変更されたときに呼び出されるメソッドです。

```objc
- (void)consentManagerDidChangeWithState:(TEALConsentStatus)consentStatus;
```

**`consentManagerDidUpdateConsentCategories`**  
同意マネージャーのユーザー同意カテゴリーが更新されたときに呼び出されるメソッドです。

```objc
-(void)consentManagerDidUpdateConsentCategories:(NSArray * \_Nullable)categories;
```

**`consentManagerWillDropDispatch`**  
同意マネージャーがトラッキングコールを破棄する予定の場合に呼び出されるメソッドです。たとえば、ユーザーがトラッキングを拒否した場合です。

```objc
- (void)consentManagerWillDropDispatch:(TEALDispatch * \_Nullable)dispatch;
```

**`consentManagerWillQueueDispatch`**  
同意マネージャーが「不明」の状態にある場合に呼び出されるメソッドです。ユーザーが同意または拒否するまで、トラッキングコールはローカルにキューに入れられます。

```objc
- (void)consentManagerWillQueueDispatch:(TEALDispatch * \_Nullable)dispatch;
```

## 同意カテゴリー

以下は、サポートされているすべての同意カテゴリーのリストです。

*   `analytics`
*   `affiliates`
*   `display_ads`
*   `email`
*   `personalization`
*   `search`
*   `social`
*   `big_data`
*   `mobile`
*   `engagement`
*   `monitoring`
*   `cdm`
*   `cdp`
*   `cookiematch`
*   `misc`

## TEALConsentStatus

**`Unknown`**  
`Unknown`ステータスは、同意マネージャーのデフォルト設定です。この状態では、同意が提供されるまで同意マネージャーはイベントをローカルにキューに入れます。

```objc
self.tealium.consentManager.userConsentStatus = Unknown
```

**`Consented`**  
`Consented`ステータスは、ユーザーがトラッキングに同意した場合に設定されます。この状態では、同意マネージャーは通常どおりすべてのトラッキングコールを許可します。

```objc
self.tealium.consentManager.userConsentStatus = Consented
```

**`NotConsented`**  
`NotConsented`ステータスは、ユーザーがトラッキングを拒否した場合に設定されます。この状態では、同意マネージャーはすべてのトラッキングコールを破棄し、SDKの処理を停止します。

```objc
self.tealium.consentManager.userConsentStatus = NotConsented
```

