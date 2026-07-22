---
title: イベントと訪問の関数の例（V2）
description: この記事では、V2のイベントと訪問の関数の例コードを提供します。
url: https://docs.tealium.com/ja/server-side/functions/event-visitor-functions/function-examples-v2/
---
## HTTP POSTでイベントデータを送信する

以下の例では、イベントデータをリクエストボディのJSONでエンドポイントにHTTP POSTリクエストを行う方法を示しています。

```
// イベントデータを送信 - HTTP POST
import {event} from 'tealium';

console.log(JSON.stringify(event));

fetch('https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d',
    {
        method: 'POST',
        body: JSON.stringify(event),
        headers: {
            'Content-Type': 'application/json'
        }
    })
    .then(response => {
        if (!response.ok) {
            throw new Error('ネットワークの応答が正常ではありませんでした。ステータスコード：${response.status}。');
        }
        return response.json();
    })
    .then(data => console.log('レスポンス：', JSON.stringify(data)))
    .catch(error => console.log('エラー：', error.message));
```

## HTTP GETでイベントデータを送信する

以下の例では、イベントデータをクエリ文字列パラメータとしてエンドポイントにHTTP GETリクエストを行う方法を示しています。

```
// イベントデータを送信 - HTTP GET
import {event} from 'tealium';

console.log(JSON.stringify(event));

fetch(encodeURI('https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d?param=${event.data}'))
    .then(response => {
        if (!response.ok) {
            throw new Error('ネットワークの応答が正常ではありませんでした。ステータスコード：${response.status}。');
        }
        return response.json();
    })
    .then(data => console.log('レスポンス：', JSON.stringify(data)))
    .catch(error => console.log('エラー：', error.message));
```

## HTTP POSTで訪問データを送信する

以下の例では、訪問プロファイルデータをリクエストボディのJSONでエンドポイントにHTTP POSTリクエストを行う方法を示しています。

```
// 訪問データを送信 - HTTP POST
import {visitor} from 'tealium';

console.log(JSON.stringify(visitor));
fetch('https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d',
    {
        method: 'POST',
        body: JSON.stringify(visitor), 
        headers: {
            'Content-Type': 'application/json'
        }
    })
    .then(response => {
        if (!response.ok) {
            throw new Error('ネットワークの応答が正常ではありませんでした。ステータスコード：${response.status}。');
        }
        return response.json();
    })
    .then(data => console.log('レスポンス：', JSON.stringify(data)))
    .catch(error => console.log('エラー：', error.message));
```

## HTTP GETで訪問データを送信する

以下の例では、訪問プロファイルデータをクエリ文字列パラメータとしてエンドポイントにHTTP GETリクエストを行う方法を示しています。

```
// 訪問データを送信 - HTTP GET
import {visitor} from 'tealium';

console.log(JSON.stringify(visitor));

fetch(encodeURI('https://webhook.site/87bb160f-475a-4258-b117-693bb2378a4d?param=${visitor.data}'))
    .then(response => {
        if (!response.ok) {
            throw new Error('ネットワークの応答が正常ではありませんでした。ステータスコード：${response.status}。');
        }
        return response.json();
    })
    .then(data => console.log('レスポンス：', JSON.stringify(data)))
    .catch(error => console.log('エラー：', error.message));
```

## 訪問データを取得してTealium Collectに送信する

この例では、関数はIPアドレスを使用して場所の都市を取得し、その都市の天気情報を取得し、都市と天気情報をTealium Collect HTTP APIに送信します。

```
import { auth, visitor, event } from "tealium";

console.log(JSON.stringify(visitor));

const ip_stack_api_key = 'your_api_key',
      weather_api_key = 'your_weather_api_key',
      ip_address = visitor?.current_visit?.properties?.ip_address;

console.log(ip_address);
(async function() {
    if(ip_address) {
    try {
        // IPアドレスを使用して場所の都市を取得
        let city_response = await fetch('https://api.ipstack.com/${ip_address}?access_key=${ip_stack_api_key}&format=1'),
        city_data = await city_response.json();
        console.log(JSON.stringify(city_data));
        // 都市を使用して現地の天気を取得
        let weather_response = await fetch(encodeURI('https://api.openweathermap.org/data/2.5/weather?q=${city_data.city}&appid=${weather_api_key}')),
            weather_data = await weather_response.json();
            console.log(JSON.stringify(weather_data));
        // 都市と天気の説明をcollectエンドポイントに送信
        await fetch(encodeURI('https://collect.tealiumiq.com/event?tealium_account=cloud-functions-usecases&tealium_profile=main&tealium_visitor_id=${visitor._id}&lookup_city=${weather_data?.name}&weather=${weather_data?.weather?.[0]?.description}&country=isp=${city_data?.connection?.isp}'));
    } catch(e) {
        console.error(e);
        return false;
    }
    } else {
        console.error("ユーザーのIPアドレスを特定できませんでした")
    }
})();
```

## Facebookの認証トークンを取得する

以下のコード例は、Facebookの認証トークンを取得する方法を示しています。

