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

このアプローチは、Tealium iQの専用プロファイルからの標準的な[Universal Tag (`utag.js`)](/ja/platforms/javascript/)インストールを使用します。唯一の違いは、`utag.js`によって生成された匿名IDに依存しないため、独自のIDを生成して永続化することです。

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
&lt;script&gt;
  // Tealium iQをロード
  (function(a,b,c,d){
    a=&#39;https://tags.tiqcdn.com/utag/[ACCOUNT]/[PROFILE]/[ENVIRONMENT]/utag.js&#39;;
    b=document;c=&#39;script&#39;;d=b.createElement(c);d.src=a;
    d.type=&#39;text/java&#39;&#43;c;d.async=true;
    a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
  })();

  // 32文字の小文字英数字の訪問IDを生成
  function generateTealiumVisitorId() {
    const chars = &#39;abcdefghijklmnopqrstuvwxyz0123456789&#39;;
    return Array.from({ length: 32 }, () =&gt; chars[Math.floor(Math.random() * chars.length)]).join(&#39;&#39;);
  }

  // 訪問IDを取得または作成して永続化
  let tealium_visitor_id = localStorage.getItem(&#39;tealium_visitor_id&#39;);
  if (!tealium_visitor_id) {
    tealium_visitor_id = generateTealiumVisitorId();
    localStorage.setItem(&#39;tealium_visitor_id&#39;, tealium_visitor_id);
  }

  // アプリ初期化
  utag.track(&#39;event&#39;, {
    &#39;tealium_event&#39;: &#39;interface_loaded&#39;,
    &#39;app_version&#39;: &#39;2.1.0&#39;,
    &#39;user_tier&#39;: &#39;enterprise&#39;,
    &#39;tealium_visitor_id&#39;: tealium_visitor_id
  });

  // PDPビュー
  function trackViewPdp(product) {
    utag.track(&#39;view&#39;, {
      &#39;tealium_event&#39;: &#39;view_pdp&#39;,
      &#39;product_id&#39;: product.id,
      &#39;product_name&#39;: product.name,
      &#39;category&#39;: product.category,
      &#39;price&#39;: product.price,
      &#39;currency&#39;: product.currency || &#39;USD&#39;,
      &#39;tealium_visitor_id&#39;: tealium_visitor_id
    });
  }

  // ボタンクリック
  function trackButtonClick(button) {
    utag.track(&#39;link&#39;, {
      &#39;tealium_event&#39;: &#39;button_click&#39;,
      &#39;button_id&#39;: button.id,
      &#39;button_text&#39;: button.text,
      &#39;location&#39;: button.location || &#39;pdp&#39;,
      &#39;app_version&#39;: &#39;2.1.0&#39;,
      &#39;tealium_visitor_id&#39;: tealium_visitor_id
    });
  }
&lt;/script&gt;
```

## オプション2：サーバーサイドトラッキング

サーバーサイドトラッキングは、[HTTP API](/ja/platforms/http-api/endpoint/)を使用してイベントを直接Tealiumに送信します。クライアントサイドソリューションと同様に、独自の匿名訪問IDを生成して永続化するための追加のユーティリティ関数を使用します。

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
  const chars = &#39;abcdefghijklmnopqrstuvwxyz0123456789&#39;;
  return Array.from({ length: 32 }, () =&gt; chars[Math.floor(Math.random() * chars.length)]).join(&#39;&#39;);
}

// 訪問IDを取得または作成して永続化
let tealium_visitor_id = localStorage.getItem(&#39;tealium_visitor_id&#39;);
if (!tealium_visitor_id) {
  tealium_visitor_id = generateTealiumVisitorId();
  localStorage.setItem(&#39;tealium_visitor_id&#39;, tealium_visitor_id);
}

async function trackPurchaseServer(order) {
  await fetch(&#39;/api/tealium/track&#39;, {
    method: &#39;POST&#39;,
    headers: { &#39;Content-Type&#39;: &#39;application/json&#39; },
    body: JSON.stringify({
      &#39;tealium_event&#39;: &#39;purchase&#39;,
      &#39;tealium_visitor_id&#39;: tealium_visitor_id,
      &#39;order_id&#39;: order.id,
      &#39;order_total&#39;: order.total,
      &#39;currency&#39;: order.currency || &#39;USD&#39;,
      &#39;items&#39;: order.items
    })
  });
}
```

