---
title: V2関数をV3ランタイムに移行する
description: 新しいイベントと訪問関数は**Action V3**ランタイムを使用します。**Action V2**ランタイムを使用している既存の関数は、**Action V3**ランタイムに移行する必要があります。この記事では、移行プロセスに関する情報を提供します。
url: https://docs.tealium.com/ja/server-side/functions/event-visitor-functions/migrate-v2-to-v3/
---
## V3とV2関数の違い

V3ランタイムを使用するイベントと訪問関数は、以下のようにV2関数と異なります：

* **パラメータと名前付きエクスポート** &ndash; 入力データはパラメータとして提供され、名前付きエクスポートではありません。
  * イベント関数には`event`と`helper`の2つのパラメータがあります。
  * 訪問関数には`visitor`、`visit`、`helper`の3つのパラメータがあります。
* **ヘルパー関数** &ndash; `helper`オブジェクトは、認証トークンIDを取得したり、グローバル変数を取得するために使用されます。
    * `auth.get()`は`helper.getAuth()`に置き換えられました。
    * `store.get()`は`helper.getGlobalVariable()`に置き換えられました。
* **イベントの収集**
  * `tealium.sendCollectEvent()`は`track()`に置き換えられ、名前付きパラメータを使用します。


<blockquote>
データ変換関数は**Transformation V0**ランタイムを使用し、V3ランタイムのリリースによって影響を受けません。
</blockquote>


### V2関数の例

以下のコード例は、収集エンドポイントにイベントを送信するV2イベント関数と、このイベント関数のV3バージョンを示しています。



```js
import { event, tealium } from "tealium";
(async () => {
    const searchQuery = new URLSearchParams({ path: event.data.dom.pathname, query: event.data.dom.search_query });
    
    const newEvent = await fetch(`https://getnew.event.com?${searchQuery}`)
        .then(response => {
            if (!response.ok) {
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.json();
        });
    
    tealium.sendCollectEvent(
        newEvent,
        event.account,
        event.profile,
        'abc123')
        .then(response => {
            if(!response.ok){
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.text();
        })
        .then(data => console.log('Result : ', data))
        .catch(error => console.error('Error:', error.message));
})();
```


```js
activate(async ({ event }) => {  
    const searchQuery = new URLSearchParams({ path: event.data.dom.pathname, query: event.data.dom.search_query });
        
    const newEvent = await fetch(`https://getnew.event.com?${searchQuery}`)
        .then(response => {
            if (!response.ok) {
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.json();
        });
        
    track(newEvent, {
        tealium_account: event.account,
        tealium_profile: event.profile,
        tealium_datasource: 'abc123'
        })
        .then(response => {
            if(!response.ok){
                throw new Error(`Network response was not ok. Status code: ${response.status}.`);
            }
            return response.text();
        })
        .then(data => console.log('Result : ', data))
        .catch(error => console.error('Error:', error.message));
})();
```



## V3関数を作成する

イベントまたは訪問関数をV3に移行するには、移行する関数のタイプに応じてV3イベントまたは訪問関数を作成します。詳細については、[関数を作成する]()を参照してください。次に、次のことを行います：

1. コードエディタでV3関数のデフォルトコードをすべて削除し、次のイベントまたは訪問コードを追加します。これは空の関数です。
次のステップで関数コードを追加し、コードを変更します。


```js
activate(async ({ event }) => {  

});
```


```js
activate(async ({ visitor, visit }) => {  

});
```



1. V2関数のコードを、以下に示す関数の最初の行の後からコピーします：
    ```js
    (async (event, helper) => {
    ```  
    そして、関数の最後の行の上で終了します：
    ```js
    })();
     ```  
1. コピーしたコードを空のV3関数に貼り付けます。`activate`行と終了行`});`の間です。

## 関数コードを更新する

関数がライブラリやヘルパー関数を使用している場合、またはTealium Collectにイベントを送信している場合、空の関数にコピーされたコードは、以下のセクションで説明するように変更する必要があります。

### Tealium Collectにイベントを送信する

例の関数は`tealium.sendCollectEvent()`を使用しています。この呼び出しは`track()`呼び出しに置き換える必要があります。以下の例は、V2の`tealium.sendCollectEvent()`呼び出しとV3の`track()`呼び出しを示しています。



```js
import { event, tealium } from 'tealium';

(async () => {
    const newEvent = { data: event.data.udo };

    tealium.sendCollectEvent(newEvent,
        event.account,
        event.profile,
        'abc123')
    ...
})();
```


```js
activate(({ event }) => {
    const newEvent = { data: event.data.udo };

    track(newEvent, {
        tealium_account: event.account,
        tealium_profile: event.profile,
        tealium_datasource: 'abc123'
    })
    ...
})
```



`track()`呼び出しでは、`'abc123'`をデータソースキーに置き換えます。

### ライブラリの使用

V2関数がライブラリ、例えばCrytpoESを使用している場合、`activate`行の前にインポート行を追加します。



```js
import { event, tealium } from "tealium";
import CryptoES from 'crypto-es';
...
```


```js
import CryptoES from 'crypto-es';
activate(async ({ event, helper }) => {  
    ...
});
```  



### 認証トークンとグローバル変数

V2関数が認証トークンまたはグローバル変数を使用している場合、V3関数の`activate`行に`helper`を関数パラメータに追加します。例えば：

```js
activate(async ({ event, helper }) => {
});
```

V2コード内の`auth.get()`のすべてのインスタンスを`helper.getAuth()`に置き換えます。例えば：



```js
import { auth } from 'tealium';

const token = auth.get("myAuthToken");
```


```js
activate(({event, helper }) => {
    const token = helper.getAuth("myAuthToken");
})
```




<blockquote>
認証トークンはHTTPリクエスト内の関数によってのみ参照できます。HTTPリクエストの外でトークンを参照しようとすると、トークンはUUIDプレースホルダーに置き換えられます。
</blockquote>


`store.get()`のすべてのインスタンスを`helper.getGlobalVariable()`に置き換えます。例えば：



```js
import {store } from 'tealium';

const gVar = store.get("myGlobalVar");
```


```js
activate(({event, helper }) => {    
    const gVar = helper.getGlobalVariable("myGlobalVar");
})
```

