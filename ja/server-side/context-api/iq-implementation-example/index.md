---
title: Context APIとiQタグ管理の実装例ガイド
description: Context APIをTealium iQタグ管理インストールに統合する例を見てください。
url: https://docs.tealium.com/ja/server-side/context-api/iq-implementation-example/
---
## 仕組み

Context APIは、ウェブサイトやアプリケーションに統合できるユニークなエンドポイントを作成します。

以下のステップに従って、[Tealium iQ Advanced JavaScript Code Extension](https://docs.tealium.com/advanced-javascript-code-extension/)を使用してTealiumワークフローにContext APIを実装します。次の例では、訪問のデータをContext APIからリクエストするためにFetch APIを使用していますが、`XMLHttpRequest`などの他のJavaScriptオプションもサポートされています。

## ステップ1: 訪問IDの取得

Tealiumの`utag_main`クッキーから`v_id`を解析します。

拡張機能に次のコードをコピーしてください。

* **タイトル**: utag.jsクッキーから識別子を解析 [Context API]
* **スコープ**: プリローダー
* **タイプ**: アドバンスドJavaScript

### `utag.js` 4.50+ 


<blockquote>
`split_cookie=false`オプションを使用する場合は、[`utag.js` 4.49以下](#utag-js-4-49-and-below)のコード例を使用してください。
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
//メモリにTealium訪問IDを保存
var moments_identifier = utag_cookies["v_id"] || null
```

### `utag.js` 4.49以下 {#utag-js-4-49-and-below}

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

// utag_mainクッキーから訪問IDを抽出
var utag_cookie = getCookie("utag_main");

//メモリにTealium訪問IDを保存

var moments_identifier = utag_cookie.split("v_id:")[1].split("$")[0] || "";
```

## ステップ2: Context APIを呼び出す

Context APIエンドポイントをリクエストし、レスポンスデータをローカル保存に保存して、オンサイトのマーケティング活動やパーソナライゼーションに使用します。

別のアドバンスドJavaScript拡張機能に次のテンプレートコードを追加し、アカウントとターゲットエンジンに応じて更新してください。このコードは、前の拡張機能で割り当てられた`moments_identifier`変数をAPIのURLエンドポイントの識別子パラメータにマッピングします。


<blockquote>
このコードが前のJavaScript拡張機能の後にロードされるようにしてください。[操作の順序](https://docs.tealium.com/order-of-operations/)を参照してください。
</blockquote>


* **タイトル**: [Context API]
* **スコープ**: プリローダー
* **タイプ**: アドバンスドJavaScript

```js
// リクエストしたいエンジンIDを割り当てます
var engine_id = "your_engine_id"; 


// suppressNotFoundはオプションのパラメータです

// 訪問が見つからない場合はHTTP 404に構成します
// var suppressNotFound = true;

// API URLを構築します
// この例にはオプションのパラメータは含まれていません
// 必要に応じてオプションのパラメータを追加してください

var apiUrl = "CONTEXT_API_ENDPOINT_URL" + moments_identifier;

// 例: "https://personalization-api.us-west.prod.tealiumapis.com/personalization/accounts/example/profiles/main/engines/abc123/visitors/" + "0123456789"

// Context APIレスポンスをlocalStorageに書き込む関数を追加します
function writeToLocalStorage(obj, engineId) {
    // localStorageキーのプレフィックス
    const prefix = 'moments_' + engineId + '_';

    // オブジェクトのプロパティをlocalStorageに保存する関数
    const saveToLocalStorage = (key, value) => {
        localStorage.setItem(prefix + key, JSON.stringify(value));
    };

    // オブジェクトの各トップレベルプロパティをループ処理します
    for (const key in obj) {
        if (obj.hasOwnProperty(key)) {
            saveToLocalStorage(key, obj[key]);
        }
    }
}


// APIをフェッチします

fetch(apiUrl)
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        return response.json();
    })
    .then(data => {
        // レスポンスデータを処理します
        if (data) {
        // データをlocalStorageに保存します。例えば、属性、バッジ、オーディエンスなどのグループに分類します。
        writeToLocalStorage(data, engine_id) 
            
        }
    })
    .catch(error => console.error('Context API error:', error));
//

```

## ステップ3: ワークフローに統合する

データをオンサイトのパフォーマンスやパーソナライゼーションベンダーと統合します。


<blockquote>
DNSリクエストプロセスを最適化するために、DNSプリフェッチングを検討してください。詳細については、[The Chromium Projects > DNS Prefetching](https://www.chromium.org/developers/design-documents/dns-prefetching/)を参照してください。
</blockquote>
 