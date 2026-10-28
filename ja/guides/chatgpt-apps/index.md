---
title: Tealium + ChatGPT アプリ
description: クライアントサイド、サーバーサイド、ハイブリッドの各アプローチで一貫した訪問IDを維持しながら、ChatGPTアプリにTealiumトラッキングを実装します。
url: https://docs.tealium.com/ja/guides/chatgpt-apps/
---
## はじめに

Tealiumは、ブラウザ、ウィジェット、カスタムChatGPTインターフェイスにおけるアプリのようなエクスペリエンスのためのデータ基盤を提供します。プラットフォーム間で一貫したデータ収集と訪問ID管理をサポートします。

このChatGPT向けソリューションでは、MCPに対応した設計を採用し、次のことを実現します。

* 主要なインタラクション（商品の表示、ボタンのクリック、購入）を追跡する。
* クライアント、サーバー、ChatGPTの各コンテキストでIDを統合する。
* Tealium Collectを使用してイベントをリアルタイムでストリーミングする。
* Tealium Context APIとTealium AudienceStreamを使用してエクスペリエンスをパーソナライズする。

## オプション1：クライアントサイドトラッキング

このアプローチでは、Tealium iQの専用プロファイルから標準の[ユニバーサルタグ（`utag.js`）](https://docs.tealium.com/ja/platforms/javascript/)をインストールします。唯一の違いは、`utag.js`によって生成される匿名IDに依存せず、ユーティリティ関数を使用して独自のIDを生成し、永続化する点です。

**利点：**

* Tealium iQタグ管理のタグベンダーマーケットプレイスをすべて利用できる。
* 同意管理が組み込まれている。
* A/Bテストとパーソナライゼーショントリガーをサポートする。

次のサンプルコードは、以下の処理を示しています。

* Webサイトの場合と同様に、`utag.js`を読み込む。
* 匿名の訪問IDを生成して永続化する。
* ChatGPTアプリの初回読み込みを追跡する。
* カスタムメソッドを使用して、関連するユーザー操作を追跡する。

```html
<script>
  // Load Tealium iQ
  (function(a,b,c,d){
    a='https://tags.tiqcdn.com/utag/[ACCOUNT]/[PROFILE]/[ENVIRONMENT]/utag.js';
    b=document;c='script';d=b.createElement(c);d.src=a;
    d.type='text/java'+c;d.async=true;
    a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
  })();

  // Generate a 32-char lowercase alphanumeric visitor ID
  function generateTealiumVisitorId() {
    const chars = 'abcdefghijklmnopqrstuvwxyz0123456789';
    return Array.from({ length: 32 }, () => chars[Math.floor(Math.random() * chars.length)]).join('');
  }

  // Retrieve or create & persist the visitor ID
  let tealium_visitor_id = localStorage.getItem('tealium_visitor_id');
  if (!tealium_visitor_id) {
    tealium_visitor_id = generateTealiumVisitorId();
    localStorage.setItem('tealium_visitor_id', tealium_visitor_id);
  }

  // App initialized
  utag.track('event', {
    'tealium_event': 'interface_loaded',
    'app_version': '2.1.0',
    'user_tier': 'enterprise',
    'tealium_visitor_id': tealium_visitor_id
  });

  // PDP view
  function trackViewPdp(product) {
    utag.track('view', {
      'tealium_event': 'view_pdp',
      'product_id': product.id,
      'product_name': product.name,
      'category': product.category,
      'price': product.price,
      'currency': product.currency || 'USD',
      'tealium_visitor_id': tealium_visitor_id
    });
  }

  // Button click
  function trackButtonClick(button) {
    utag.track('link', {
      'tealium_event': 'button_click',
      'button_id': button.id,
      'button_text': button.text,
      'location': button.location || 'pdp',
      'app_version': '2.1.0',
      'tealium_visitor_id': tealium_visitor_id
    });
  }
</script>
```

## オプション2：サーバーサイドトラッキング

サーバーサイドトラッキングでは、[HTTP API](https://docs.tealium.com/ja/platforms/http-api/endpoint/)を使用してイベントをTealiumに直接送信します。クライアントサイドのソリューションと同様に、追加したユーティリティ関数を使用して独自の匿名訪問IDを生成し、永続化します。

次のシナリオでは、このアプローチを推奨します。

* CSPの制限によって外部JavaScriptを読み込めない場合。
* 購入などの重要なイベントのデータトラッキングを確実に行う必要がある場合。

次のサーバーサイドトラッキングソリューションを利用できます。

### Node.jsアプリ（推奨）

Node.jsソリューションには、匿名訪問IDを生成して永続化し、追跡対象イベントのラッパー関数を呼び出すクライアントコードが含まれています。

たとえば、次のサンプルコードは訪問IDを生成し、注文トラッキングリクエストをサーバーに送信します。`order`オブジェクトは、顧客が購入を完了したときにアプリから渡されます。

```js
// Generate a 32-char lowercase alphanumeric visitor ID
function generateTealiumVisitorId() {
  const chars = 'abcdefghijklmnopqrstuvwxyz0123456789';
  return Array.from({ length: 32 }, () => chars[Math.floor(Math.random() * chars.length)]).join('');
}

// Retrieve or create & persist the visitor ID
let tealium_visitor_id = localStorage.getItem('tealium_visitor_id');
if (!tealium_visitor_id) {
  tealium_visitor_id = generateTealiumVisitorId();
  localStorage.setItem('tealium_visitor_id', tealium_visitor_id);
}

async function trackPurchaseServer(order) {
  await fetch('/api/tealium/track', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      'tealium_event': 'purchase',
      'tealium_visitor_id': tealium_visitor_id,
      'order_id': order.id,
      'order_total': order.total,
      'currency': order.currency || 'USD',
      'items': order.items
    })
  });
}
```

次のサンプルサーバーサイドコードでは、トラッキング呼び出しを受け付けるエンドポイントを構成し、[Tealium for Node.js](https://docs.tealium.com/ja/platforms/node/install/)を使用して、それらのイベントをTealium Collectに転送します。

```js
// npm i tealium-collect express
const express = require('express');
const TealiumCollect = require('tealium-collect');
const app = express();
app.use(express.json());

const tealium = new TealiumCollect({
  'account': 'your-account',
  'profile': 'chatgpt-app',
  'environment': 'prod'
});

app.post('/api/tealium/track', async (req, res) => {
  try {
    const tealium_visitor_id = req.body.tealium_visitor_id;

    if (!/^[a-z0-9]{32}$/.test(tealium_visitor_id || '')) {
      return res.status(400).json({ error: 'Invalid or missing tealium_visitor_id' });
    }

    const allowed = new Set(['interface_loaded','view_pdp','button_click','purchase']);
    if (!allowed.has(req.body.tealium_event)) {
      return res.status(400).json({ error: 'Unsupported event type' });
    }

    await tealium.track({
      ...req.body,
      tealium_visitor_id,
      'timestamp': req.body.timestamp || new Date().toISOString()
    });

    res.status(204).end();
  } catch (e) {
    console.error('Tealium track error:', e);
    res.status(500).json({ error: 'Tracking failed' });
  }
});

app.listen(3000, () => console.log('Tealium server listening on 3000'));
```
### ブラウザーアプリ

`<script>` タグを埋め込めるブラウザーアプリでは、この方法を使用します。このコードは、`fetch()` と [HTTP API](https://docs.tealium.com/ja/platforms/http-api/endpoint/) を使用してイベントを Tealium に直接送信し、同じユーティリティメソッドを使用して匿名訪問 ID を生成および永続化します。

```html
<script>
  // Generate a 32-char lowercase alphanumeric visitor ID
  function generateTealiumVisitorId() {
    const chars = 'abcdefghijklmnopqrstuvwxyz0123456789';
    return Array.from({ length: 32 }, () => chars[Math.floor(Math.random() * chars.length)]).join('');
  }

  // Retrieve or create & persist the visitor ID
  let tealium_visitor_id = localStorage.getItem('tealium_visitor_id');
  if (!tealium_visitor_id) {
    tealium_visitor_id = generateTealiumVisitorId();
    localStorage.setItem('tealium_visitor_id', tealium_visitor_id);
  }

  async function sendCollectEvent(payload) {
    const base = {
      'tealium_account': 'your-account',
      'tealium_profile': 'chatgpt-app',
      'tealium_visitor_id': tealium_visitor_id,
      'timestamp': new Date().toISOString()
    };

    await fetch('https://collect.tealiumiq.com/event', {
      'method': 'POST',
      'headers': { 'Content-Type': 'application/json' },
      'body': JSON.stringify({ ...base, ...payload })
    });
  }

  function trackViewPdpServer(product) {
    return sendCollectEvent({
      'tealium_event': 'view_pdp',
      'product_id': product.id,
      'product_name': product.name,
      'product_category': product.category,
      'product_price': product.price,
      'product_currency': product.currency || 'USD'
    });
  }

  function trackButtonClickServer(button) {
    return sendCollectEvent({
      'tealium_event': 'button_click',
      'button_id': button.id,
      'button_text': button.text,
      'location': button.location || 'pdp',
      'app_version': '2.1.0'
    });
  }
</script>
```

## オプション 3：ハイブリッド（推奨）

ハイブリッド方式では、クライアント側のソリューションを使用して `interface_loaded`、`view_pdp`、`button_click` などのインタラクションイベントをトラッキングし、サーバー側のソリューションを使用して `purchase` などの信頼性が求められるイベントをトラッキングします。アプリを可能な限り完全にトラッキングするために、この方式を推奨します。


<blockquote>
When running the hybrid solution, do not load the Tealium Collect tag in your iQ profile. This prevents duplicate event tracking.
</blockquote>


## 訪問 ID

正確なトラッキングと統合された訪問プロファイルを実現するために、クライアント側とサーバー側のイベントの両方で、常に同じ匿名訪問 ID を使用してください。この方式により、ChatGPT、Web、モバイル全体で単一の訪問 ID が維持され、一貫したトラッキングとリアルタイムのパーソナライゼーションが可能になります。


<blockquote>
We recommend including known user identifiers as separate parameters when available, for example `customer_id` or `email_address_hash`, but do not use these values to replace `tealium_visitor_id`.
</blockquote>


## MCP 統合（任意）

ChatGPT から呼び出せるシンプルな MCP ツールをサーバーから公開します。この方式では、ChatGPT が会話ロジックを処理し、サーバーが形式、ID、ポリシーを適用します。

**ツール：** `tealium-track-event`

**スキーマの例：**

```json
{
  "account": "your-account",
  "profile": "chatgpt-app",
  "environment": "prod",
  "event": "view_pdp",
  "visitorId": "abcdefghijklmnopqrstuvwxyz012345",
  "data": {
    "product_id": "widget-123",
    "price": 29.99,
    "currency": "USD"
  }
}
```

**検証：**

* `visitorId` は正規表現 `/^[a-z0-9]{32}$/` に一致する必要があります。
* `event` は許可されたイベントのリスト（`interface_loaded`、`view_pdp`、`button_click`、`purchase`）に含まれている必要があります。

## Context API MCP

パーソナライゼーションを有効にするには、[Context API MCP サーバー](https://docs.tealium.com/context-api-mcp-server/)をアプリに追加します。

**フローの例：**

1. `view_pdp`、`button_click`、`purchase` イベントをトラッキングします。
2. **AudienceStream** が訪問プロファイルを構築します。
3. チャット UI（または MCP ツール）が `tealium_visitor_id` を使用して **Context API** にクエリを実行します。
4. レスポンスが状況に合わせて調整されます（レコメンデーション、オファー、トーン）。

## データプライバシーとコンプライアンス

このアプリは、次の機能によってデータプライバシーとコンプライアンスをサポートします。

* Tealium iQ Consent Manager による同意ベースのアクティベーション。
* データ送信前の省略またはハッシュ化による PII ガバナンス。
* 地域別のコンプライアンス（GDPR、CCPA、データレジデンシー）。

## サンプルアプリ

### 前提条件

* Node.js 18 以降（LTS）
* `npm` または `pnpm`
* Tealium のアカウント、プロファイル、環境
* （任意）MCP を公開するための ngrok
 
### インストール  
    
1. メインプロジェクトの依存関係をインストールします。   
    ```bash
    pnpm install
    ```
2. サーバーの依存関係をインストールします。   
    ```bash
    cd server
    pnpm install
    cd ..
    ```

### アプリケーションの実行  
  
1. フロントエンドバンドルをビルドします。  
    ```sh
    pnpm run build  
    ```
2. MCP サーバーを起動します。  
    ```sh
    cd server  
    pnpm start
    ```  
2. サーバーは [http://localhost:8000/mcp](http://localhost:8000/mcp) で実行されます。
3. ngrok トンネルを生成します（新しいターミナルで実行）。  
    ```sh
    ngrok http 8000  
    ```
3. ngrok から次の出力が返されます。  
    ```none
    Session Status    online  
    Account           Your Account (Plan: Free)  
    Update            update available (version 3.x.x, Ctrl-C to update)  
    Version           3.x.x  
    Region            United States (us)  
    Web Interface     http://127.0.0.1:4040  
    Forwarding        https://abc123def456.ngrok-free.app -> http://localhost:8000  
    ```
4. サーバーコード内の CSP ドメインを更新します。
    * ターミナル出力から ngrok URL（例：`https://abc123def456.ngrok-free.app`）をコピーします。  
    * `server/index.ts` の 30 行目と 34 行目で、`https://resolvedly-pouched-nena.ngrok-free.dev` を新しい ngrok URL に置き換えます。 
    * `src/tealium/TealiumTracker.tsx` の 134 行目にも同じ変更を加えます。
5. サーバーを再起動します。  
    ```sh
    # Kill the current server (Ctrl+C)
    cd server
    pnpm start
    ``` 
6. 新しい URL を使用してフロントエンドを再ビルドします。  
    ```sh
    cd ..  
    pnpm run build
    ```  

次のアクセスポイントを記録しておいてください。  

* ローカル MCP サーバー：[http://localhost:8000/mcp](http://localhost:8000/mcp)  
* ヘルスチェック：[http://localhost:8000/health](http://localhost:8000/health)
* API エンドポイント：[http://localhost:8000/api/tealium/track](http://localhost:8000/api/tealium/track)  
* 公開 ngrok URL：ngrok URL + `/mcp`
* 公開 API：ngrok URL + `/api/tealium/track`

### ChatGPT へのアプリの追加

1. **ChatGPT > Settings > Apps and Connectors** に移動します。
2. **Advanced Settings** で **Developer Mode** を有効にします。
3. **MCP server field** に **ngrok URL** を貼り付けます。

### Tealium アプリの起動

1. プロンプトが表示されたら、`tealium-tracker` ツールを使用します。  
1. Tealium のアカウント、プロファイル、環境を入力します。  
1. Tealium Universal タグ（`utag.js`）が読み込まれ、Web アプリの場合と同様にイベントがトラッキングされます。


<blockquote>
If third-party libraries are blocked, allow their resources in your CSP.
</blockquote>


### **サーバー側イベントトラッキング**

サーバー側トラッキングを有効にすると、クライアント側の呼び出しが `/api/tealium/track` に送信されます。このエンドポイントは、Tealium Collect NPM モジュールを使用してトラッキングリクエストを実行します。



[Tealium Trace](https://docs.tealium.com/about-trace/) で結果を検証します。

