---
title: Tealium + ChatGPT アプリ
description: クライアントサイド、サーバーサイド、ハイブリッドアプローチで一貫した訪問IDを持つChatGPTアプリにTealiumトラッキングを実装します。
url: https://docs.tealium.com/ja/guides/chatgpt-apps/
---
## はじめに

Tealiumは、ブラウザ、ウィジェット、カスタムChatGPTインターフェースでアプリのような体験のためのデータ基盤を提供します。これは、プラットフォーム間で一貫したデータ収集と訪問ID管理をサポートします。

このChatGPTソリューションは、MCPフレンドリーな設計を使用して以下を実現します：

* 主要なインタラクション（製品閲覧、ボタンクリック、購入）の追跡。
* クライアント、サーバー、およびChatGPTコンテキスト間でのIDの統合。
* Tealium Collectを使用したリアルタイムでのイベントストリーミング。
* Tealium Moments APIおよびTealium AudienceStreamを使用した体験のパーソナライズ。

## オプション1：クライアントサイドトラッキング

このアプローチは、Tealium iQの専用プロファイルからの標準的な[Universal Tag (`utag.js`)](https://docs.tealium.com/ja/platforms/javascript/)インストールを使用します。唯一の違いは、`utag.js`によって生成された匿名IDに依存しないため、独自のIDを生成して永続化することです。

**利点：**

* Tealium iQタグ管理タグベンダーマーケットプレイスへのフルアクセス。
* 同意のための組み込みサポート。
* A/Bテストとパーソナライゼーショントリガーをサポート。

以下のサンプルコードは次のことを示しています：

* ウェブサイトで行うように`utag.js`をロードします。
* 匿名訪問IDを生成して永続化します。
* ChatGPTアプリの初期ロードを追跡します。
* カスタムメソッドで関連するユーザーアクションを追跡します。

```html
<script>
  // Tealium iQをロード
  (function(a,b,c,d){
    a='https://tags.tiqcdn.com/utag/[ACCOUNT]/[PROFILE]/[ENVIRONMENT]/utag.js';
    b=document;c='script';d=b.createElement(c);d.src=a;
    d.type='text/java'+c;d.async=true;
    a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
  })();

  // 32文字の小文字英数字の訪問IDを生成
  function generateTealiumVisitorId() {
    const chars = 'abcdefghijklmnopqrstuvwxyz0123456789';
    return Array.from({ length: 32 }, () => chars[Math.floor(Math.random() * chars.length)]).join('');
  }

  // 訪問IDを取得または作成して永続化
  let tealium_visitor_id = localStorage.getItem('tealium_visitor_id');
  if (!tealium_visitor_id) {
    tealium_visitor_id = generateTealiumVisitorId();
    localStorage.setItem('tealium_visitor_id', tealium_visitor_id);
  }

  // アプリ初期化
  utag.track('event', {
    'tealium_event': 'interface_loaded',
    'app_version': '2.1.0',
    'user_tier': 'enterprise',
    'tealium_visitor_id': tealium_visitor_id
  });

  // PDPビュー
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

  // ボタンクリック
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

サーバーサイドトラッキングは、[HTTP API](https://docs.tealium.com/ja/platforms/http-api/endpoint/)を使用してイベントを直接Tealiumに送信します。クライアントサイドソリューションと同様に、独自の匿名訪問IDを生成して永続化するための追加のユーティリティ関数を使用します。

次のシナリオでこのアプローチを推奨します：

* CSP制限により外部JavaScriptのロードが防止される場合。
* 購入などの重要なイベントのデータトラッキングを保証するため。

以下に利用可能なサーバーサイドトラッキングソリューションを示します：

### Node.jsアプリ（推奨）

Node.jsソリューションには、匿名訪問IDを生成して永続化するクライアントコードと、追跡されたイベントのためのラッパー関数の呼び出しが含まれています。

たとえば、次のサンプルコードは訪問IDを生成し、顧客が購入を完了したときにアプリから取得される`order`オブジェクトを使用してサーバーに注文追跡リクエストを送信します。

```js
// 32文字の小文字英数字の訪問IDを生成
function generateTealiumVisitorId() {
  const chars = 'abcdefghijklmnopqrstuvwxyz0123456789';
  return Array.from({ length: 32 }, () => chars[Math.floor(Math.random() * chars.length)]).join('');
}

// 訪問IDを取得または作成して永続化
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

次のサンプルサーバーサイドコードは、トラッキングコールを受け入れるエンドポイントを構成し、[Tealium for Node.js](https://docs.tealium.com/ja/platforms/node/install/)を使用してそれらのイベントをTealium Collectに転送します。

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
    res.status 500).json({ error: 'Tracking failed' });
  }
});

app.listen(3000, () => console.log('Tealium server listening on 3000'));
```
### ブラウザアプリ

`<script>` タグを埋め込むことができるブラウザアプリでこのアプローチを使用します。このコードは `fetch()` と [HTTP API](https://docs.tealium.com/ja/platforms/http-api/endpoint/) を使用してイベントを直接 Tealium に送信し、匿名訪問 ID を生成および保持するための同じユーティリティメソッドを使用します。

```html
<script>
  // 32文字の小文字英数字の訪問IDを生成
  function generateTealiumVisitorId() {
    const chars = 'abcdefghijklmnopqrstuvwxyz0123456789';
    return Array.from({ length: 32 }, () => chars[Math.floor(Math.random() * chars.length)]).join('');
  }

  // 訪問IDを取得または作成して保持
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

## オプション3: ハイブリッド（推奨）

ハイブリッドアプローチは、クライアントサイドソリューションを使用して `interface_loaded`、`view_pdp`、`button_click` などのインタラクションイベントを追跡し、サーバーサイドソリューションを使用して `purchase` などの権威あるイベントを追跡します。このアプローチを使用することで、アプリの追跡を最も完全に行うことができます。


