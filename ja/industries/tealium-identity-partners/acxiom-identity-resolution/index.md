---
title: Acxiom Identity ResolutionのためのTealium Functionsの使用
description: この記事では、Acxiom identityプロバイダから確率的なアイデンティティデータを取得し、訪問プロファイルに保存するための訪問関数の使用方法について説明します。
url: https://docs.tealium.com/ja/industries/tealium-identity-partners/acxiom-identity-resolution/
---
Acxiomからのデータを取得するために、訪問関数の使用を推奨します。訪問関数についての詳細は、[Event and Visitor Functions](/ja/server-side/functions/event-visitor-functions/about/)を参照してください。

訪問関数は以下のことを行います：

*   Acxiomから追加のデータをリクエストします。
*   追加のデータと`tealium_visitor_id`を含むイベントをTealium Collectに送信します。

関数から送信されたイベントによって、EventStreamの属性と訪問の属性が豊かになります。

## 前提条件

*   Tealium EventSteamとTealium Functions。
*   データソースとしてのTealium Collect API。
*   追加情報を保存するための訪問の属性。
*   訪問の属性をエンリッチするために必要な属性を持つ`acxiom_function_event`というタイトルのイベント仕様。
*   イベント属性の値に訪問の属性を構成するためのエンリッチメント。

Acxiom Real Tagタグがインストールされていると、この関数は最も効果的に動作します。この識別子は、訪問の信頼度を高めます。

## イベントを処理するための関数の作成

関数を作成するには：

1.  **Functions**に移動します。
2.  **Add Function**をクリックします。
3.  関数の名前を入力します。
4.  関数の説明を記入します。
5.  **Processed Event**トリガーを選択します。
6.  トリガーのイベントフィードを選択します。
7.  **Continue**をクリックします。
8.  下記のサンプルコードを**Code**ボックスに入力します。
9.  必要に応じてコードをカスタマイズします。
10.  関数を保存します。

**Test**機能とPostman API Workbenchなどのツールを使用して、関数をテストすることができます。

関数の作成についての詳細は、[Managing Functions](/ja/server-side/functions/manage-functions/create-function/)を参照してください。

## 例の関数コード

以下に示すテスト例の関数は、送信した属性に基づいて訪問プロファイルをマッチングしようとします：

| 属性 | 説明 |
| --------- | ----------- |
| `acxiom_function_event` | イベント仕様の名前 |
| `realId`   | Acxiom rTag |
| `address`  | ユーザーの住所 |
| `phone`    | ユーザーの電話番号 |
| `email`    | ユーザーのメールアドレス |
| `fullName` | ユーザーのフルネーム |

関数は、プロファイルの豊かさを増すための追加のユーザーデータを返します。

このコードは現在ベータ版です。

