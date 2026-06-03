---
title: イベントと訪問の関数の例（V2）
description: この記事では、V2のイベントと訪問の関数の例コードを提供します。
url: https://docs.tealium.com/ja/server-side/functions/event-visitor-functions/function-examples-v2/
---
## HTTP POSTでイベントデータを送信する

以下の例では、イベントデータをリクエストボディのJSONでエンドポイントにHTTP POSTリクエストを行う方法を示しています。

```
// イベントデータを送信 - HTTP POST
import {event} from &#39;tealium&#39;;

console.log(JSON.stringify(event));

fetch(&#39;https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d&#39;,
    {
        method: &#39;POST&#39;,
        body: JSON.stringify(event),
        headers: {
            &#39;Content-Type&#39;: &#39;application/json&#39;
        }
    })
    .then(response =&gt; {
        if (!response.ok) {
            throw new Error(&#39;ネットワークの応答が正常ではありませんでした。ステータスコード：${response.status}。&#39;);
        }
        return response.json();
    })
    .then(data =&gt; console.log(&#39;レスポンス：&#39;, JSON.stringify(data)))
    .catch(error =&gt; console.log(&#39;エラー：&#39;, error.message));
```

## HTTP GETでイベントデータを送信する

以下の例では、イベントデータをクエリ文字列パラメータとしてエンドポイントにHTTP GETリクエストを行う方法を示しています。

```
// イベントデータを送信 - HTTP GET
import {event} from &#39;tealium&#39;;

console.log(JSON.stringify(event));

fetch(encodeURI(&#39;https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d?param=${event.data}&#39;))
    .then(response =&gt; {
        if (!response.ok) {
            throw new Error(&#39;ネットワークの応答が正常ではありませんでした。ステータスコード：${response.status}。&#39;);
        }
        return response.json();
    })
    .then(data =&gt; console.log(&#39;レスポンス：&#39;, JSON.stringify(data)))
    .catch(error =&gt; console.log(&#39;エラー：&#39;, error.message));
```

## HTTP POSTで訪問データを送信する

以下の例では、訪問プロファイルデータをリクエストボディのJSONでエンドポイントにHTTP POSTリクエストを行う方法を示しています。

```
// 訪問データを送信 - HTTP POST
import {visitor} from &#39;tealium&#39;;

console.log(JSON.stringify(visitor));
fetch(&#39;https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d&#39;,
    {
        method: &#39;POST&#39;,
        body: JSON.stringify(visitor), 
        headers: {
            &#39;Content-Type&#39;: &#39;application/json&#39;
        }
    })
    .then(response =&gt; {
        if (!response.ok) {
            throw new Error(&#39;ネットワークの応答が正常ではありませんでした。ステータスコード：${response.status}。&#39;);
        }
        return response.json();
    })
    .then(data =&gt; console.log(&#39;レスポンス：&#39;, JSON.stringify(data)))
    .catch(error =&gt; console.log(&#39;エラー：&#39;, error.message));
```

## HTTP GETで訪問データを送信する

以下の例では、訪問プロファイルデータをクエリ文字列パラメータとしてエンドポイントにHTTP GETリクエストを行う方法を示しています。

```
// 訪問データを送信 - HTTP GET
import {visitor} from &#39;tealium&#39;;

console.log(JSON.stringify(visitor));

fetch(encodeURI(&#39;https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d?param=${visitor.data}&#39;))
    .then(response =&gt; {
        if (!response.ok) {
            throw new Error(&#39;ネットワークの応答が正常ではありませんでした。ステータスコード：${response.status}。&#39;);
        }
        return response.json();
    })
    .then(data =&gt; console.log(&#39;レスポンス：&#39;, JSON.stringify(data)))
    .catch(error =&gt; console.log(&#39;エラー：&#39;, error.message));
```

## 訪問データを取得してTealium Collectに送信する

この例では、関数はIPアドレスを使用して場所の都市を取得し、その都市の天気情報を取得し、都市と天気情報をTealium Collect HTTP APIに送信します。