次のサンプルサーバーサイドコードは、トラッキングコールを受け入れるエンドポイントを構成し、[Tealium for Node.js](/ja/platforms/node/install/)を使用してそれらのイベントをTealium Collectに転送します。

```js
// npm i tealium-collect express
const express = require(&#39;express&#39;);
const TealiumCollect = require(&#39;tealium-collect&#39;);
const app = express();
app.use(express.json());

const tealium = new TealiumCollect({
  &#39;account&#39;: &#39;your-account&#39;,
  &#39;profile&#39;: &#39;chatgpt-app&#39;,
  &#39;environment&#39;: &#39;prod&#39;
});

app.post(&#39;/api/tealium/track&#39;, async (req, res) =&gt; {
  try {
    const tealium_visitor_id = req.body.tealium_visitor_id;

    if (!/^[a-z0-9]{32}$/.test(tealium_visitor_id || &#39;&#39;)) {
      return res.status(400).json({ error: &#39;Invalid or missing tealium_visitor_id&#39; });
    }

    const allowed = new Set([&#39;interface_loaded&#39;,&#39;view_pdp&#39;,&#39;button_click&#39;,&#39;purchase&#39;]);
    if (!allowed.has(req.body.tealium_event)) {
      return res.status(400).json({ error: &#39;Unsupported event type&#39; });
    }

    await tealium.track({
      ...req.body,
      tealium_visitor_id,
      &#39;timestamp&#39;: req.body.timestamp || new Date().toISOString()
    });

    res.status(204).end();
  } catch (e) {
    console.error(&#39;Tealium track error:&#39;, e);
    res.status 500).json({ error: &#39;Tracking failed&#39; });
  }
});

app.listen(3000, () =&gt; console.log(&#39;Tealium server listening on 3000&#39;));
```
### ブラウザアプリ

`&lt;script&gt;` タグを埋め込むことができるブラウザアプリでこのアプローチを使用します。このコードは `fetch()` と [HTTP API](/ja/platforms/http-api/endpoint/) を使用してイベントを直接 Tealium に送信し、匿名訪問 ID を生成および保持するための同じユーティリティメソッドを使用します。

```html
&lt;script&gt;
  // 32文字の小文字英数字の訪問IDを生成
  function generateTealiumVisitorId() {
    const chars = &#39;abcdefghijklmnopqrstuvwxyz0123456789&#39;;
    return Array.from({ length: 32 }, () =&gt; chars[Math.floor(Math.random() * chars.length)]).join(&#39;&#39;);
  }

  // 訪問IDを取得または作成して保持
  let tealium_visitor_id = localStorage.getItem(&#39;tealium_visitor_id&#39;);
  if (!tealium_visitor_id) {
    tealium_visitor_id = generateTealiumVisitorId();
    localStorage.setItem(&#39;tealium_visitor_id&#39;, tealium_visitor_id);
  }

  async function sendCollectEvent(payload) {
    const base = {
      &#39;tealium_account&#39;: &#39;your-account&#39;,
      &#39;tealium_profile&#39;: &#39;chatgpt-app&#39;,
      &#39;tealium_visitor_id&#39;: tealium_visitor_id,
      &#39;timestamp&#39;: new Date().toISOString()
    };

    await fetch(&#39;https://collect.tealiumiq.com/event&#39;, {
      &#39;method&#39;: &#39;POST&#39;,
      &#39;headers&#39;: { &#39;Content-Type&#39;: &#39;application/json&#39; },
      &#39;body&#39;: JSON.stringify({ ...base, ...payload })
    });
  }

  function trackViewPdpServer(product) {
    return sendCollectEvent({
      &#39;tealium_event&#39;: &#39;view_pdp&#39;,
      &#39;product_id&#39;: product.id,
      &#39;product_name&#39;: product.name,
      &#39;product_category&#39;: product.category,
      &#39;product_price&#39;: product.price,
      &#39;product_currency&#39;: product.currency || &#39;USD&#39;
    });
  }

  function trackButtonClickServer(button) {
    return sendCollectEvent({
      &#39;tealium_event&#39;: &#39;button_click&#39;,
      &#39;button_id&#39;: button.id,
      &#39;button_text&#39;: button.text,
      &#39;location&#39;: button.location || &#39;pdp&#39;,
      &#39;app_version&#39;: &#39;2.1.0&#39;
    });
  }
&lt;/script&gt;
```

