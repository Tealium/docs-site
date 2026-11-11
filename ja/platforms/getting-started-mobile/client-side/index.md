---
title: クライアントサイド
description: クライアントサイドソリューションの機能について説明します。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/client-side/
---
## Web

タグ管理は、ベンダータグの構成とビジネスロジックを `utag.js` という静的なJavaScriptファイルに保存するクライアントサイドソリューションです。訪問がサイトを閲覧すると、このファイルがブラウザ（クライアントサイド）で読み込まれて実行され、読み込むベンダータグとそのデータの送信方法が決定されます。これらのファイルは、ブラウザによって取得された後、以降のページビューでキャッシュされ、ネットワークトラフィックとページパフォーマンスが最適化されます。

詳しくは、[タグ管理の仕組み](https://docs.tealium.com/how-tag-management-works/)を参照してください。


## モバイル

タグ管理では、モバイルアプリのタグと構成を管理するために、iOS用とAndroid用にそれぞれ個別の[モバイルプロファイル](https://docs.tealium.com/create-mobile-profile/)を使用します。モバイルプロファイルによって `mobile.html` というファイルが生成され、Tealiumの次のパスにパブリッシュされます。

`http://tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/mobile.html`

モバイルアプリにTealiumを追加すると、クライアントサイドソリューションは非表示のWebViewを使用して、モバイルデバイス向けに最適化された `mobile.html` を読み込みます。このページにはTealium SDKの動作を制御する構成が含まれており、`utag.js` を読み込んでタグ構成を実行します。

`mobile.html` の内容の例：

```html
<!DOCTYPE html>
<!--tealium tag management - mobile.webview ut4.0.201905291649, Copyright 2019 Tealium.com Inc. All Rights Reserved.-->
<html>
<head><title>Tealium Mobile Webview</title></head>
<body>
<script type="text/javascript">
var utag_cfg_ovrd={noview:true};
var mps = {
    "5": {
        "_is_enabled":"true",
        "battery_saver":"true",
        "dispatch_expiration":"-1",
        "enable_collect":"false",
        "enable_s2s_legacy":"false",
        "enable_tag_management":"true",
        "event_batch_size":"1",
        "minutes_between_refresh":"15.0",
        "offline_dispatch_limit":"100",
        "override_log":"",
        "wifi_only_sending":"false"
    },
    "_firstpublish":"true"
}
</script>
<script type="text/javascript" src="//tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/utag.js"></script>
</body>
</html>
```

このクライアントサイドソリューションでは、従来のタグ管理ワークフローに従ってアプリにタグをデプロイし、トラッキング動作に関連するモバイル構成を調整できます。

次の図は、訪問がモバイルアプリを使用する際に、タグ管理がベンダータグ構成を読み込む仕組みを示しています。この例では、Tealium SDKがトラッキングされた購入イベントを、非表示のWebView内のJavaScriptトラッキングコールに変換する方法を示しています。ベンダータグはモバイルWebページ上と同様に非表示のWebView内で実行され、トラッキングデータはアプリ（クライアントサイド）からベンダーへ直接送信されます。

![](https://docs.tealium.com/images/platforms/getting-started-mobile/tag_management_data_flow_diagram.png)

### メリット

クライアントサイドのアプローチには、次のメリットがあります。

* **タグベンダーのサポート**
クライアントサイドソリューションはタグ管理を使用してデプロイされるため、既存のタグマーケットプレイス統合を利用できます。
* **データレイヤーのカスタマイズ**
[拡張機能](https://docs.tealium.com/about-extensions/)を使用することで、データレイヤーをより柔軟にカスタマイズできます。

### 考慮事項

次の点に注意してください。

* **WebViewの動作**
ネイティブWebViewはiOS／Android APIによって提供されるため、Tealiumでは制御できない動作を示す場合があります。
* **メモリ使用量**
ネイティブWebViewを使用すると、アプリのメモリ使用量が若干増加します。
* **ネットワークトラフィック**
アプリにデプロイするタグが多いほど、ベンダーのJavaScriptタグと、それらによって生成されるトラッキングピクセルの読み込みにより、ネットワークトラフィックが増加します。

## ユースケース

クライアントサイドソリューションは、次のシナリオに最適です。

### タグ管理のみ

タグ管理のみを契約しており、イベントストリーミングを利用できない場合。

### 複雑な分析

複雑な分析実装が必要であり、必要なデータレイヤーを追加するためのリソースがない場合、またはデプロイまでの期間が短い場合。クライアントサイドのタグ管理ソリューションを使用して拡張機能を実行できるため、分析要件に応じて組み込みのデータレイヤーを操作できます。また、ネイティブアプリで多大な開発時間を費やす代わりに、タグ管理で迅速に構成できます。

### 必須のベンダーSDK

Firebase、プッシュ通知、コンテンツの変更、アトリビューションフィンガープリンティングなど、サードパーティのベンダーSDKが提供するモバイル固有の機能が必要な場合。クライアントサイドソリューションでは[リモートコマンド](https://docs.tealium.com/ja/platforms/remote-commands/)を利用できます。これは、非表示のWebView内からネイティブコードブロックをトリガーし、タグ管理内で構成するための仕組みです。

## サポートされるライブラリ

次のプラットフォームでは、タグ管理のクライアントサイドソリューションがサポートされています。

* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-java/)
* [Tealium for Cordova](https://docs.tealium.com/ja/platforms/cordova/)
* [Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/)
* [Tealium for React Native](https://docs.tealium.com/ja/platforms/react-native/)
* [Tealium for Xamarin](https://docs.tealium.com/ja/platforms/xamarin/)

## Tealium Collectタグ

[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)は、Tealium Customer Data Hubのサーバーサイド製品であるイベントストリーミングにデータを送信します。このタグは、[ネイティブCollectモジュール](https://docs.tealium.com/ja/platforms/getting-started-mobile/server-side/#tealium-collect-module)に対応するクライアントサイドソリューションです。アプリで両方を使用すると利用量が倍増し、アカウントに追加料金が発生します。

クライアントサイドのTealium Collectタグの主なメリットは、収集前に拡張機能を使用してデータレイヤーをカスタマイズできることです。