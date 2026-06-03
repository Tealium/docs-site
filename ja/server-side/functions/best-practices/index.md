---
title: 関数のベストプラクティス
description: この記事では、メモリと実行時間の制限を超えないための関数のベストプラクティスを提供します。
url: https://docs.tealium.com/ja/server-side/functions/best-practices/
---
## 実行時間を決定するためのテストを実行する

データ変換関数は実行時間が150ミリ秒に制限されています。イベントと訪問関数は実行時間が10秒に制限されています。

関数の実行時間に影響を与える要因は多くあります。関数が許可された時間内に実行できるかを確認するために、予想されるイベントペイロードで複数のテストを実行してください。

## ユニバーサルデータオブジェクト（UDO）を正規化する

データレイヤーには、イベントが発生したページに関する基本情報が含まれています。UDOは、特定のイベントタイプの情報を含むより動的な構造です。これは、イベントのサイズが異なる可能性があることを意味します。推奨される最大イベントサイズは50KBです。データをコンパクトに保つために、冗長なデータエントリを削除してください。同じデータが複数のフィールド（例えば、データレイヤーとUDOで）に存在する場合、それはUDOからの削除の候補です。特定のイベントタイプに必要ないデータチャンクも、イベントUDOからの削除の候補です。

## 標準モジュールの部分的なインポートを使用する

実行環境は、部分的なインポートをサポートする標準モジュールを提供しています。これにはCryptoESが含まれます。

モジュール全体をインポートするのではなく、必要な機能のみをインポートしてください。例えば：

```
import { MD5 } from &#39;crypto-es/lib/md5.js&#39;;
```

## デバッグログメッセージの使用を避ける

本番環境に関数を公開する前に、デバッグ目的で使用される `console.log` メッセージを削除またはコメントアウトしてください。

例えば、イベント全体をログに送信するために `JSON.stringify` の使用を避けてください。次の例に示すように、特定の変数のログメッセージを使用してください：

```
console.log(event.data.udo.property_to_track);
```

## 組み込みの `flatten()` モジュールを使用する

組み込みの `flatten()` モジュールは、任意のネストされたオブジェクトをフラット化するために使用できます。これは、データ変換関数に特に有用です。変換関数は、オブジェクトの配列やネストされたオブジェクトなど、ネストされたデータ構造を扱うことができますが、イベントがネストされたデータ構造を含まないようにフラット化する必要があります。

## JavaScriptの最適化を使用する

配列やオブジェクトのプロパティを反復処理するなど、集中的なタスクにはJavaScriptの最適化を使用してください。

### 配列を反復処理する例

```js
const array = [1, 2, 3];
const arrayLength = array.length;

for (let i = 0; i &lt; arrayLength; i&#43;&#43;) {
    const arrayItem = array[i];
}
```

### オブジェクトのプロパティを反復処理する例

```js
const obj = { a: 1, b: 2, c: 3 };
const keys = Object.getOwnPropertyNames(obj);
const keysLength = keys.length;

for (let i = 0; i &lt; keysLength; i&#43;&#43;) {
    const keyName = keys[i];
    const value = obj[keyName];
}
```

## HTTPリクエスト内でのみ認証トークンを参照する

認証トークンは、関数がHTTPリクエストのコンテキスト内で実行される場合にのみ利用可能です。HTTPリクエストの外で認証トークンを参照すると、システムはトークンをUUIDプレースホルダーに置き換えます。

```js
// 正しい: HTTPリクエストハンドラ内でのアクセストークン
activate(async ({ visitor, helper }) =&gt; {
  const response = await fetch(
    &#34;https://fcm.googleapis.com/v1/projects/YOURPROJECT/messages:send&#34;,
    {
      method: &#34;POST&#34;,
      headers: {
        &#39;Authorization&#39;: &#39;Bearer &#39; &#43; helper.getAuth(&#39;firebase_cloud_messaging&#39;),
        &#39;Content-Type&#39;: &#39;application/json&#39;
      },
      body:body
    }
  );
});
}

// 不正確: HTTPリクエストハンドラの外でのアクセストークン
const token = helper.getAuth(&#39;firebase_cloud_messaging&#39;); // これはUUIDプレースホルダーに置き換えられます
```