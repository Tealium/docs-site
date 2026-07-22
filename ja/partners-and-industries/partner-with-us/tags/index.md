---
title: タグ
description: Tealium Tag Managementでブラウザベースのタグを統合する方法について説明します。
url: https://docs.tealium.com/ja/partners-and-industries/partner-with-us/tags/
---


独自のJavaScriptタグをTealium Tag Marketplaceで提供したい場合や、ユーザーが長いリリースサイクルを待たずに貴社のタグをサイトに追加できるようにしたい場合は、このガイドをお読みください。タグの仕組みと、Tealium Tag Managementとの正式な統合によるメリットについて説明します。

## タグの仕組み

タグマーケットプレイスのタグは、貴社のタグによる機能の完全な統合を提供します。つまり、タグが求めるオプションとトラッキング対象のイベントはすべて、Tealiumユーザーのアカウントで、単一の構成可能なタグインスタンスに統合されます。

### 構成

タグの内部的な動作はほとんどのユーザーからは見えないため、ユーザーはポイントアンドクリック方式のセットアップオプションに集中できます。その一方で、Tealiumユーザーはタグを実行するコードにアクセスし、JavaScriptで快適に操作できます。

タグは次の3か所で管理されます。

* **構成**
タグの構成は、タグのインスタンスごとに1回だけ構成されます。通常、ページごとの違いはありません。
[タグ構成の詳細については、こちらを参照してください](https://community.tealiumiq.com/t5/iQ-Tag-Management/Tags/ta-p/5016)。
* **タグ配信ルール**
タグ配信ルールは、ページまたはイベントにタグを読み込むタイミングを決定します。タグ配信ルールの条件は、データレイヤーの値に基づきます。
[タグ配信ルールの詳細については、こちらを参照してください](https://community.tealiumiq.com/t5/iQ-Tag-Management/Load-Rules/ta-p/5098)。
* **データマッピング**
データマッピングは、データレイヤーのどの動的値がタグに必要で、対応するどの変数名がベンダーによって使用されるかを決定します。また、ページ内イベントのトラッキング方法もマッピングによって決定されます。
[データマッピングの詳細については、こちらを参照してください](https://community.tealiumiq.com/t5/iQ-Tag-Management/Data-Mappings/ta-p/10645)。

### ブラウザへの読み込み

ベンダータグはTealium Universal Tag（utag.js）によって読み込まれます。これは、Tag Managementアカウントからの構成ロジックが含まれるラッパータグです。後続のベンダータグは、非同期のJavaScriptを使用して読み込まれ、タグマネージャの外部での実行時と同じように実行されます。

ベンダーのタグライブラリや画像ピクセルは、ページのDOMに同じように表示されます。Tealiumでは、タグができる限り仕様どおりに読み込まれるように努めています。まれにコードの変更が必要になった場合も、最終的なトラッキングビーコンが要件に適合するよう確認しています。


<blockquote>
Tealiumで同期JavaScriptを読み込み、A/Bテストや多変量テストを行うベンダーをサポートすることもできます。
</blockquote>


### eコマース値

製品データおよび注文データを収集するeコマースタグ用に、TealiumではE-Commerce Extensionという便利な機能を提供しています。これは、すべての標準的なeコマースデータを自動的にタグに統合する機能です。アカウントで構成したE-Commerce Extensionは、eコマース値を必要とするすべてのタグに対するグローバルデータマッピングとしての役割を果たします。これにより、このタイプのタグのセットアップに必要な労力を最小限に抑えることができます。

[E-Commerce Extensionの詳細については、こちらを参照してください](https://community.tealiumiq.com/t5/iQ-Tag-Management/E-commerce-Extension/ta-p/11927)。

## タグの種類

貴社のタグソリューションの実装に加えて、Tealiumはシステムの能力に応じて追加の統合オプションを提供できます。

### 標準

ほとんどすべてのタグで、同じ形式に従って、JavaScriptファイルを読み込み、コードの初期化を行い、ページから動的データを収集して、タグをトリガーしています。この標準フレームワークの適用範囲は、静的パラメータを使用する最も単純な画像ピクセルから、ページのタイプごとに異なるコードを実行してページから動的データを収集する複雑なJavaScriptライブラリにまで及びます。

### Cookie照合

Cookie照合タグの目的は、特殊なリクエストを使用して、Tealiumとシステムの間で訪問IDを同期することです。これにより、システムの一意の訪問IDをTealiumのサーバー側プラットフォームと共有し、Tealiumの訪問IDを受け取ることができます。このタイプの統合は、_標準タグへの追加として_使用されます。

#### 例

次の例は、Cookie照合リクエストを示しています。

```plain
GET https://sync.example-dsp.net/get-userId?
tealium_visitor_id=abxyz0909&
tealium_account=my_account&
tealium_profile=main&
tealium_datasource=abc123
```

このリクエストはブラウザを起点とし、Tealiumの訪問IDをシステムに送信します。結果として、システムの訪問IDとTealiumの訪問IDがTealiumに返されます。これは、Tealiumが照合テーブルをホスティングしていることを示します（推奨）。Tealiumへの最後のリクエストには、Tealiumから提供されたすべての変数と、一致したベンダーのIDが含まれます。

以下は、Tealiumに戻るリダイレクトの例です。

```plain
GET https://collect.tealiumiq.com/vdata?
dsp_uid=4595-23423442&
tealium_visitor_id=abxyz0909&
tealium_account=my_account&
tealium_profile=main&
tealium_datasource=abc123
```

次のCookie照合例では、リダイレクトのリクエストをURLパラメータとして渡しています（DSPのエンドポイントが受け取る場合）。

```plain
GET https://sync.example-dsp.net/get-userId?
redirect=https://collect.tealiumiq.com/vdata?dsp_uid=$UID&tealium_visitor_id=abxyz0909&tealium_account=egbrand&tealium_profile=main&tealium_datasource=abc123
```

### サーバー側有効化

サーバー側有効化タグには、直接Tealium EventStreamとAudienceStreamにイベントを送信するための追加機能が備えられています。たとえば、マウスの動きのトラッキングによりユーザーセンチメントを推測するユーザーエクスペリエンスベンダーは、直接Tealium Collectに対して特定のイベントをトリガーすることができます。このタイプの統合が_標準タグに含まれています_。

次に示す関数の例では、Tealiumイベントエンドポイントにデータを送信します。
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

貴社のテクノロジーを統合する方法については、[お問い合わせください](https://community.tealiumiq.com/t5/Become-a-Technology-Partner/bd-p/become-a-technology-partner) 。

