---
title: iOSおよびAndroidのGoogleアナリティクスで「広告機能」を構成する
description: この記事では、iOSおよびAndroidのGoogleアナリティクスで広告機能を構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/setting-up-advertising-features-in-google-analytics-for-ios-and-android/
---
## 背景

AndroidおよびiOS用のネイティブGoogleアナリティクスSDKは、人口統計と興味報告などの広告機能を有効にする方法を提供します。しかし、TealiumのSDKを介してGAを実装する場合、これらの機能はデフォルトでは得られません。これは、すべてのTealiumユーザーが広告データを必要とするわけではなく、デフォルトで含まれていた場合、インストール時に追加の許可が必要になるためです。

## 前提条件

1. この機能を使用するには、アプリのデータレイヤーに以下のデータがTealiumトラッキングAPIを介して公開されていることを確認する必要があります：
  * Android広告ID（通称「ADID」） - この構成方法の詳細については、以下の付録Aを参照してください
  * 広告主用iOS ID（通称「IDFA」） - この構成方法の詳細については、以下の付録Bを参照してください

1. さらに、Google Universal Analyticsタグテンプレートが20151026（2015年10月26日）より後のバージョンであることを確認する必要があります。不明な場合は、[Tag Status Checker]()ツールを使用してプロファイルのテンプレートバージョンを確認してください。現在のタグテンプレートがカスタマイズされていないことを確認してからアップグレードしてください。不明な場合は、アカウントマネージャーに相談してください。
1. Googleアナリティクスプロパティで人口統計と興味報告を有効にする必要があります。このタスクは、GAアカウント構成内でGA管理者によって完了する必要があります。

### GAタグの構成

1. Tealium IQでADIDおよびIDFAパラメータを表す新しい[データソース]()を追加します。データソース名は`idfa`および`adid`で十分ですが、アプリ開発者がUIで指定したものと同じ名前を使用していることを確認してください。そうでない場合、機能しません。
1. 広告追跡機能が有効であることをGAに通知するために、追加のパラメータが必要です。これを構成するために、最終的にGAの`ate`パラメータにマッピングされる1つの追加データソースが必要です：&lt;br&gt;
![](/images/client-side-tags/ate.png)

1. 新しい[Set Data Values]()拡張機能を追加し、新しい広告追跡データソースを文字列値`1`に構成します：
![](/images/client-side-tags/2016-04-14-1724.png)

1. 次のようにマッピングを構成します。`&amp;`（アンパサンド）記号は意図的であり、マッピング名の一部です。これらのマッピングはカスタムマッピングとして手動で入力する必要があります。現在、マッピングツールボックスには含まれていません：
![](/images/client-side-tags/2016-04-14-1729.png)コピー＆ペーストの簡単のために、ここにテキスト形式でマッピング名を示します：
```
set.&amp;idfa
set.&amp;adid
set.&amp;ate
```

1. 上記の項目がすべて構成されたら、プロファイルを保存して公開します。現在、ADIDおよびIDFAがデータレイヤーにない場合でも、これらのマッピングを事前に追加することができます。開発者がこれらをアプリに追加すると、アクティブになります。

### 重要な注意点

この機能を有効にすると、データがGAに表示されるまで最大24時間かかる場合があります。ヒットが少なすぎると、GAはデータを表示しません。これは個々のユーザーを誤って特定する可能性があるためです。特定のトラフィックの閾値に達するまで、GAはデータを表示することを許可しません。

## 付録A - AndroidのデータレイヤーにADIDを追加する

このガイドでは、AndroidでADIDを取得する方法について説明します。これは外部リンクであり、Tealiumはその内容を管理していません：

&lt;https://www.safaribooksonline.com/blog/2014/01/16/advertising-id-android-kitkat/&gt;

ADIDを取得したら、次のAPIコールを使用してTealium Android SDKを介してデータを追加できます。これにより、アプリ内の各後続ヒットでデータが利用可能になり、アプリの起動間で値が維持されます：

Tealium SDK v4.x

```
Tealium.getGlobalCustomData().edit().putLong(&#34;adid&#34;, &#34;&amp;lt;your advertising id here&amp;gt;&#34;).apply();
```

Tealium SDK v5.x：

```
 Tealium.getInstance(&#34;instancename&#34;).getDataSources().getPersistentDataSources().edit().putString(&#34;adid&#34;, &#34;&amp;lt;your advertising id here&amp;gt;&#34;).apply();
```

NB: `instancename`をアプリで使用している実際のインスタンス名に置き換え、プレースホルダーテキストを実際のADIDに置き換えてください。

## 付録B - iOSのデータレイヤーにIDFAを追加する

このガイドでは、iOSでIDFAを取得する方法について説明します。これは外部リンクであり、Tealiumはその内容を管理していません：

&lt;http://www.brianjcoleman.com/how-to-use-apples-identifier-for-advertisers-idfa/&gt;

IDFAを取得したら、次のAPIコールを使用してTealium iOS SDKを介してデータを追加できます。これにより、アプリ内の各後続ヒットでデータが利用可能になり、アプリの起動間で値が維持されます：

Tealium SDK v4.x

```
[Tealium addGlobalCustomData&amp;colon;@{@&#34;idfa&#34; : @&#34;&amp;lt;your idfa here&amp;gt;&#34; }];
```

Tealium SDK v5.x

```
 [[Tealium instanceForKey:@&#34;instancename&#34;] addPersistentDataSources: @{@&#34;idfa&#34;:@&#34;&lt;your idfa here&gt;&#34;}];
```

NB: `instancename`をアプリで使用している実際のインスタンス名に置き換え、プレースホルダーテキストを実際のIDFAに置き換えてください。