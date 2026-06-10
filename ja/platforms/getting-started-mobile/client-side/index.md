---
title: クライアントサイド
description: クライアントサイドソリューションの機能について学びましょう。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/client-side/
---
## Web

Tealium iQタグ管理は、ベンダータグの構成とビジネスロジックを`utag.js`という静的JavaScriptに保存するクライアントサイドソリューションです。訪問があなたのサイトを閲覧すると、このファイルがブラウザ（クライアントサイド）でロードされ、どのベンダータグをロードし、データをどのように送信するかを決定します。これらのファイルがブラウザによって取得されると、ネットワークトラフィックとページパフォーマンスを最適化するために、次のページビューに対してキャッシュされます。

[how Tag Management works]()について詳しく学びましょう。


## モバイル

iQタグ管理では、モバイルアプリのタグと構成を管理するために、iOSとAndroidのそれぞれに対して別々の[モバイルプロファイル]()を使用します。モバイルプロファイルは`mobile.html`というファイルを生成し、以下のTealiumのパスに公開します：

`http://tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/mobile.html`

Tealiumをモバイルアプリに追加すると、クライアントサイドソリューションは隠されたwebviewを使用して`mobile.html`をロードします。これはモバイルデバイスに最適化されています。このページには、Tealium SDKの動作を制御する構成が含まれており、`utag.js`をロードしてタグ構成を実行します。

`mobile.html`のサンプル内容：

```html
&lt;!DOCTYPE html&gt;
&lt;!--tealium tag management - mobile.webview ut4.0.201905291649, Copyright 2019 Tealium.com Inc. All Rights Reserved.--&gt;
&lt;html&gt;
&lt;head&gt;&lt;title&gt;Tealium Mobile Webview&lt;/title&gt;&lt;/head&gt;
&lt;body&gt;
&lt;script type=&#34;text/javascript&#34;&gt;
var utag_cfg_ovrd={noview:true};
var mps = {
    &#34;5&#34;: {
        &#34;_is_enabled&#34;:&#34;true&#34;,
        &#34;battery_saver&#34;:&#34;true&#34;,
        &#34;dispatch_expiration&#34;:&#34;-1&#34;,
        &#34;enable_collect&#34;:&#34;false&#34;,
        &#34;enable_s2s_legacy&#34;:&#34;false&#34;,
        &#34;enable_tag_management&#34;:&#34;true&#34;,
        &#34;event_batch_size&#34;:&#34;1&#34;,
        &#34;minutes_between_refresh&#34;:&#34;15.0&#34;,
        &#34;offline_dispatch_limit&#34;:&#34;100&#34;,
        &#34;override_log&#34;:&#34;&#34;,
        &#34;wifi_only_sending&#34;:&#34;false&#34;
    },
    &#34;_firstpublish&#34;:&#34;true&#34;
}
&lt;/script&gt;
&lt;script type=&#34;text/javascript&#34; src=&#34;//tags.tiqcdn.com/utag/ACCOUNT/PROFILE/ENVIRONMENT/utag.js&#34;&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
```

このクライアントサイドソリューションにより、従来のタグ管理ワークフローに従ってアプリにタグをデプロイし、トラッキング行動に関連するモバイル構成を調整することができます。

以下の図は、訪問がモバイルアプリを使用する際に、iQタグ管理がベンダータグ構成をロードする方法を示しています。この例では、Tealium SDKがトラッキングされた購入イベントを隠されたwebview内のJavaScriptトラッキングコールに変換する方法を示しています。ベンダータグは隠されたwebview内で実行され、トラッキングデータはアプリ（クライアントサイド）から直接ベンダーに送信されます。

![](/images/platforms/getting-started-mobile/tag_management_data_flow_diagram.png)

### 利点

クライアントサイドのアプローチには以下の利点があります：

* **タグベンダーサポート**
クライアントサイドソリューションはiQタグ管理を使用してデプロイされるため、既存の[Tag Marketplace]()の統合にアクセスできます。
* **データレイヤーカスタマイズ**
[extensions]()を使用したデータレイヤーのカスタマイズオプションが増えます。

### 考慮事項

以下の点を考慮してください：

* **WebViewの挙動**
ネイティブのwebviewsはiOS/AndroidのAPIによって提供され、Tealiumの制御を超えた挙動を示すことがあります。
* **メモリ使用量**
ネイティブのwebviewはアプリ内でわずかに多くのメモリを使用します。
* **ネットワークトラフィック**
アプリにデプロイするタグが多いほど、ベンダーのJavaScriptタグとそれに伴うトラッキングピクセルのロードにより、ネットワークトラフィックが増加します。

## ユースケース

クライアントサイドソリューションは、以下のシナリオに最適です。

### iQタグ管理のみ
あなたはiQタグ管理のみを購読しており、Tealium EventStreamにはアクセスできません。

### 複雑な分析
複雑な分析の実装を行っており、必要なデータレイヤーを追加するリソースがないか、またはデプロイするための時間が短い場合。クライアントサイドのタグ管理ソリューションを使用して拡張を実行することで、分析のニーズに合わせて組み込みのデータレイヤーを操作し、ネイティブアプリの高価な開発時間をiQタグ管理の迅速な構成作業にオフロードすることができます。

### 必要なベンダーSDK
Firebase、プッシュ通知、コンテンツの変更、またはアトリビューションフィンガープリンティングなど、サードパーティのベンダーSDKからモバイル特有の機能が必要な場合。クライアントサイドソリューションは、隠されたwebview内からネイティブコードブロックをトリガーし、iQタグ管理内で構成する方法である[remote commands](/ja/platforms/remote-commands/)を提供します。

## サポートされているライブラリ

以下のプラットフォームは、タグ管理クライアントサイドソリューションをサポートしています：

* [Tealium for Android](/ja/platforms/android-java/)
* [Tealium for Cordova](/ja/platforms/cordova/)
* [Tealium for iOS](/ja/platforms/ios-swift/)
* [Tealium for React Native](/ja/platforms/react-native/)
* [Tealium for Xamarin](/ja/platforms/xamarin/)

## Tealium Collectタグ

[Tealium Collect Tag]()は、Tealium Customer Data Hubのサーバーサイド製品EventStreamにデータを送信します。このタグは、[native Collect Module](/ja/platforms/getting-started-mobile/server-side/#tealium-collect-module)のクライアントサイドソリューションです。アプリ内で両方を使用すると、使用量が2倍になり、アカウントに追加の料金が発生します。

クライアントサイドのTealium Collectタグの主な利点は、収集前にデータレイヤーをカスタマイズするための拡張の使用能力です。