<blockquote>
ハイブリッドソリューションを実行する際は、iQプロファイルでTealium Collectタグをロードしないでください。これにより、イベントの重複追跡が防止されます。
</blockquote>


## 訪問のアイデンティティ

正確な追跡と統一された訪問プロファイルを確保するためには、クライアントサイドとサーバーサイドのイベントの両方で同じ匿名訪問IDを常に使用してください。このアプローチにより、ChatGPT、ウェブ、モバイルを通じて単一の訪問アイデンティティが維持され、一貫した追跡とリアルタイムのパーソナライゼーションが可能になります。


<blockquote>
利用可能な場合は、`customer_id` や `email_address_hash` などの既知のユーザー識別子を別のパラメータとして含めることをお勧めしますが、これらの値を `tealium_visitor_id` で置き換えることはしないでください。
</blockquote>


## MCP統合（オプション）

サーバーからChatGPTが呼び出すシンプルなMCPツールを公開します。このアプローチにより、ChatGPTは会話ロジックを処理し、サーバーは形式、アイデンティティ、ポリシーを強制します。

**ツール:** `tealium-track-event`

**例のスキーマ:**

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

**検証:**

* `visitorId` は正規表現 `/^[a-z0-9]{32}$/` に一致する必要があります。
* `event` は許可されたイベントリスト（`interface_loaded`, `view_pdp`, `button_click`, `purchase`）に含まれている必要があります。

## Moments API MCP

[Moments MCP server](https://docs.tealium.com/moments-api-mcp-server/) をアプリに追加してパーソナライゼーションを有効にします。

**例のフロー:**

1. `view_pdp`, `button_click`, `purchase` のイベントを追跡します。
2. **AudienceStream** が訪問プロファイルを構築します。
3. Chat UI（またはMCPツール）が `tealium_visitor_id` で **Moments API** を照会します。
4. 応答は（推奨、オファー、トーンなど）適応します。

## データプライバシーとコンプライアンス

このアプリは、以下の機能を通じてデータプライバシーとコンプライアンスをサポートします：

* Tealium iQ Consent Managerを通じた同意駆動のアクティベーション。
* データを送信する前に省略またはハッシュ化することによるPIIガバナンス。
* 地域コンプライアンス（GDPR、CCPA、データ居住）。

## サンプルアプリ

### 前提条件

* Node.js 18+ (LTS)
* `npm` または `pnpm`
* Tealium アカウント、プロファイル、環境
* (オプション) ngrok for MCP exposure

### インストール

1. メインプロジェクトの依存関係をインストールします：
    ```bash
    pnpm install
    ```
2. サーバーの依存関係をインストールします：
    ```bash
    cd server
    pnpm install
    cd ..
    ```

### アプリケーションの実行

1. フロントエンドバンドルをビルドします：
    ```sh
    pnpm run build
    ```
2. MCPサーバーを起動します：
    ```sh
    cd server
    pnpm start
    ```
2. サーバーは [http://localhost:8000/mcp](http://localhost:8000/mcp) で実行されます
3. 新しいターミナルでngrokトンネルを生成します：
    ```sh
    ngrok http 8000
    ```
3. ngrokは次の出力を返します：
    ```none
    Session Status    online
    Account           Your Account (Plan: Free)
    Update            update available (version 3.x.x, Ctrl-C to update)
    Version           3.x.x
    Region            United States (us)
    Web Interface     http://127.0.0.1:4040
    Forwarding        https://abc123def456.ngrok-free.app -> http://localhost:8000
    ```
4. サーバーコードのCSPドメインを更新します：
    * ターミナル出力からngrok URLをコピーします（例：`https://abc123def456.ngrok-free.app`）。
    * `server/index.ts` の30行目と34行目で、`https://resolvedly-pouched-nena.ngrok-free.dev` を新しいngrok URLに置き換えます。
    * `src/tealium/TealiumTracker.tsx` の134行目でも同じ更新を行います。
5. サーバーを再起動します：
    ```sh
    # 現在のサーバーを終了します（Ctrl+C）
    cd server
    pnpm start
    ```
6. 新しいURLでフロントエンドを再ビルドします：
    ```sh
    cd ..
    pnpm run build
    ```

次のアクセスポイントに注意してください：

* ローカルMCPサーバー：[http://localhost:8000/mcp](http://localhost:8000/mcp)
* ヘルスチェック：[http://localhost:8000/health](http://localhost:8000/health)
* APIエンドポイント：[http://localhost:8000/api/tealium/track](http://localhost:8000/api/tealium/track)
* 公開ngrok URL：ngrok URL + `/mcp`
* 公開API：ngrok URL + `/api/tealium/track`

### ChatGPTでアプリを追加

1. **ChatGPT > 構成 > アプリとコネクタ**に移動します。
2. **詳細構成**の下で**開発者モード**を有効にします。
3. **MCPサーバーフィールド**に**ngrok URL**を貼り付けます。

### Tealiumアプリの起動

1. プロンプトが表示されたら、`tealium-tracker` ツールを使用します。
1. Tealiumアカウント、プロファイル、環境を入力します。
1. Tealium Universalタグ (`utag.js`) がロードされ、ウェブアプリでイベントを追跡します。


<blockquote>
サードパーティのライブラリがブロックされている場合は、CSPでそのリソースを許可してください。
</blockquote>


### **サーバーサイドイベント追跡**

サーバーサイドの追跡をオンにすると、クライアントサイドの呼び出しが `/api/tealium/track` に送信され、Tealium Collect NPMモジュールを使用して追跡リクエストが行われます。



[Tealium Trace](https://docs.tealium.com/about-trace/)で結果を検証します。

