---
title: AdobeVisitorServiceモジュール
description: 各ユーザーに対してクロスデバイス訪問IDを提供します。
url: https://docs.tealium.com/ja/platforms/android-kotlin/module-list/adobe-visitor-service/
---
Adobe Visitor Serviceモジュールは、訪問のExperience Cloud ID（ECID）を取得および維持するためにAdobeのREST APIと直接連携します。

[AdobeVisitorService](/ja/platforms/getting-started-mobile/adobe-visitor-service/)モジュールについてもっと学びましょう。

## 要件

* [Tealium Kotlin for Android](/ja/platforms/android-kotlin/)
* 有効なAdobeアカウントとAdobe組織ID

## サンプルアプリ

Android用の[AdobeVisitorServiceモジュールサンプルアプリ](https://github.com/Tealium/tealium-kotlin/tree/master/mobile)を探索して、Tealiumライブラリとベストプラクティスの実装についての知識を深めましょう。

## インストール

AdobeVisitorServiceモジュールはTealium SDKの初期化時に構成され、リモート構成機能はありません。

このモジュールは`DispatchValidator`として機能し、Adobe組織IDなしでは送信が阻止されます。Adobe APIからECIDを取得しようとしますが、5回の失敗後は、データ損失を避けるためにECIDなしでの続行が許可されます。データ送信は有効なECIDを持つことよりも優先されます。

ECIDが取得できなかった可能性のある原因は以下の通りです：

- 無効な応答、例えば応答は受け取ったが有効なECIDを含んでいなかった。
- 応答がなかった。
- Adobe組織IDが無効だった。

### Maven

Tealium Mavenリポジトリを追加：http://maven.tealiumiq.com/releases/

依存関係を追加：`com.tealium:kotlin-adobe-visitor`


```kotlin
import com.tealium.adobe.api.AdobeAuthState
import com.tealium.adobe.api.AdobeVisitor
import com.tealium.adobe.api.ResponseListener
import com.tealium.adobe.kotlin.*

...

val config = TealiumConfig(
      app,
      &#34;&lt;account&gt;&#34;,
      &#34;&lt;profile&gt;&#34;,
      Environment.DEV,
      collectors = mutableSetOf(Collectors.AdobeVisitor),
      dispatchers = mutableSetOf(Dispatchers.Collect)
  )
  config.adobeVisitorOrgId = BuildConfig.ADOBE_ORG_ID

  tealium = Tealium.create(BuildConfig.TEALIUM_INSTANCE, config)
```

既知の訪問IDをリンクするか認証状態を構成するには、[既知の訪問IDと認証状態を構成する](/ja/platforms/getting-started-mobile/adobe-visitor-service/#set-a-known-visitor-id-and-authentication-state)を参照してください。