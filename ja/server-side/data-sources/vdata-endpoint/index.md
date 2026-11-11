---
title: Visitor Data Enrichment（/vdata）を使用したデータのインポート
description: 任意の外部システムからリアルタイムのデータ更新をEvent Streamingに送信します。
url: https://docs.tealium.com/ja/server-side/data-sources/vdata-endpoint/
---## はじめに

Event Streamingにデータを取り込む標準的な方法として、次の2つをご存じの方も多いでしょう。

* [Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)：WebサイトのイベントデータをEvent Streamingに送信する処理を管理します。このタグはTag Management内で構成します。
* [ファイルインポートデータソース](https://docs.tealium.com/about-file-import/)：訪問データをEvent Streamingに一括インポートするプロセスを管理します。

Event Streamingがデータを受信する方法には、3つ目の方法があることをご存じでしょうか。この追加の方法はVisitor Data Enrichmentと呼ばれ、任意の外部システムからリアルタイムのデータ更新をEvent Streamingに送信するために使用できます。以降のセクションでは、詳細と例を説明します。

### /vdata/i.gifとは？

* Tealium Collectエンドポイントの`/vdata/`パスは、通常、従来のトラッキングピクセルで使用される名前と値のペア形式でデータを受信するために使用されます。  
   ```
   //my.domain.com/my.gif?name1=value1&name2=value2
   ```

* `/vdata/ `URLには、特別かつ必須のキーと値（`tealium_`で始まるもの）がありますが、それ以外のものはすべてデータレイヤーの構築に使用されます。  
   ```
   //collect.tealiumiq.com/vdata/i.gif?tealium_account=ACCOUNT&tealium_profile=PROFILE&tealium_vid=ID&name1=value1&name2=value2
   ```

* データ収集を特定のリージョンに限定できます。  
たとえば、ドイツ国内でのみデータを収集するには、`collect-eu-central-1.tealiumiq.com`を使用します。

### 想定されるユースケース

次のリストでは、Visitor Data Enrichmentの想定される用途について説明します。

* Event Streamingを通じてベンダーにデータを送信する  
モバイルアプリでは、Tealiumの`/vdata/i.gif`を使用してWebViewを経由せず、アプリケーションからEvent Streamingに直接データを送信できます。
* Cookie Syncサービスのエンドポイントとして使用する  
これにより、タグベンダーは`/vdata/i.gif`の場所にリダイレクトし、その訪問IDをEvent Streamingに送信できます。
* インプレッショントラッキング  
ディスプレイ広告は通常、iFrame内に読み込まれます。Visitor Data Enrichmentを使用すると、訪問にどの広告が表示されたかを追跡できます。
* CMS、CRM、BIなどのシステムから、データのJSONオブジェクトをEvent StreamingにPOSTする  
システムで生成される機密データをブラウザ経由で送信したくない一方で、訪問に対してアクションを実行するためにEvent Streamingがそのデータをリアルタイムで必要とする場合に、この方法を使用できます。

### Tealium RESTエンドポイントの必須パラメータ

次の表では、Tealium RESTエンドポイントの必須パラメータについて説明します。

|パラメータ|説明|
|---| ---|
|`tealium_account`|Event Streaming／Tag Managementのアカウント名|
|`tealium_profile`|Event Streamingを構成したプロファイル名|
|`tealium_vid`|トラッキングリクエストの送信元を示す、一意の訪問IDまたはセカンダリID（エンコードされたメールアドレスやデバイスIDなど）|
|`tealium_trace_id`|（任意）Trace機能を使用したテストの場合にのみ必須|

## GETリクエストの例

```
GET //collect.tealiumiq.com/vdata/i.gif?tealium_account=ACCOUNT&tealium_profile=PROFILE&tealium_vid=ID&ut.event=view&page_name=product_detail&product_id=sku123456
```

#### メールに埋め込む場合の例

```
<img src="//collect.tealiumiq.com/vdata/i.gif?tealium_account=ACCOUNT&tealium_profile=PROFILE&tealium_vid=ID&ut.event=view&email_id=december2015&content_type=
```

`/vdata/i.gif`の使用はVisitor Data Enrichmentを利用する最も一般的な方法であり、この方法を強く推奨します。サーバーから異なる形式でデータを直接送信する場合、制限や要件が存在する可能性があるため、以降のセクションではそのためのオプションを紹介します。

### JavaScriptを使用したGETリクエストの例

次の例は、インプレッショントラッキング情報をEvent Streamingに送信するようにディスプレイ広告をコーディングする方法を示しています。

```
//build your object of data
var a={
    "data":{
        "event_name":"ad_tracking",
        "ad_image_id":"%%macro_to_get_ADID%%",
        "ad_advertiser_id":"%%macro_to_get_ADVID%%",
        "ad_campaign_id":"%%macro_to_get_CAMPID%%",
        "ad_user_id":"%%macro_to_get_USERID%%"
    },
    "event":"view"
}

//stringify the object for the GET event
var json_string = JSON.stringify(a);

//send the data to your collect endpoint
var img = new Image();
img.src='//collect.tealiumiq.com/account/profile/2/i.gif?data='+encodeURIComponent(json_string);

```

## POSTリクエストの例

POSTリクエストの例はGETリクエストと似ていますが、GETと比較して、POSTでは送信可能なデータ量の制限が少なくなります。

### JavaScriptを使用したPOSTリクエストの例

```
//build your object of data
var a={
   "data":{
      "event_name":"myEvent",
      "customer_id":"user1@tealium.com",
      "cp.trace_id":"12345"
   },
   "event":"view" //change this to "link" or "view" depending on the type of event
}

//stringify the object for the POST event
var json_string = JSON.stringify(a);

//POST the data to your collect endpoint
if (json_string!="") {
   var formData = new FormData();
   formData.append("data", json_string);
   function postData(data) {
      var xhr = new XMLHttpRequest();
      xhr.open('post', "//collect.tealiumiq.com/account/profile/2/i.gif", true);
      xhr.withCredentials = true;
      xhr.send(data);
   }
   postData(formData);
}
```

### cURLを使用したPOSTリクエストの例

次の例は、コマンドラインインターフェイス（CLI）またはMacのターミナルからEvent StreamingにデータをPOSTする方法を示しています。この例は通常、テスト目的でのみ使用されます。

```
curl -H "Content-Type: application/json" -X POST -d '{"data":{"event_name":"myEvent","customer_id":"user1@tealium.com","cp.trace_id":"12345"},"event":"view"}' https://collect.tealiumiq.com/account/profile/2/i.gif
```

### Pythonを使用したPOSTリクエストの例

次の例は、Pythonを使用してプログラムから実行するためのコーディング方法を示しており、[python.org](https://docs.python.org/release/2.6/library/httplib.html)の例に基づいています。

```
import requests, json
body = {'data':{'event_name':'abc_score','cp.trace_id':'04759','abc_score':'0.56','customer_id':'9999999'},'event':'view'}
headers = {"Content-Type": "text/plain","Accept": "image/gif"}
r = requests.post(' https://collect.tealiumiq.com/account/profile/2/i.gif', data = json.dumps(body), headers=headers);
```

この例ではPythonの「Requests」モジュールを使用します。このモジュールは、次のコマンドでインストールできます。

```
pip2 install requests
```

Python 3では、次を使用します。

```
pip3 install requests
```


<blockquote>
完了したら、必要に応じて更新してテストします。
</blockquote>
