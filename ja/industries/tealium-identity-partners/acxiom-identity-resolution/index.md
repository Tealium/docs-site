---
title: Acxiom Identity ResolutionのためのTealium Functionsの使用
description: この記事では、訪問関数を使用してAcxiomアイデンティティプロバイダーから確率的アイデンティティデータを取得し、訪問プロファイルに保存する方法について説明します。
url: https://docs.tealium.com/ja/industries/tealium-identity-partners/acxiom-identity-resolution/
---
Acxiomからデータを取得するために訪問関数の使用を推奨します。訪問関数についての詳細は、[イベントと訪問関数](https://docs.tealium.com/ja/server-side/functions/event-visitor-functions/about/)を参照してください。

訪問関数は以下の操作を行います：

*   Acxiomから追加データをリクエストします。
*   追加データと`tealium_visitor_id`を含むイベントをTealium Collectに送信します。

EventStream属性と訪問属性は、関数から送信されたイベントによって豊かにされます。

## 前提条件

*   Tealium EventSteamおよびTealium Functions。
*   データソースとしてのTealium Collect API。
*   追加情報を保存する訪問属性。
*   訪問属性をエンリッチするために必要な属性を持つイベント仕様である`acxiom_function_event`。
*   イベント属性の値に訪問属性を構成するエンリッチメント。

Acxiom Real Tagタグがインストールされている場合、関数は最も効果的に動作します。この識別子は訪問の信頼度を高めます。

## イベントを処理する関数の作成

関数を作成するには：

1.  **Transform > Functions**に移動します。
2.  **Add Function**をクリックします。
3.  関数の名前を入力します。
4.  関数の説明をノートに入力します。
5.  **Processed Event**トリガーを選択します。
6.  トリガーのためのイベントフィードを選択します。
7.  **Continue**をクリックします。
8.  下記のサンプルコードを**Code**ボックスに入力します。
9.  構成に必要に応じてコードをカスタマイズします。
10.  関数を保存します。

**Test**機能とPostman API Workbenchなどのツールを使用して関数をテストできます。

関数の作成に関する詳細は、[Managing Functions](https://docs.tealium.com/ja/server-side/functions/manage-functions/create-function/)を参照してください。

## 例示関数コード

以下に含まれるテスト例関数は、送信された属性に基づいて訪問プロファイルをマッチングしようとします：

| 属性 | 説明 |
| --------- | ----------- |
| `acxiom_function_event` | イベント仕様名 |
| `realId`   | Acxiom rTag |
| `address`  | ユーザーの住所 |
| `phone`    | ユーザーの電話番号 |
| `email`    | ユーザーのメールアドレス |
| `fullName` | ユーザーのフルネーム |

関数はプロファイルエンリッチメントのための追加ユーザーデータを返します。


<blockquote>
このコードは現在ベータ版です。
</blockquote>


```js
// イベントスコープ関数では、event, authなどのモジュールが使用可能です
import { event, store, tealium } from "tealium";
(async () => {
    
    // これらのエンドポイントは、Acxiomとの構成に特有のものです。
    const access_url="https://mydomain.com/metrics/access_token"
    const query_url="https://mydomain.com/metrics"
    const query_name="demo_dsapi_match"

    // イベントオブジェクトで使用可能なものを正確に知るために、これをアンコメントしてください
    //console.log('Data available:\n', JSON.stringify(event, null, 2));

    const data = {};
    data.tealium_account = event?.data?.udo?.tealium_account;
    data.tealium_profile = event?.data?.udo?.tealium_profile;
    data.visitor_id = event?.data?.udo?.visitor_id;
    data.trace_id = event?.data?.firstparty_tealium_cookies?.trace_id;
    data.acxiom_real_id = event?.data?.udo?.acxiom_real_id || "";
    data.customer_email = event?.data?.udo?.customer_email;
    data.customer_first_name = event?.data?.udo?.customer_first_name;
    data.customer_last_name = event?.data?.udo?.customer_last_name;
    data.customer_full_name = `${data.customer_first_name} ${data.customer_last_name}`

    // acxiom_real_idが利用可能かチェックします
    // if (typeof data.acxiom_real_id === "undefined") {
    //     console.error("acxiom_entity_id is unavailable.");
    //     return;
    // }

    // グローバル変数からリフレッシュトークンを取得します
    const refresh_token = store.get("acxiom_refresh_token")
    console.log("refresh_token: ", refresh_token)

    // アクセストークンを生成します
    const access_token_request = await fetch(access_url, {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
            "Authorization": `Bearer ${refresh_token}`
        },
        body: `{"grant_type":"refresh_token","refresh_token":"${refresh_token}"}`
    })
    .catch((error) => {
        console.error('Error:', error);
    });
    const access_token_response = await access_token_request.json();
    // console.log("access_token_response:", JSON.stringify(access_token_response));
    const access_token = access_token_response.jwt_token;
    // console.log("access_token: ", access_token)

    // Acxiom PAILからacxiom_real_idを使用してquery_execution_idを取得します
    const response = await fetch(`${query_url}/named_queries/${query_name}/execute`, {
        method: "POST",
        redirect: "follow",
        headers: {
            "Content-Type": "application/json",
            "Authorization": `Bearer ${access_token}`
        },
        body: `{
            "realID": "${data?.acxiom_real_id}", 
            "address": "${data?.customer_address}", 
            "phone": "${data?.customer_phone}", 
            "email": "${data?.customer_email}", 
            "fullName": "${data?.customer_full_name}"
        }`
    })
    .then(res => {
        console.log("Res: ", JSON.stringify(res))
        return res
    })
    // .then(response => console.log("Response: ", JSON.stringify(response)))
    .catch(error => console.error('Error: ', error.message));
    const body = await response.json();
    const query_execution_id = body.query_execution_id
    
    // console.log("Status: " + response.status);
    console.log("Body: " + JSON.stringify(body, null, 2));

    // Acxiomからの応答データが利用可能かチェックします
    if (!response.ok) {
        console.error("Acxiom response data is unavailable.");
        return;
    }

    // query_execution_idを使用してAcxiom PAILからデータを取得します
    const payload = await fetch(`${query_url}/query_executions/${query_execution_id}`, {
        method: "GET",
        headers: {
            "Content-Type": "application/json",
            "Authorization": `Bearer ${access_token}`
        }
    })
    .then(res => {
        console.log("Res: ", JSON.stringify(res))
        return res
    })
    // .then(response => response.json())
    // .then(response => console.log("Response: ", JSON.stringify(response)))
    .catch(err => console.error(err));

    const user_data = await payload.json();
    console.log("user_data: ", JSON.stringify(user_data))

    let data_object = {};
    for (let i=0; i < user_data.column_info.length; i++) {
        data_object[user_data.column_info[i].name] = user_data.data[0][i]
    }
    // data_object = JSON.stringify(data_object)

    let newEvent = {};
    newEvent = { ...data_object }
    newEvent.tealium_event = "acxiom_function_event";
    newEvent.visitor_id = data.visitor_id;
    newEvent.tealium_trace_id = data?.tealium_trace_id;
    newEvent.customer_email = data_object?.email;
    
    console.log("newEvent: " + JSON.stringify(newEvent, null, 2));

    // Acxiomから受け取ったデータをTealiumに送信します
    tealium
        .sendCollectEvent(newEvent, data.tealium_account, data.tealium_profile)
        .then(response => {
            console.log('Status code: ', response.status);
            return response;
        })
        .then(data => console.log('Result: ', JSON.stringify(data, null, 2)))
        .catch(error => console.error('Error: ', error.message));
})();
```