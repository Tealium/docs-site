---
title: ビジターデータエンリッチメント(/vdata)を使用したデータのインポート
description: 任意の外部システムからEventStreamにリアルタイムでデータ更新を送信します。
url: https://docs.tealium.com/ja/server-side/data-sources/vdata-endpoint/
---## はじめに

EventStreamにデータを取り込むための以下の2つの標準的な方法については、おそらくご存知でしょう：

* Tealium iQ内で構成された、ウェブサイトのイベントデータをEventStreamにトリガーする[Tealium Collectタグ]()。
* EventStreamにビジターデータを一括でインポートするプロセスを管理する[File Import Data Source]()。

EventStreamがデータを受け取るための第3の方法があることをご存知でしたか？この追加の方法はビジターデータエンリッチメントと呼ばれ、任意の外部システムからEventStreamにリアルタイムでデータ更新を送信するために使用できます。以下のセクションでは詳細と例を提供します。

### /vdata/i.gifとは何ですか？

* Tealium Collectエンドポイントの`/vdata/`パスは、通常、トラッキングピクセルに伝統的な名前/値のペア形式でデータを受け取るために使用されます。  
   ```
   //my.domain.com/my.gif?name1=value1&amp;name2=value2
   ```

* `/vdata/`URLには、特別で必須のキー値（`tealium_`で始まるもの）がありますが、それ以外のものはすべてデータレイヤーを構築するために使用されます  
   ```
   //collect.tealiumiq.com/vdata/i.gif?tealium_account=ACCOUNT&amp;tealium_profile=PROFILE&amp;tealium_vid=ID&amp;name1=value1&amp;name2=value2
   ```

* データ収集は特定の地域に限定できます。  
例えば、ドイツでのデータ収集のみにする場合は、`collect-eu-central-1.tealiumiq.com`を使用します

### ポテンシャルな使用ケース

以下のリストは、ビジターデータエンリッチメントの潜在的な使用例を説明しています。

* EventStream経由でベンダーにデータを送信する  
モバイルアプリは、アプリケーションから直接データをEventStreamにトリガーし、webviewをスキップする能力を持っています。これはTealiumの`/vdata/i.gif`を使用します。
* クッキーシンクサービスのエンドポイントとして使用する  
これにより、タグベンダーは`/vdata/i.gif`の場所にリダイレクトし、自分のビジターIDをEventStreamに送信することができます
* インプレッショントラッキング  
ディスプレイ広告は通常、iFrame内にロードされます。ビジターデータエンリッチメントは、どの広告がビジターに表示されたかを追跡するのに役立ちます。
* CMS/CRM/BIなどのシステムがJSONオブジェクトのデータをEventStreamにPOSTする  
この方法は、ブラウザを通じて送信したくない機密データをシステムが生成する場合、またはEventStreamがリアルタイムでビジターに対するアクションを取るためにデータが必要な場合に使用できます。

### Tealium RESTエンドポイントの必須パラメーター

以下の表は、Tealium RESTエンドポイントの必須パラメーターを説明しています：

|パラメーター| 説明|
|---| ---|
|`tealium_account`| EventStream/Tealium iQのアカウント名|
|`tealium_profile`| EventStreamが構成されているプロファイル名|
|`tealium_vid`| トラッキングリクエストが発生するユニークなビジターIDまたはセカンダリID（エンコードされたメールアドレスやデバイスIDなど）|
|`tealium_trace_id`| 任意。Trace機能でテストする場合のみ必要|

## サンプルGETリクエスト

```
GET //collect.tealiumiq.com/vdata/i.gif?tealium_account=ACCOUNT&amp;tealium_profile=PROFILE&amp;tealium_vid=ID&amp;ut.event=view&amp;page_name=product_detail&amp;product_id=sku123456
```

#### これがメールに埋め込まれているとどのように見えるか

```
&lt;img src=&#34;//collect.tealiumiq.com/vdata/i.gif?tealium_account=ACCOUNT&amp;tealium_profile=PROFILE&amp;tealium_vid=ID&amp;ut.event=view&amp;email_id=december2015&amp;content_type=
```

`/vdata/i.gif`の使用は、ビジターデータエンリッチメントを使用する最も一般的な方法であり、強く推奨します。サーバーから直接データを異なる形式で送信する際の制限や要件がある場合、以下のセクションでその方法を提供します。

