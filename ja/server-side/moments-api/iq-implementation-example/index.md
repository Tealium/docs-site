---
title: Moments APIとiQタグ管理の実装ガイド
description: Moments APIをTealium iQタグ管理インストールに統合する例を見てみましょう。
url: https://docs.tealium.com/ja/server-side/moments-api/iq-implementation-example/
---
## 動作原理

Moments APIは、ウェブサイトやアプリケーションに統合できるユニークなエンドポイントを作成します。

以下のステップに従って、[Tealium iQ Advanced JavaScript Code Extension]()を使用してTealiumワークフローにMoments APIを実装します。この例では、訪問のデータをMoments APIからリクエストするためにFetch APIを使用していますが、`XMLHttpRequest`などの他のJavaScriptオプションもサポートされています。

## ステップ1: 訪問IDの取得

Tealiumの`utag_main`クッキーから`v_id`を解析します。

拡張機能に次のコードをコピーします。使用している`utag.js`のバージョンに応じてください。

* **タイトル**: utag.jsクッキーから識別子を解析 [Moments API]
* **スコープ**: プリローダー
* **タイプ**: アドバンスドJavaScript

### `utag.js` 4.50以上

`split_cookie=false`オプションを使用する場合は、[`utag.js` 4.49以下](#utag-js-4-49-and-below)のコード例を使用してください。

```js
read_utag_cookies = function() {
  if(!document.cookie || document.cookie === &#34;&#34;) {
    return {};
  }
  var cookies = document.cookie.split(&#34;; &#34;);
  return cookies.reduce(function(result, cookie) {
    var kv = cookie.split(&#34;=&#34;);
    if(kv[0].startsWith(&#34;utag_&#34;)) {
      var cookie_name = kv[0].split(&#34;_&#34;)[1];
      var cookie_name_with_tag = &#34;utag_&#34; &#43; cookie_name;
      var name_trimmed = kv[0].replace(cookie_name_with_tag&#43;&#34;_&#34;, &#34;&#34;);
      result[name_trimmed] = String(kv[1]).replace(/%3b/g, &#39;;&#39;)
    }
    return result;
  }, {});
}
var utag_cookies = read_utag_cookies();
//メモリにTealium訪問IDを保存
var moments_identifier = utag_cookies[&#34;v_id&#34;] || null
```

### `utag.js` 4.49以下 {#utag-js-4-49-and-below}

```js
function getCookie(cname) {
    let name = cname &#43; &#34;=&#34;;
    let decodedCookie = decodeURIComponent(document.cookie);
    let ca = decodedCookie.split(&#39;;&#39;);
    for (let i = 0; i &lt; ca.length; i&#43;&#43;) {
        let c = ca[i];
        while (c.charAt(0) == &#39; &#39;) {
            c = c.substring(1);
        }
        if (c.indexOf(name) == 0) {
            return c.substring(name.length, c.length);
        }
    }
    return &#34;&#34;;
}

// utag_mainクッキーから訪問IDを抽出
var utag_cookie = getCookie(&#34;utag_main&#34;);

//メモリにTealium訪問IDを保存

var moments_identifier = utag_cookie.split(&#34;v_id:&#34;)[1].split(&#34;$&#34;)[0] || &#34;&#34;;
```

## ステップ2: Moments APIを呼び出す

Moments APIエンドポイントをリクエストし、応答データをローカル保存に保存して、オンサイトのマーケティング活動やパーソナライゼーションに使用します。

別のアドバンスドJavaScript拡張機能に次のテンプレートコードを追加し、アカウントとターゲットエンジンに応じて更新します。このコードは、前の拡張機能で割り当てられた`moments_identifier`変数をAPIのURLエンドポイントの識別子パラメータにマッピングします。

このコードが前のJavaScript拡張機能の後にロードされるように、[操作の順序]()に従ってください。

* **タイトル**: [Moments API]
* **スコープ**: プリローダー
* **タイプ**: アドバンスドJavaScript

```js
// リクエストするエンジンIDを割り当てます
var engine_id = &#34;your_engine_id&#34;; 


// suppressNotFoundはオプションのパラメータです

// 訪問が見つからない場合はHTTP 404に構成します
// var suppressNotFound = true;

// API URLを構築します
// この例ではオプションのパラメータは含まれていません
// 必要に応じてオプションのパラメータを追加します

var apiUrl = &#34;MOMENTS_API_ENDPOINT_URL&#34; &#43; moments_identifier;

// 例: &#34;https://personalization-api.us-west.prod.tealiumapis.com/personalization/accounts/example/profiles/main/engines/abc123/visitors/&#34; &#43; &#34;0123456789&#34;

// Moments APIの応答をlocalStorageに書き込む関数を追加します
function writeToLocalStorage(obj, engineId) {
    // localStorageキーのプレフィックス
    const prefix = &#39;moments_&#39; &#43; engine_id &#43; &#39;_&#39;;

    // オブジェクトのプロパティをlocalStorageに保存する関数
    const saveToLocalStorage = (key, value) =&gt; {
        localStorage.setItem(prefix &#43; key, JSON.stringify(value));
    };

    // オブジェクトの各トップレベルプロパティをループします
    for (const key in obj) {
        if (obj.hasOwnProperty(key)) {
            saveToLocalStorage(key, obj[key]);
        }
    }
}


// APIをフェッチします

fetch(apiUrl)
    .then(response =&gt; {
        if (!response.ok) {
            throw new Error(&#39;Network response was not ok&#39;);
        }
        return response.json();
    })
    .then(data =&gt; {
        // 応答データを処理します
        if (data) {
        // データをlocalStorageに構成します。例えば、属性、バッジ、オーディエンスなどのグループに分類します。
        writeToLocalStorage(data, engine_id) 
            
        }
    })
    .catch(error =&gt; console.error(&#39;Moments API error:&#39;, error));
//

```

## ステップ3: ワークフローに統合する

データをオンサイトのパフォーマンスやパーソナライゼーションベンダーと統合します。

DNSリクエストプロセスを最適化するために、DNSプリフェッチを検討してください。詳細については、[The Chromium Projects &gt; DNS Prefetching](https://www.chromium.org/developers/design-documents/dns-prefetching/)を参照してください。 