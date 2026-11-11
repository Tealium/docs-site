---
title: Webhookコネクタについて
description: WebhookコネクタをHTTP APIエンドポイントに接続し、完全なJSONペイロードを送信するか、個々の属性をリクエストフィールドにマッピングすることで、イベントデータまたは訪問データをサービスに直接送信します。
url: https://docs.tealium.com/ja/server-side/connectors/webhook-connectors/about/
---
## 要件

* イベントデータ用にEvent Streamingが有効化されたTealiumアカウント
* 訪問データ用にCustomer Data Platform（CDP）が有効化されたTealiumアカウント

## 仕組み

Webhookコネクタは、HTTPリクエストを通じてイベントデータまたは訪問データをベンダーに送信します。HTTPリクエストのすべての要素を構成できるため、ベンダーが必要とするリクエストを正確に作成できます。

## 認証

HTTPベースのWebhookコネクタでは、次の認証方式がサポートされています。

* **BasicAuth**：リクエストとともに送信されるユーザー名とパスワードを使用してWebhookリクエストを認証します。
* **OAuth2 3-Legged**：ユーザーに代わってアクセストークンを発行するユーザー同意フローを通じて、Webhookリクエストを認証します。アクセストークンを取得するには、ユーザーがサービスにログインする必要があります。
* **OAuth2 2-Legged**：ユーザーの関与なしに、サーバー間アクセストークンを使用してWebhookリクエストを認証します。
* **OAuth2 (2-legged) with mTLS**：サーバー間アクセストークンと、DigiCertが発行した相互TLSクライアント証明書を組み合わせて、Webhookリクエストを認証します。この証明書は、トークンリクエスト側のTLSハンドシェイク中に提示されます。必要に応じて、配信側にもmTLSを適用できます。
* **mTLS**：OAuth2トークンフローを使用せず、DigiCertが発行した相互TLSクライアント証明書を使用してWebhookリクエストを認証します。
* **JWT**：JSON Web Tokenを使用してWebhookリクエストを認証します。

Webhook OAuth2は、OAuth 2.0認証を明示的に必要とするサービスで使用されます。

詳細については、[webhook-authentication](https://docs.tealium.com/webhook-authentication/)を参照してください。


<blockquote>
Webhookを使用してJDBC互換データベースにデータを送信する方法については、[Webhook JDBC](https://docs.tealium.com/webhook-jdbc/)を参照してください。
</blockquote>


## アクション

| アクション名 | 説明 | Webhook（BasicAuth） | Webhook OAuth2 |
|:--------|:--------|:------|:-----|
| HTTPリクエストによるイベントデータの送信 | イベントオブジェクト全体を、URLエンコードされたJSON文字列またはJSONペイロードとして送信します。 | ✓ | ✓ |
| HTTPリクエストによる訪問データの送信 | 訪問プロファイルオブジェクト全体を、URLエンコードされたJSON文字列またはJSONペイロードとして送信します。 | ✓ | ✓ |
| HTTPリクエストによるカスタムデータの送信（詳細） | マッピングで指定された個々のイベント属性または訪問属性を送信します。 | ✓ | ✓ |
| HTTPリクエストによるバッチデータの送信 | イベントオブジェクト全体を、URLエンコードされたJSON文字列またはJSONペイロードとして送信します。 | ✓ | ✓ |
| HTTPリクエストによるカスタムバッチデータの送信（詳細） | マッピングで指定されたイベント属性または訪問属性をバッチで送信します。 | ✓ | ✓ |

詳細については、[webhook-actions](https://docs.tealium.com/webhook-actions/)を参照してください。

## HTTPレスポンスCookie

Cookieベースのセッション管理はWebブラウザーでは一般的ですが、ステートレスAPIと通信するサーバー間環境では通常推奨されません。そのため、WebhookコネクタはCookieベースのセッションを追跡せず、HTTPレスポンス内の`Set-Cookie`ヘッダー値を事実上無視します。