```
import { auth } from 'tealium';
const token = auth.get('facebook_token');

fetch('https://graph.facebook.com/v8.0/act_12345678/customaudiences??access_token=${token}&fields=approximate_count%2Csubtype%2Cname%2Cdata_source&limit=10')
  .then(response => response.json())
  .then(data => console.log('データ：', data))
  .catch(error => console.log('エラー：', error.message));
```

### Facebookにデータを送信する

この例では、イベントデータをFacebook GraphまたはMarketing APIに送信してキャンペーンを作成する方法を示しています。Facebookキャンペーンの詳細については、[https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group).](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)を参照してください。

```
import {auth, event} from 'tealium';

const ACT_ID = 11111111111;
const ACCESS_TOKEN = auth.get("facebook_token");

fetch('https://graph.facebook.com/v8.0/act_${ACT_ID}/campaigns?access_token=${ACCESS_TOKEN}',
    {
        method: 'POST',
        body: 'name=${event.data}&objective=PAGE_LIKES&status=PAUSED&special_ad_categories=[]'
    })
    .then(response => {
            if (!response.ok) {
                throw new Error('ネットワークの応答が正常ではありませんでした。ステータスコード：${response.status}。');
            }
            return response.json();
        })
    .then(data => console.log('レスポンス：', JSON.stringify(data)))
    .catch(error => console.log('エラー：', error.message));
```

## Facebookキャンペーンを作成する

この例では、Facebookキャンペーンを作成する方法を示しています。

```
import { auth } from "tealium";

const ACT_ID = 11111111111;
const ACCESS_TOKEN = auth.get("facebook_token");

(async function () {
    console.time('function');
    try {
        console.log('キャンペーンを作成中...');
        let campaignId = await createCampaign({ campaignName: 'My Campaign' });
        console.log('キャンペーンID', campaignId);

        console.log('カスタムオーディエンスを作成中...');
        let customAudienceId = await createCustomAudience({ caName: 'My_Audience' });
        console.log('カスタムオーディエンスID', customAudienceId);

        console.log('広告セットを作成中...');
        customAudienceId = 23846304008770411;
        let adSetId = await createAdSet({ campaignId: campaignId, customAudienceId: customAudienceId });
        console.log('広告セットID', adSetId);

        console.log('広告クリエイティブを作成中...');
        // let adCreativeId = await createAdCreative();
        // 現在のAPI呼び出しは機能していないため、事前に手動で作成したIDを使用します
        let adCreativeId = 'adCreativeId';
        console.log('広告クリエイティブID ', adCreativeId);

        console.log('広告を作成中...');
        let adId = await createAd({ adsetId: adSetId, adCreativeId: adCreativeId });
        console.log('広告ID', adId);
        console.timeEnd('function');
    } catch (error) {
        console.log(error);
    }
})();

async function createAd({ adsetId, adCreativeId }) {
    const params = {
        'status': 'PAUSED',
        'adset_id': adsetId,
        'name': 'My Ad',
        'creative': { 'creative_id': adCreativeId },
    };

    let result = await fetch('https://graph.facebook.com/v7.0/act_${ACT_ID}/ads?access_token=${ACCESS_TOKEN}',
        {
            method: 'POST',
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

async function createAdSet({ campaignId, customAudienceId }) {
    const params = {
        'name': 'AdSet',
        'lifetime_budget': '1000',
        'start_time': '2020-07-01T23:41:41-0800',
        'end_time': '2020-07-07T23:41:41-0800',
        'campaign_id': campaignId,
        'bid_amount': '1',
        'billing_event': 'IMPRESSIONS',
        'optimization_goal': 'LINK_CLICKS',
        'targeting': {
            "geo_locations": {
                "countries": ["US"],
            },
            "age_min": 25,
            "age_max": 40,
            "custom_audiences": [{ "id": customAudienceId }]
        },
        'status': 'PAUSED'
    };
    let result = await fetch('https://graph.facebook.com/v7.0/act_${ACT_ID}/adsets?access_token=${ACCESS_TOKEN}',
        {
            method: 'POST',
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

async function createCustomAudience({ caName }) {
    const params = {
        'name': caName,
        'subtype': 'CUSTOM',
        'description': 'People who purchased on my website',
        'customer_file_source': 'USER_PROVIDED_ONLY',
    };
    let result = await fetch('https://graph.facebook.com/v7.0/act_${ACT_ID}/customaudiences?access_token=${ACCESS_TOKEN}',
        {
            method: 'POST',
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

async function createCampaign({ campaignName }) {
    const params = {
        'objective': 'LINK_CLICKS',
        'status': 'PAUSED',
        'buying_type': 'AUCTION',
        'name': campaignName,
        'special_ad_categories': 'NONE'
    };
    let result = await fetch('https://graph.facebook.com/v8.0/act_${ACT_ID}/campaigns?access_token=${ACCESS_TOKEN}',
        {
            method: 'POST',
            body: jsonToRequestBodyString(params)
        });
    let json = await result.json();
    return json.id;
}

function jsonToRequestBodyString(json) {
    return Object.keys(json).map(function (key) {
        return encodeURIComponent(key) + '=' +
            ((typeof json[key] === 'string' || json[key] instanceof String) ? encodeURIComponent(json[key]) : JSON.stringify(json[key]));
    }).join('&');
}
```