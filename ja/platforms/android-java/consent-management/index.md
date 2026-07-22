---
title: 同意管理
description: Androidのための同意を実装する方法を学びます。
url: https://docs.tealium.com/ja/platforms/android-java/consent-management/
---
## 使用法

同意管理モジュールの使用は推奨されており、ライブラリに自動的に含まれ、初期化時にネイティブコードで有効になります。

対応しているプラットフォームは、Androidモバイル、Android TV、Android Wearを含みます。

詳細については、[platforms/getting-started-mobile/consent-management](https://docs.tealium.com/platforms/getting-started-mobile/consent-management/)を参照してください。

## サンプルアプリ

私たちのライブラリ、トラッキング方法、ベストプラクティスの実装に慣れるために、Android Consent Managementの[サンプルアプリ](https://github.com/Tealium/tealium-android/tree/master/Samples/ConsentManagerDemoApp)を探索してみてください。

Androidの同意管理方法のリストについては、[APIリファレンス](https://docs.tealium.com/ja/platforms/android-java/api/consent-manager/)を参照してください。

## 有効化

以下の例は、同意管理を有効にする方法を示しています：

```java
//TealiumHelper.java
import com.tealium.library.ConsentManager;

public static final String TEALIUM_MAIN = "main";

public static void initialize(Application application) {
	final Tealium.Config config = Tealium.Config.create(application, "ACCOUNT", "PROFILE", "ENVIRONMENT");

	config.enableConsentManager(TEALIUM_MAIN); //enable with tealium instance name

	final Tealium tealiumInstance = Tealium.createInstance(TEALIUM_MAIN, config);
}
```

## データレイヤー

同意管理が有効になっている間、以下の変数が各トラッキング呼び出しで送信されます：

| 変数名 | 説明 | 例 |
| --- | --- | --- |
| `policy` | 同意が収集されたポリシー | `gdpr` |
| `consent_status` | ユーザーの現在の同意ステータス | `consented` |
| `consent_categories` | ユーザーが同意している現在のカテゴリー | `[ANALYTICS, CDP]` |


## 例

### シンプルなオプトイン  

以下の例は、同意管理にオプトインする方法を示しています：

```java
tealiumInstance.getConsentManager()
      .setUserConsentStatus(ConsentManager.ConsentStatus.CONSENTED);
```

### グループオプトイン

以下の例は、カテゴリーベースの同意モデルを示しています。ここでは、トラッキングカテゴリーがより少ない数の高レベルカテゴリーにグループ化され、それらはあなたによって定義されます：

```java
tealiumInstance.getConsentManager()
     .setUserConsentStatusWithCategories(ConsentManager.ConsentStatus.CONSENTED,
          new String[] {ConsentManager.ConsentCategory.ANALYTICS});
```

例えば、Tealiumの同意カテゴリー`"big_data"`、`"analytics"`、`"monitoring"`を"performance"という単一のカテゴリーにグループ化することを選択することができます。これは、全カテゴリーから選択するよりもユーザーにとって簡単かもしれません。これを最も許可しないものから最も許可するもの（全カテゴリー）までのスライダーインターフェースで表現することを選択することができます。

![](https://docs.tealium.com/images/platforms/android/consent-slider.gif)

### カテゴリーベースのオプトイン

以下の例は、ユーザーが全カテゴリーから各カテゴリーを明示的に選択しなければならないカテゴリーベースの同意モデルを示しています。デフォルトは`UNKNOWN`で、ユーザーが同意を提供するまでヒットをキューに入れます。ユーザーが任意のカテゴリーに同意すると、イベントがデキューされ、同意カテゴリーデータが各トラッキング呼び出しに追加されます。

```java
tealiumInstance.getConsentManager()
   .setUserConsentStatusWithCategories(ConsentManager.ConsentStatus.CONSENTED,
       new String[] {ConsentManager.ConsentCategory.ANALYTICS,
                     ConsentManager.ConsentCategory.PERSONALIZATION});
```


![](https://docs.tealium.com/images/platforms/android/consent-categories.gif)