## オプション3: ハイブリッド（推奨）

ハイブリッドアプローチは、クライアントサイドソリューションを使用して `interface_loaded`、`view_pdp`、`button_click` などのインタラクションイベントを追跡し、サーバーサイドソリューションを使用して `purchase` などの権威あるイベントを追跡します。このアプローチを使用することで、アプリの追跡を最も完全に行うことができます。

ハイブリッドソリューションを実行する際は、iQプロファイルでTealium Collectタグをロードしないでください。これにより、イベントの重複追跡が防止されます。

## 訪問のアイデンティティ

正確な追跡と統一された訪問プロファイルを確保するためには、クライアントサイドとサーバーサイドのイベントの両方で同じ匿名訪問IDを常に使用してください。このアプローチにより、ChatGPT、ウェブ、モバイルを通じて単一の訪問アイデンティティが維持され、一貫した追跡とリアルタイムのパーソナライゼーションが可能になります。

利用可能な場合は、`customer_id` や `email_address_hash` などの既知のユーザー識別子を別のパラメータとして含めることをお勧めしますが、これらの値を `tealium_visitor_id` で置き換えることはしないでください。

## MCP統合（オプション）

サーバーからChatGPTが呼び出すシンプルなMCPツールを公開します。このアプローチにより、ChatGPTは会話ロジックを処理し、サーバーは形式、アイデンティティ、ポリシーを強制します。

**ツール:** `tealium-track-event`

**例のスキーマ:**

```json
{
  &#34;account&#34;: &#34;your-account&#34;,
  &#34;profile&#34;: &#34;chatgpt-app&#34;,
  &#34;environment&#34;: &#34;prod&#34;,
  &#34;event&#34;: &#34;view_pdp&#34;,
  &#34;visitorId&#34;: &#34;abcdefghijklmnopqrstuvwxyz012345&#34;,
  &#34;data&#34;: {
    &#34;product_id&#34;: &#34;widget-123&#34;,
    &#34;price&#34;: 29.99,
    &#34;currency&#34;: &#34;USD&#34;
  }
}
```

**検証:**

* `visitorId` は正規表現 `/^[a-z0-9]{32}$/` に一致する必要があります。
* `event` は許可されたイベントリスト（`interface_loaded`, `view_pdp`, `button_click`, `purchase`）に含まれている必要があります。

## Moments API MCP

[Moments MCP server]() をアプリに追加してパーソナライゼーションを有効にします。

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

* Node.js 18&#43; (LTS)
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
    Forwarding        https://abc123def456.ngrok-free.app -&gt; http://localhost:8000
    ```
4. サーバーコードのCSPドメインを更新します：
    * ターミナル出力からngrok URLをコピーします（例：`https://abc123def456.ngrok-free.app`）。
    * `server/index.ts` の30行目と34行目で、`https://resolvedly-pouched-nena.ngrok-free.dev` を新しいngrok URLに置き換えます。
    * `src/tealium/TealiumTracker.tsx` の134行目でも同じ更新を行います。
5. サーバーを再起動します：
    ```sh
    # 現在のサーバーを終了します（Ctrl&#43;C）
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
* 公開ngrok URL：ngrok URL &#43; `/mcp`
* 公開API：ngrok URL &#43; `/api/tealium/track`

### ChatGPTでアプリを追加

1. **ChatGPT &gt; 構成 &gt; アプリとコネクタ**に移動します。
2. **詳細構成**の下で**開発者モード**を有効にします。
3. **MCPサーバーフィールド**に**ngrok URL**を貼り付けます。

### Tealiumアプリの起動

1. プロンプトが表示されたら、`tealium-tracker` ツールを使用します。
1. Tealiumアカウント、プロファイル、環境を入力します。
1. Tealium Universalタグ (`utag.js`) がロードされ、ウェブアプリでイベントを追跡します。

サードパーティのライブラリがブロックされている場合は、CSPでそのリソースを許可してください。

### **サーバーサイドイベント追跡**

サーバーサイドの追跡をオンにすると、クライアントサイドの呼び出しが `/api/tealium/track` に送信され、Tealium Collect NPMモジュールを使用して追跡リクエストが行われます。



[Tealium Trace]()で結果を検証します。