```
import { auth, visitor, event } from &#34;tealium&#34;;

console.log(JSON.stringify(visitor));

const ip_stack_api_key = &#39;your_api_key&#39;,
      weather_api_key = &#39;your_weather_api_key&#39;,
      ip_address = visitor?.current_visit?.properties?.ip_address;

console.log(ip_address);
(async function() {
    if(ip_address) {
    try {
        // IPアドレスを使用して場所の都市を取得
        let city_response = await fetch(&#39;https://api.ipstack.com/${ip_address}?access_key=${ip_stack_api_key}&amp;format=1&#39;),
        city_data = await city_response.json();
        console.log(JSON.stringify(city_data));
        // 都市を使用して現地の天気を取得
        let weather_response = await fetch(encodeURI(&#39;https://api.openweathermap.org/data/2.5/weather?q=${city_data.city}&amp;appid=${weather_api_key}&#39;)),
            weather_data = await weather_response.json();
            console.log(JSON.stringify(weather_data));
        // 都市と天気の説明をcollectエンドポイントに送信
        await fetch(encodeURI(&#39;https://collect.tealiumiq.com/event?tealium_account=cloud-functions-usecases&amp;tealium_profile=main&amp;tealium_visitor_id=${visitor._id}&amp;lookup_city=${weather_data?.name}&amp;weather=${weather_data?.weather?.[0]?.description}&amp;country=isp=${city_data?.connection?.isp}&#39;));
    } catch(e) {
        console.error(e);
        return false;
    }
    } else {
        console.error(&#34;ユーザーのIPアドレスを特定できませんでした&#34;)
    }
})();
```

## Facebookの認証トークンを取得する

以下のコード例は、Facebookの認証トークンを取得する方法を示しています。

```
import { auth } from &#39;tealium&#39;;
const token = auth.get(&#39;facebook_token&#39;);

fetch(&#39;https://graph.facebook.com/v8.0/act_12345678/customaudiences??access_token=${token}&amp;fields=approximate_count%2Csubtype%2Cname%2Cdata_source&amp;limit=10&#39;)
  .then(response =&gt; response.json())
  .then(data =&gt; console.log(&#39;データ：&#39;, data))
  .catch(error =&gt; console.log(&#39;エラー：&#39;, error.message));
```

### Facebookにデータを送信する

この例では、イベントデータをFacebook GraphまたはMarketing APIに送信してキャンペーンを作成する方法を示しています。Facebookキャンペーンの詳細については、[https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group).](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)を参照してください。

```
import {auth, event} from &#39;tealium&#39;;

const ACT_ID = 11111111111;
const ACCESS_TOKEN = auth.get(&#34;facebook_token&#34;);

fetch(&#39;https://graph.facebook.com/v8.0/act_${ACT_ID}/campaigns?access_token=${ACCESS_TOKEN}&#39;,
    {
        method: &#39;POST&#39;,
        body: &#39;name=${event.data}&amp;objective=PAGE_LIKES&amp;status=PAUSED&amp;special_ad_categories=[]&#39;
    })
    .then(response =&gt; {
            if (!response.ok) {
                throw new Error(&#39;ネットワークの応答が正常ではありませんでした。ステータスコード：${response.status}。&#39;);
            }
            return response.json();
        })
    .then(data =&gt; console.log(&#39;レスポンス：&#39;, JSON.stringify(data)))
    .catch(error =&gt; console.log(&#39;エラー：&#39;, error.message));
```

## Facebookキャンペーンを作成する

この例では、Facebookキャンペーンを作成する方法を示しています。