### JavaScriptを使用したサンプルGETリクエスト

以下の例は、表示広告をコーディングして、インプレッショントラッキング情報をEventStreamに送信する方法を示しています。

```
//データのオブジェクトを作成します
var a={
    &#34;data&#34;:{
        &#34;event_name&#34;:&#34;ad_tracking&#34;,
        &#34;ad_image_id&#34;:&#34;%%macro_to_get_ADID%%&#34;,
        &#34;ad_advertiser_id&#34;:&#34;%%macro_to_get_ADVID%%&#34;,
        &#34;ad_campaign_id&#34;:&#34;%%macro_to_get_CAMPID%%&#34;,
        &#34;ad_user_id&#34;:&#34;%%macro_to_get_USERID%%&#34;
    },
    &#34;event&#34;:&#34;view&#34;
}

//GETイベントのためにオブジェクトを文字列化します
var json_string = JSON.stringify(a);

//データをcollectエンドポイントに送信します
var img = new Image();
img.src=&#39;//collect.tealiumiq.com/account/profile/2/i.gif?data=&#39;&#43;encodeURIComponent(json_string);

```

## サンプルPOSTリクエスト

POSTリクエストの例はGETと似ていますが、POSTでのデータの送信は、送信できるデータの量に関してGETと比較して制限が少ないという点が異なります。

### JavaScriptを使用したサンプルPOSTリクエスト

```
//データのオブジェクトを作成します
var a={
   &#34;data&#34;:{
      &#34;event_name&#34;:&#34;myEvent&#34;,
      &#34;customer_id&#34;:&#34;user1@tealium.com&#34;,
      &#34;cp.trace_id&#34;:&#34;12345&#34;
   },
   &#34;event&#34;:&#34;view&#34; //イベントのタイプに応じてこれを&#34;link&#34;または&#34;view&#34;に変更します
}

//POSTイベントのためにオブジェクトを文字列化します
var json_string = JSON.stringify(a);

//データをcollectエンドポイントにPOSTします
if (json_string!=&#34;&#34;) {
   var formData = new FormData();
   formData.append(&#34;data&#34;, json_string);
   function postData(data) {
      var xhr = new XMLHttpRequest();
      xhr.open(&#39;post&#39;, &#34;//collect.tealiumiq.com/account/profile/2/i.gif&#34;, true);
      xhr.withCredentials = true;
      xhr.send(data);
   }
   postData(formData);
}
```

### cURLを使用したサンプルPOSTリクエスト

以下の例は、Command Line Interface（CLI）またはMacのターミナルからEventStreamにデータをPOSTする方法を示しています。この例は、おそらくテストのためだけに使用されるでしょう。

```
curl -H &#34;Content-Type: application/json&#34; -X POST -d &#39;{&#34;data&#34;:{&#34;event_name&#34;:&#34;myEvent&#34;,&#34;customer_id&#34;:&#34;user1@tealium.com&#34;,&#34;cp.trace_id&#34;:&#34;12345&#34;},&#34;event&#34;:&#34;view&#34;}&#39; https://collect.tealiumiq.com/account/profile/2/i.gif
```

### Pythonを使用したサンプルPOSTリクエスト

以下の例は、Pythonを使用してこれをプログラム的にコーディングして実行する方法を示しており、[python.org](https://docs.python.org/release/2.6/library/httplib.html)の例に基づいています。

```
import requests, json
body = {&#39;data&#39;:{&#39;event_name&#39;:&#39;abc_score&#39;,&#39;cp.trace_id&#39;:&#39;04759&#39;,&#39;abc_score&#39;:&#39;0.56&#39;,&#39;customer_id&#39;:&#39;9999999&#39;},&#39;event&#39;:&#39;view&#39;}
headers = {&#34;Content-Type&#34;: &#34;text/plain&#34;,&#34;Accept&#34;: &#34;image/gif&#34;}
r = requests.post(&#39; https://collect.tealiumiq.com/account/profile/2/i.gif&#39;, data = json.dumps(body), headers=headers);
```

この例ではPythonの&#34;Requests&#34;モジュールを使用しています。これは以下のコマンドを使用してインストールできます：

```
pip2 install requests
```

Python3の場合は：

```
pip3 install requests
```

を使用します。

完了したら、更新して適切にテストしてください。

