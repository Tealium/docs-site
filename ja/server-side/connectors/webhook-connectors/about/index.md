---
title: Webhookコネクタについて
description: WebhookコネクタをHTTP APIエンドポイントに接続して、イベントデータまたは訪問データを直接サービスに送信します。これは、完全なJSONペイロードを投稿するか、個々の属性をリクエストフィールドにマッピングすることによって行います。
url: https://docs.tealium.com/ja/server-side/connectors/webhook-connectors/about/
---
## 要件

* EventStream用に有効化されたTealiumアカウント（イベントデータ用）
* AudienceStream用に有効化されたTealiumアカウント（訪問データ用）

## 動作原理

Webhookコネクタは、HTTPリクエストを通じてイベントまたは訪問データをベンダーに送信します。HTTPリクエストのすべての側面を構成して、ベンダーに必要な正確なリクエストを作成できます。

## 認証

HTTPベースのWebhookコネクタに対応する認証方法は以下の通りです：

* **BasicAuth**: リクエストと共に送信されるユーザー名とパスワードを使用してWebhookリクエストを認証します。
* **OAuth2 3-Legged**: ユーザーの同意を得たフローを通じてWebhookリクエストを認証し、ユーザーに代わってアクセストークンを発行します。サービスにログインしてアクセストークンを取得する必要があります。
* **OAuth2 2-Legged**: ユーザーの関与なしにサーバー間のアクセストークンを使用してWebhookリクエストを認証します。
* **OAuth2 (2-legged) with mTLS**: サーバー間のアクセストークンとDigiCert発行の相互TLSクライアント証明書を組み合わせてWebhookリクエストを認証します。証明書はトークンリクエストのTLSハンドシェイク中に提示されます。オプションで、配信レグにもmTLSを適用できます。
* **mTLS**: DigiCert発行の相互TLSクライアント証明書を使用してWebhookリクエストを認証しますが、OAuth2トークンフローは使用しません。
* **JWT**: JSON Webトークンを使用してWebhookリクエストを認証します。

Webhook OAuth2は、OAuth 2.0認証を明示的に要求するサービスに使用されます。

詳細については、[webhook-authentication](https://docs.tealium.com/webhook-authentication/)を参照してください。


<blockquote>
JDBC互換データベースにデータを送信するためにWebhookを使用するには、[Webhook JDBC](https://docs.tealium.com/webhook-jdbc/)を参照してください。
</blockquote>


## アクション

| アクション名    | 説明    | Webhook (BasicAuth) | Webhook OAuth2 |
|:--------|:--------|:------|:-----|
| HTTPリクエストを介してイベントデータを送信  | イベントオブジェクト全体を、URLエンコードされたJSON文字列またはJSONペイロードとして送信します。     | ✓      | ✓     |
| HTTPリクエストを介して訪問データを送信 | 訪問プロファイルオブジェクト全体を、URLエンコードされたJSON文字列またはJSONペイロードとして送信します。 | ✓    | ✓      |
| HTTPリクエストを介してカスタマイズされたデータを送信（高度）    | マッピングで指定された個々のイベント/訪問属性を送信します。          | ✓      | ✓       |
| HTTPリクエストを介してバッチデータを送信  | イベントオブジェクト全体を、URLエンコードされたJSON文字列またはJSONペイロードとして送信します。     | ✓      | ✓     |
| HTTPリクエストを介してバッチカスタマイズデータを送信（高度） | マッピングで指定されたバッチイベント/訪問属性を送信します。    | ✓      | ✓          |

詳細については、[webhook-actions](https://docs.tealium.com/webhook-actions/)を参照してください。

## HTTPレスポンスクッキー

クッキーベースのセッション管理はWebブラウザで一般的ですが、ステートレスAPIと通信するサーバー間環境では一般的に推奨されません。そのため、Webhookコネクタはクッキーベースのセッションを追跡せず、HTTPレスポンスの`Set-Cookie`ヘッダー値を効果的に無視します。