```
import { auth } from &#34;tealium&#34;;

const ACT_ID = 11111111111;
const ACCESS_TOKEN = auth.get(&#34;facebook_token&#34;);

(async function () {
    console.time(&#39;function&#39;);
    try {
        console.log(&#39;キャンペーンを作成中...&#39;);
        let campaignId = await createCampaign({ campaignName: &#39;My Campaign&#39; });
        console.log(&#39;キャンペーンID&#39;, campaignId);

        console.log(&#39;カスタムオーディエンスを作成中...&#39;);
        let customAudienceId = await createCustomAudience({ caName: &#39;My_Audience&#39; });
        console.log(&#39;カスタムオーディエンスID&#39;, customAudienceId);

        console.log(&#39;広告セットを作成中...&#39;);
        customAudienceId = 23846304008770411;
        let adSetId = await createAdSet({ campaignId: campaignId, customAudienceId: customAudienceId });
        console.log(&#39;広告セットID&#39;, adSetId);

        console.log(&#39;広告クリエイティブを作成中...&#39;);
        // let adCreativeId = await createAdCreative();
        // 現在のAPI呼び出しは機能していないため、事前に手動で作成したIDを使用します
        let adCreativeId = &#39;adCreativeId&#39;;
        console.log(&#39;広告クリエイティブID &#39;, adCreativeId);

        console.log(&#39;広告を作成中...&#39;);
        let adId = await createAd({ adsetId: adSetId, adCreativeId: adCreativeId });
        console.log(&#39;広告ID&#39;, adId);
        console.timeEnd(&#39;function&#39;);
    } catch (error) {
        console.log(error);
    }
})();

async function createAd({ adsetId, adCreativeId }) {
    const params = {
        &#39;status&#39;: &#39;PAUSED&#39;,
        &#39;adset_id&#39;: adsetId,
        &#39;name&#39;: &#39;My Ad&#39;,
        &#39;creative&#39;: { &#39;creative_id&#39;: adCreativeId },
    };

    let result = await fetch(&#39;https://graph.facebook.com/v7.0/act_${ACT_ID}/ads?access_token=${ACCESS_TOKEN}&#39;,
        {
            method: &#39;POST&#39;,
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

async function createAdSet({ campaignId, customAudienceId }) {
    const params = {
        &#39;name&#39;: &#39;AdSet&#39;,
        &#39;lifetime_budget&#39;: &#39;1000&#39;,
        &#39;start_time&#39;: &#39;2020-07-01T23:41:41-0800&#39;,
        &#39;end_time&#39;: &#39;2020-07-07T23:41:41-0800&#39;,
        &#39;campaign_id&#39;: campaignId,
        &#39;bid_amount&#39;: &#39;1&#39;,
        &#39;billing_event&#39;: &#39;IMPRESSIONS&#39;,
        &#39;optimization_goal&#39;: &#39;LINK_CLICKS&#39;,
        &#39;targeting&#39;: {
            &#34;geo_locations&#34;: {
                &#34;countries&#34;: [&#34;US&#34;],
            },
            &#34;age_min&#34;: 25,
            &#34;age_max&#34;: 40,
            &#34;custom_audiences&#34;: [{ &#34;id&#34;: customAudienceId }]
        },
        &#39;status&#39;: &#39;PAUSED&#39;
    };
    let result = await fetch(&#39;https://graph.facebook.com/v7.0/act_${ACT_ID}/adsets?access_token=${ACCESS_TOKEN}&#39;,
        {
            method: &#39;POST&#39;,
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

async function createCustomAudience({ caName }) {
    const params = {
        &#39;name&#39;: caName,
        &#39;subtype&#39;: &#39;CUSTOM&#39;,
        &#39;description&#39;: &#39;People who purchased on my website&#39;,
        &#39;customer_file_source&#39;: &#39;USER_PROVIDED_ONLY&#39;,
    };
    let result = await fetch(&#39;https://graph.facebook.com/v7.0/act_${ACT_ID}/customaudiences?access_token=${ACCESS_TOKEN}&#39;,
        {
            method: &#39;POST&#39;,
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

async function createCampaign({ campaignName }) {
    const params = {
        &#39;objective&#39;: &#39;LINK_CLICKS&#39;,
        &#39;status&#39;: &#39;PAUSED&#39;,
        &#39;buying_type&#39;: &#39;AUCTION&#39;,
        &#39;name&#39;: campaignName,
        &#39;special_ad_categories&#39;: &#39;NONE&#39;
    };
    let result = await fetch(&#39;https://graph.facebook.com/v8.0/act_${ACT_ID}/campaigns?access_token=${ACCESS_TOKEN}&#39;,
        {
            method: &#39;POST&#39;,
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

function jsonToRequestBodyString(json) {
    return Object.keys(json).map(function (key) {
        return encodeURIComponent(key) &#43; &#39;=&#39; &#43;
            ((typeof json[key] === &#39;string&#39; || json[key] instanceof String) ? encodeURIComponent(json[key]) : JSON.stringify(json[key]));
    }).join(&#39;&amp;&#39;);
}
```