```js
// イベントスコープの関数では、以下のモジュールが使用可能です: event, auth
import { event, store, tealium } from &#34;tealium&#34;;
(async () =&gt; {
    
    // これらのエンドポイントは、Acxiomとのセットアップに特有のものです。
    const access_url=&#34;https://mydomain.com/metrics/access_token&#34;
    const query_url=&#34;https://mydomain.com/metrics&#34;
    const query_name=&#34;demo_dsapi_match&#34;

    // このコメントを外すと、イベントオブジェクトで何が使用可能かを正確に知ることができます
    //console.log(&#39;Data available:\n&#39;, JSON.stringify(event, null, 2));

    const data = {};
    data.tealium_account = event?.data?.udo?.tealium_account;
    data.tealium_profile = event?.data?.udo?.tealium_profile;
    data.visitor_id = event?.data?.udo?.visitor_id;
    data.trace_id = event?.data?.firstparty_tealium_cookies?.trace_id;
    data.acxiom_real_id = event?.data?.udo?.acxiom_real_id || &#34;&#34;;
    data.customer_email = event?.data?.udo?.customer_email;
    data.customer_first_name = event?.data?.udo?.customer_first_name;
    data.customer_last_name = event?.data?.udo?.customer_last_name;
    data.customer_full_name = `${data.customer_first_name} ${data.customer_last_name}`

    // acxiom_real_idが利用可能かどうかを確認します
    // if (typeof data.acxiom_real_id === &#34;undefined&#34;) {
    //     console.error(&#34;acxiom_entity_id is unavailable.&#34;);
    //     return;
    // }

    // グローバル変数からリフレッシュトークンを取得します
    const refresh_token = store.get(&#34;acxiom_refresh_token&#34;)
    console.log(&#34;refresh_token: &#34;, refresh_token)

    // アクセストークンを生成します
    const access_token_request = await fetch(access_url, {
        method: &#34;POST&#34;,
        headers: {
            &#34;Content-Type&#34;: &#34;application/json&#34;,
            &#34;Authorization&#34;: `Bearer ${refresh_token}`
        },
        body: `{&#34;grant_type&#34;:&#34;refresh_token&#34;,&#34;refresh_token&#34;:&#34;${refresh_token}&#34;}`
    })
    .catch((error) =&gt; {
        console.error(&#39;Error:&#39;, error);
    });
    const access_token_response = await access_token_request.json();
    // console.log(&#34;access_token_response:&#34;, JSON.stringify(access_token_response));
    const access_token = access_token_response.jwt_token;
    // console.log(&#34;access_token: &#34;, access_token)

    // Acxiom PAILからacxiom_real_idを使用してquery_execution_idを取得します
    const response = await fetch(`${query_url}/named_queries/${query_name}/execute`, {
        method: &#34;POST&#34;,
        redirect: &#34;follow&#34;,
        headers: {
            &#34;Content-Type&#34;: &#34;application/json&#34;,
            &#34;Authorization&#34;: `Bearer ${access_token}`
        },
        body: `{
            &#34;realID&#34;: &#34;${data?.acxiom_real_id}&#34;, 
            &#34;address&#34;: &#34;${data?.customer_address}&#34;, 
            &#34;phone&#34;: &#34;${data?.customer_phone}&#34;, 
            &#34;email&#34;: &#34;${data?.customer_email}&#34;, 
            &#34;fullName&#34;: &#34;${data?.customer_full_name}&#34;
        }`
    })
    .then(res =&gt; {
        console.log(&#34;Res: &#34;, JSON.stringify(res))
        return res
    })
    // .then(response =&gt; console.log(&#34;Response: &#34;, JSON.stringify(response)))
    .catch(error =&gt; console.error(&#39;Error: &#39;, error.message));
    const body = await response.json();
    const query_execution_id = body.query_execution_id
    
    // console.log(&#34;Status: &#34; &#43; response.status);
    console.log(&#34;Body: &#34; &#43; JSON.stringify(body, null, 2));

    // Acxiomからのレスポンスデータが利用可能かどうかを確認します
    if (!response.ok) {
        console.error(&#34;Acxiom response data is unavailable.&#34;);
        return;
    }

    // query_execution_idを使用してAcxiom PAILからデータを取得します
    const payload = await fetch(`${query_url}/query_executions/${query_execution_id}`, {
        method: &#34;GET&#34;,
        headers: {
            &#34;Content-Type&#34;: &#34;application/json&#34;,
            &#34;Authorization&#34;: `Bearer ${access_token}`
        }
    })
    .then(res =&gt; {
        console.log(&#34;Res: &#34;, JSON.stringify(res))
        return res
    })
    // .then(response =&gt; response.json())
    // .then(response =&gt; console.log(&#34;Response: &#34;, JSON.stringify(response)))
    .catch(err =&gt; console.error(err));

    const user_data = await payload.json();
    console.log(&#34;user_data: &#34;, JSON.stringify(user_data))

    let data_object = {};
    for (let i=0; i &lt; user_data.column_info.length; i&#43;&#43;) {
        data_object[user_data.column_info[i].name] = user_data.data[0][i]
    }
    // data_object = JSON.stringify(data_object)

    let newEvent = {};
    newEvent = { ...data_object }
    newEvent.tealium_event = &#34;acxiom_function_event&#34;;
    newEvent.visitor_id = data.visitor_id;
    newEvent.tealium_trace_id = data?.tealium_trace_id;
    newEvent.customer_email = data_object?.email;
    
    console.log(&#34;newEvent: &#34; &#43; JSON.stringify(newEvent, null, 2));

    // Acxiomから受け取ったデータをTealiumに送信します
    tealium
        .sendCollectEvent(newEvent, data.tealium_account, data.tealium_profile)
        .then(response =&gt; {
            console.log(&#39;Status code: &#39;, response.status);
            return response;
        })
        .then(data =&gt; console.log(&#39;Result: &#39;, JSON.stringify(data, null, 2)))
        .catch(error =&gt; console.error(&#39;Error: &#39;, error.message));
})();
```
