---
title: Context API とタグ管理の実装例ガイド
description: Context API をタグ管理環境に統合するソリューション例を紹介します。
url: https://docs.tealium.com/ja/server-side/context-api/iq-implementation-example/
---
## 仕組み

Context API は、Web サイトやアプリケーションに統合できる一意のエンドポイントを作成します。

[タグ管理の Advanced JavaScript Code 拡張機能](https://docs.tealium.com/advanced-javascript-code-extension/)を使用して Context API を Tealium ワークフローに実装するには、以下の手順を実行します。次の例では、Fetch API を使用して Context API から訪問のデータをリクエストしていますが、`XMLHttpRequest` など、その他の JavaScript オプションもサポートされています。

## 手順 1：訪問 ID を取得する

Tealium の `utag_main` Cookie から `v_id` を解析します。

使用している `utag.js` のバージョンに応じて、以下のコードを拡張機能にコピーします。

* **タイトル**：utag.js Cookie から識別子を解析 [Context API]
* **スコープ**：Pre Loader
* **タイプ**：Advanced JavaScript

### `utag.js` 4.50 以降


<blockquote>
If you use the `split_cookie=false` option, use the [`utag.js` 4.49 and below](#utag-js-4-49-and-below) code examples.
</blockquote>


```js
read_utag_cookies = function() {
  if(!document.cookie || document.cookie === "") {
    return {};
  }
  var cookies = document.cookie.split("; ");
  return cookies.reduce(function(result, cookie) {
    var kv = cookie.split("=");
    if(kv[0].startsWith("utag_")) {
      var cookie_name = kv[0].split("_")[1];
      var cookie_name_with_tag = "utag_" + cookie_name;
      var name_trimmed = kv[0].replace(cookie_name_with_tag+"_", "");
      result[name_trimmed] = String(kv[1]).replace(https://docs.tealium.com/%3b/g, ';')
    }
    return result;
  }, {});
}
var utag_cookies = read_utag_cookies();
//save the Tealium Visitor ID in memory
var moments_identifier = utag_cookies["v_id"] || null
```

### `utag.js` 4.49 以前 {#utag-js-4-49-and-below}

```js
function getCookie(cname) {
    let name = cname + "=";
    let decodedCookie = decodeURIComponent(document.cookie);
    let ca = decodedCookie.split(';');
    for (let i = 0; i < ca.length; i++) {
        let c = ca[i];
        while (c.charAt(0) == ' ') {
            c = c.substring(1);
        }
        if (c.indexOf(name) == 0) {
            return c.substring(name.length, c.length);
        }
    }
    return "";
}

// Extracting the visitor ID from the utag_main cookie
var utag_cookie = getCookie("utag_main");

//save the Tealium Visitor ID in memory

var moments_identifier = utag_cookie.split("v_id:")[1].split("$")[0] || "";
```

## 手順 2：Context API を呼び出す

Context API エンドポイントにリクエストを送信し、レスポンスデータをローカル保存に保存して、サイト内マーケティング活動やパーソナライゼーションに使用します。

以下のテンプレートコードを別の Advanced JavaScript 拡張機能に追加し、アカウントと対象エンジンに応じて更新します。このコードは、前の拡張機能で割り当てた `moments_identifier` 変数を、API の URL エンドポイントの識別子パラメーターにマッピングします。


<blockquote>
Ensure this code loads after the previous JavaScript extension according to the [Order of Operations](https://docs.tealium.com/order-of-operations/).
</blockquote>


* **タイトル**：[Context API]
* **スコープ**：Pre Loader
* **タイプ**：Advanced JavaScript

```js
// Assign the engine ID you want to request 
var engine_id = "your_engine_id"; 


// suppressNotFound is an optional parameter 

// Set to false for HTTP 404 when visitor is not found 
// var suppressNotFound = true;

// Construct the API URL
// This example does not include optional parameters
// Add optional parameters, if required

var apiUrl = "CONTEXT_API_ENDPOINT_URL" + moments_identifier;

// Example: "https://personalization-api.us-west.prod.tealiumapis.com/personalization/accounts/example/profiles/main/engines/abc123/visitors/" + "0123456789"

// Add function for writing the Context API response to localStorage
function writeToLocalStorage(obj, engineId) {
    // Prefix for localStorage keys
    const prefix = 'moments_' + engineId + '_';

    // Function to save an object property to localStorage
    const saveToLocalStorage = (key, value) => {
        localStorage.setItem(prefix + key, JSON.stringify(value));
    };

    // Loop through each top-level property in the object
    for (const key in obj) {
        if (obj.hasOwnProperty(key)) {
            saveToLocalStorage(key, obj[key]);
        }
    }
}


// Fetch the API

fetch(apiUrl)
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        return response.json();
    })
    .then(data => {
        // Handle the response data
        if (data) {
        // set the data to localStorage, categorised by grouping. For example, attributes, badges, and audiences.
        writeToLocalStorage(data, engine_id) 
            
        }
    })
    .catch(error => console.error('Context API error:', error));
//

```

## 手順 3：ワークフローに統合する

ユースケースに応じて、サイト内パフォーマンスまたはパーソナライゼーションのベンダーとデータを統合します。


<blockquote>
To optimize the DNS request process, consider using DNS prefetching. For more information, see [The Chromium Projects > DNS Prefetching](https://www.chromium.org/developers/design-documents/dns-prefetching/).
</blockquote>
