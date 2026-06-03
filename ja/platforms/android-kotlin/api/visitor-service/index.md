---
title: VisitorService
description: TealiumがAndroid（Kotlin）向けに提供するVisitorServiceクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/android-kotlin/api/visitor-service/
---
## クラス: `VisitorService`

以下は、Kotlin用の`VisitorService`モジュールの一般的に使用されるメソッドとプロパティをまとめたものです。

| メソッド/プロパティ | 説明 |
| ----- | ------ |
| [`overrideVisitorServiceUrl`](#overridevisitorserviceurl) | 現在のVisitorProfileを取得するために使用されるURLを上書きする`TealiumConfig`オプション |
| [`overrideVisitorServiceProfile`](#overridevisitorserviceprofile) | 現在のVisitorProfileを取得するために使用されるプロファイル名を上書きする`TealiumConfig`オプション |
| [`requestVisitorProfile()`](#requestvisitorprofile) | 現在のVisitorProfileが更新されるように要求するメソッド |
| [`visitorServiceRefreshInterval`](#visitorservicerefreshinterval) | SDKが自動的に最新のVisitorProfileを取得するまでの最小時間間隔を構成する`TealiumConfig`オプション |

### `overrideVisitorServiceUrl`

`TealiumConfig`オブジェクトの拡張プロパティ。VisitorServiceモジュールがプロジェクトに含まれている場合にのみ利用可能です。

VisitorServiceモジュールがVisitorProfileオブジェクトを取得するために使用するURLを上書きします。
デフォルトのURL: `&#34;https://visitor-service.tealiumiq.com/{ACOUNT_NAME}/{PROFILE_NAME}/{VISITOR_ID}&#34;`

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceUrl = url
```

### `overrideVisitorServiceProfile`

`TealiumConfig`オブジェクトの拡張プロパティ。VisitorServiceモジュールがプロジェクトに含まれている場合にのみ利用可能です。

VisitorServiceモジュールがVisitorProfileオブジェクトを取得するために使用するTealiumのプロファイル名を上書きします。デフォルトでは、VisitorServiceモジュールは`TealiumConfig`で構成されたプロファイル名を使用します。

```java
val config = TealiumConfig(...)
config.overrideVisitorServiceProfile = &#34;main&#34;
```

### `requestVisitorProfile`

VisitorProfileが更新されるように要求するメソッド。これは、各ディスパッチ、またはディスパッチのバッチがTealium Customer Data Hubに送信された後に発生します。

このメソッドを使用して、他の任意の時点で更新を要求します。これはネットワークリクエストを行うため、コルーチンから呼び出す必要がある`suspend`関数です。メインスレッド上では呼び出されません。

```java
runBlocking(Dispatchers.IO) {
    tealium.visitorService?.requestVisitorProfile()
}
```

### `visitorServiceRefreshInterval`

VisitorProfileデータの更新間隔を秒単位で構成します。`requestVisitorProfile()`への呼び出しはこの構成を無視します。

デフォルト: 300 (5分)

```java
val config = TealiumConfig(...)
config.visitorServiceRefreshInterval = TimeUnit.MINUTES.toSeconds(30) // 30分
```

## インターフェース: `VisitorUpdatedListener`

`VisitorUpdatedListener`はリスナークラスです。更新があるたびにVisitorProfileの最新バージョンを受け取るために登録します。実装する必要があるメソッドは1つだけです：[`onVisitorUpdated(visitorProfile: VisitorProfile)`](#onVisitorUpdated)。

### `onVisitorUpdated`

既存のクラスに`onVisitorUpdated`メソッドを実装するか、`Tealium`インスタンスを作成した後に匿名オブジェクトを渡します。以下の例は後者を示しています。

```java
val tealium = Tealium.create(...) {
    events.subscribe(object : VisitorUpdatedListener {
        override fun onVisitorUpdated(visitorProfile: VisitorProfile) {
            Logger.dev(&#34;--&#34;, &#34;VisitorProfile updated: $visitorProfile&#34;)
        }
    })
}
```

利用可能なプロパティの詳細については、[VisitorProfile](/ja/platforms/android-kotlin/api/visitor-profile/)のドキュメンテーションを参照してください。
