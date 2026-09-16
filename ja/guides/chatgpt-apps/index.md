---
title: Tealium + ChatGPT アプリ
description: クライアントサイド、サーバーサイド、ハイブリッドアプローチで一貫した訪問IDを持つChatGPTアプリでのTealiumトラッキングの実装。
url: https://docs.tealium.com/ja/guides/chatgpt-apps/
---
## はじめに

Tealiumは、ブラウザ、ウィジェット、カスタムChatGPTインターフェースでアプリのような体験のためのデータ基盤を提供します。プラットフォーム全体で一貫したデータ収集と訪問ID管理をサポートします。

このChatGPTソリューションは、MCPフレンドリーな設計を使用して以下を実現します：

* 主要なインタラクション（製品閲覧、ボタンクリック、購入）の追跡。
* クライアント、サーバー、ChatGPTコンテキスト間でのIDの統合。
* Tealium Collectを使用したリアルタイムでのイベントストリーミング。
* Tealium Context APIとTealium AudienceStreamを使用した体験のパーソナライズ。

## オプション 1: クライアントサイドトラッキング

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

## オプション 2: サーバーサイドトラッキング

サーバーサイドトラッキングは、[HTTP API](https://docs.tealium.com/ja/platforms/http-api/endpoint/)を使用してイベントを直接Tealiumに送信します。クライアントサイドソリューションと同様に、追加のユーティリティ関数を使用して独自の匿名訪問IDを生成して永続化します。

次のシナリオでこのアプローチを推奨します：

* CSP制限により外部JavaScriptのロードが防止される場合。
* 購入などの重要なイベントのデータトラッキングを保証するため。

以下のサーバーサイドトラッキングソリューションが利用可能です：

### Node.jsアプリ（推奨）

Node.jsソリューションには、匿名訪問IDを生成して永続化するクライアントコードと、追跡されたイベントのためのラッパー関数の呼び出しが含まれています。

たとえば、次のサンプルコードは訪問IDを生成し、顧客が購入を完了したときにアプリから取得される`order`オブジェクトを使用して注文追跡リクエストをサーバーに送信します。

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
    res.status(500).json({ error: 'Tracking failed' });
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

ハイブリッドアプローチは、クライアントサイドソリューションを使用して `interface_loaded`、`view_pdp`、`button_click` などのインタラクションイベントを追跡し、サーバーサイドソリューションを使用して `purchase` などの権威あるイベントを追跡します。このアプローチを推奨します。


<blockquote>
ハイブリッドソリューションを実行するときは、iQプロファイルでTealium Collectタグを読み込まないでください。これにより、イベントの重複追跡が防止されます。
</blockquote>


## 訪問のアイデンティティ

正確な追跡と統一された訪問プロファイルを確保するために、クライアントサイドとサーバーサイドのイベントの両方で同じ匿名訪問IDを常に使用してください。このアプローチは、ChatGPT、ウェブ、モバイルを通じて単一の訪問アイデンティティを維持し、一貫した追跡とリアルタイムのパーソナライゼーションを可能にします。


<blockquote>
利用可能な場合は、`customer_id` や `email_address_hash` などの既知のユーザー識別子を別のパラメータとして含めることをお勧めしますが、これらの値を `tealium_visitor_id` で置き換えることはしないでください。
</blockquote>


## MCP統合（オプショナル）

サーバーからシンプルなMCPツールを公開して、ChatGPTが会話ロジックを処理できるようにします。このアプローチでは、サーバーが形式、アイデンティティ、ポリシーを強制します。

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

## Context API MCP

アプリに [Context API MCP server](https://docs.tealium.com/context-api-mcp-server/) を追加してパーソナライゼーションを有効にします。

**例のフロー:**

1. イベント `view_pdp`, `button_click`, `purchase` を追跡します。
2. **AudienceStream** が訪問プロファイルを構築します。
3. Chat UI（またはMCPツール）が `tealium_visitor_id` で **Context API** を照会します。
4. 応答は（推奨事項、オファー、トーンなど）適応します。

## データプライバシーとコンプライアンス

このアプリは、以下の機能を通じてデータプライバシーとコンプライアンスをサポートします：

* Tealium iQ Consent Managerを通じた同意駆動型アクティベーション。
* データを送信する前に省略またはハッシュ化することによるPIIガバナンス。
* 地域コンプライアンス（GDPR、CCPA、データ居住）。