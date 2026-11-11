---
title: タグ
description: ブラウザベースのタグをTealium iQタグ管理と統合する方法について説明します。
url: https://docs.tealium.com/ja/partners-and-industries/partner-with-us/tags/
---


JavaScriptタグをTealiumタグマーケットプレイスで提供したいとお考えですか？長期にわたるリリースサイクルを経ることなく、ユーザーがタグをサイトへシームレスに追加できるようにしたいとお考えですか？その場合、このガイドではタグの仕組みと、Tealium iQタグ管理との公式統合によって得られる追加のメリットについて説明します。

## タグの仕組み

タグマーケットプレイスのタグは、タグの機能を完全に統合したものです。つまり、タグで必要となるすべてのオプションとトラッキング対象イベントが、Tealiumユーザーのアカウント内で、構成可能な単一のタグインスタンスにまとめられます。

### 構成

タグの内部動作はほとんどのユーザーから隠されているため、ユーザーはポイント＆クリック形式のセットアップオプションに集中できます。ただし、JavaScriptの操作に慣れているTealiumユーザーは、タグを実行するコードを利用できます。

タグは次の3つの要素で管理されます。

* **構成**   
タグの構成はタグのインスタンスごとに一度構成され、通常はページごとに変わることはありません。
[タグ構成の詳細](https://docs.tealium.com/manage-templates/)。
* **ロードルール**  
ロードルールは、ページまたはイベントでタグを読み込むタイミングを決定します。ロードルールの条件は、データレイヤーの値に基づきます。
[ロードルールの詳細](https://docs.tealium.com/about-load-rules/)。
* **データマッピング**  
データマッピングは、タグがデータレイヤーから必要とする動的な値と、ベンダーが使用する対応する変数名を決定します。また、マッピングによってページ内イベントのトラッキング方法も決まります。
[データマッピングの詳細](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)。

### ブラウザでの読み込み

ベンダータグは、Tealium Universal Tag（utag.js）によって読み込まれます。これは、iQタグ管理アカウントの構成ロジックを含むラッパータグです。後続のベンダータグは非同期JavaScriptを使用して読み込まれ、タグマネージャーの外部で実行される場合と同じように動作します。

ベンダーは、同じタグライブラリまたはイメージピクセルがページのDOMに表示されることを想定できます。Tealiumでは、お客様の仕様どおりにタグを読み込むために最大限の努力を払っています。まれにコードを変更する必要がある場合でも、最終的なトラッキングビーコンがお客様の要件を満たすようにします。


<blockquote>
Tealiumでは、A/Bテストおよび多変量テストのベンダーをサポートするため、同期JavaScriptを読み込むこともできます。
</blockquote>


### Eコマース値

製品データと注文データを収集するEコマースタグ向けに、TealiumではEコマース拡張機能と呼ばれる便利な機能を提供しています。この機能により、すべての標準Eコマースデータがタグと自動的に統合されます。アカウントでEコマース拡張機能を構成すると、これらの値を必要とするすべてのタグに対するグローバルデータマッピングとして機能します。これにより、この種のタグのセットアップに必要な作業を最小限に抑えることができます。

[Eコマース拡張機能の詳細](https://docs.tealium.com/e-commerce-extension/)。

## タグの種類

タグソリューションの実装に加えて、Tealiumではお客様のシステム機能に応じた追加の統合オプションを提供できます。

### 標準

ほぼすべてのタグは、JavaScriptファイルを読み込み、コードを初期化し、ページから動的データを収集して、タグをトリガーするという同じ規則に従います。この標準フレームワークは、静的パラメータを持つ単純なイメージピクセルから、ページタイプごとに異なるコードを実行し、ページから動的データを収集する複雑なJavaScriptライブラリまで、さまざまな形態があります。

### Cookie Match

Cookie Matchタグの目的は、特殊なリクエストを使用して、Tealiumとお客様のシステム間で訪問識別子を同期することです。これにより、お客様のシステム固有の訪問IDをTealiumのサーバーサイドプラットフォームと共有し、その代わりにTealiumの訪問IDを受け取ることができます。この種の統合は、_標準タグに加えて_使用します。

#### 例

次の例は、Cookie Matchリクエストを示しています。

```http
GET https://sync.example-dsp.net/get-userId?
tealium_visitor_id=abxyz0909&
tealium_account=my_account&
tealium_profile=main&
tealium_datasource=abc123 
```

このリクエストはブラウザから送信され、Tealiumの訪問IDをお客様のシステムへ送ります。その結果、お客様のシステムの訪問IDとTealiumの訪問IDを含む転送リクエストがTealiumへ返されます。これは、Tealiumがマッチテーブルをホストしていることを示しており、推奨される方式です。Tealiumへの最終リクエストには、指定されたすべてのTealium変数と、ベンダー側で照合されたIDが含まれます。

次に、Tealiumへリダイレクトする例を示します。

```http
GET https://collect.tealiumiq.com/vdata?
dsp_uid=4595-23423442&
tealium_visitor_id=abxyz0909&
tealium_account=my_account&
tealium_profile=main&
tealium_datasource=abc123
```

次のCookie Matchの例では、DSPのエンドポイントが対応している場合、リダイレクトリクエストをURLパラメータとして渡します。

```http
GET https://sync.example-dsp.net/get-userId?
redirect=https://collect.tealiumiq.com/vdata?dsp_uid=$UID&tealium_visitor_id=abxyz0909&tealium_account=egbrand&tealium_profile=main&tealium_datasource=abc123
```

### サーバーサイド対応

サーバーサイド対応タグには、Tealium EventStreamとAudienceStreamへイベントを直接送信できる機能が追加されています。たとえば、マウスの動きをトラッキングしてユーザーの感情を推測するユーザーエクスペリエンスベンダーは、特定のイベントをTealium Collectへ直接送信できます。この種の統合は、_標準タグに含まれます_。

次のサンプル関数は、Tealiumのイベントエンドポイントへデータを送信します。  
```javascript
window.tealium.sendEvent = function(event_data) {
    //Send Event to CDH event endpoint
    event_data['tealium_event'] = "EVENT_NAME";
    event_data['tealium_account'] = b.tealium_account; // required
    event_data['tealium_profile'] = b.tealium_profile; // required
    event_data['tealium_visitor_id'] = b.tealium_visitor_id; // required
    event_data['tealium_trace_id'] = b["cp.trace_id"]; // optional
    event_data['tealium_datasource'] = 'DATASOURCE_KEY'; // optional

    var data = new FormData();
    data.append("data", JSON.stringify(event_data));

    if (window.utag && utag.data && utag.data.tealium_account) {
        var xhr = new XMLHttpRequest();
        xhr.open("POST", "https://collect.tealiumiq.com/event?");
        xhr.send(data);
        }
    return true;
};
```

## パートナーになる

お客様のテクノロジーを統合するには、[お問い合わせください](https://tealium.com/tealium-partner-network/)。