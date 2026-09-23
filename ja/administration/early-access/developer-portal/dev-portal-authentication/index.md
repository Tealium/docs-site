---
title: 開発者ポータル認証
description: この記事では、OAuth2クライアント認証情報とベアラートークンを使用してTealium APIへのAPIリクエストを認証する方法について説明します。
url: https://docs.tealium.com/ja/administration/early-access/developer-portal/dev-portal-authentication/
---
Tealium APIへのアクセスにはベアラートークンが必要です。開発者ポータルは、エンドユーザーの操作が不要なサーバー間通信用に設計されたOAuth2クライアント認証情報グラントを使用します。

認証フローは以下の通りです：

1. アプリケーションがクライアントIDとクライアントシークレットをトークンエンドポイントに送信します。
1. トークンエンドポイントは認証情報を検証し、JWTアクセストークンを返します。
1. アプリケーションは、すべてのAPIリクエストの`Authorization`ヘッダーにトークンを含めます。
1. APIゲートウェイはトークンを検証し、要求された操作がトークンのスコープと一致するかを確認します。

クライアント認証情報はバックエンドサービス専用です。ブラウザやモバイルクライアントでは使用しないでください。

## 始める前に

開発者ポータルで登録されたアプリケーションからクライアントIDとクライアントシークレットが必要です。アプリケーションの作成方法については、[アプリケーション](https://docs.tealium.com/dev-portal-applications/)を参照してください。

開発者ポータルはアプリケーションを作成する際にクライアントシークレットを一度だけ表示します。保存していない場合は、認証する前に開発者ポータルでシークレットを回転させて新しいものを生成してください。

## アクセストークンのリクエスト


<blockquote>
アプリケーション詳細ページまたはAPIリファレンス画面から**トークン生成**をクリックすることで、コードを書かずにベアラートークンを生成できます。詳細については、[APIリファレンスからベアラートークンを生成する](https://docs.tealium.com/dev-portal-api-reference/#generate-a-bearer-token-from-the-api-reference)を参照してください。
</blockquote>


Tealium APIは複合スコープを持つOAuth 2.0クライアント認証情報を使用します。スコープの形式は以下の通りです：

```none
{account}:{profile}:{apiFamily}:{apiVersion}:{resource}:{action}
```

| セグメント | 説明 |
| --- | --- |
| `account` | あなたのTealiumアカウント名、例えば `tealium-corp`。 |
| `profile` | 特定のプロファイル、例えば `main`、またはアカウント内のすべてのプロファイルに対しては `*`。 |
| `apiFamily` | スコープが許可するAPI、例えば `cdp-api`。購読したAPIから取得します。 |
| `apiVersion` | そのAPIのバージョン、例えば `2026-07`、またはすべてのバージョンに対しては `*`。URLパスとは異なり、ここでは `v` プレフィックスはありません。 |
| `resource` | APIリソース、例えば `labels` や `audiences`。 |
| `action` | GETリクエストに対しては `read`、POST、PUT、DELETEリクエストに対しては `write`、管理操作に対しては `manage`。 |

スコープは付与された通りにリクエストしてください。アカウント内のすべてのプロファイルへのアクセスが許可されている場合（`*`を使用）、ワイルドカード形式をリクエストする必要があります。ワイルドカードトークンはそのアカウントの任意のプロファイルに対するリクエストを承認します。ポータルは**ベアラートークン取得**ドロワーで正確なスコープ文字列を表示するため、手作業でそれらを作成する必要はありません。

アカウント内のすべてのプロファイルへのアクセスが許可されている場合、`*`ワイルドカードを使用してリクエストします：

```bash
curl -X POST \
https://api.tealiumapis.com/oauth/token \
-u '{client_id}:{client_secret}' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=client_credentials' \
-d 'scope=tealium-corp:*:cdp-api:2026-07:labels:read'
```

特定のプロファイルへのアクセスが許可されている場合、そのプロファイルをリクエストします：

```bash
curl -X POST \
https://api.tealiumapis.com/oauth/token \
-u '{client_id}:{client_secret}' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=client_credentials' \
-d 'scope=tealium-corp:main:cdp-api:2026-07:labels:read'
```

複数のスコープをリクエストする場合、それらをスペースで区切ります：

```bash
-d 'scope=tealium-corp:*:cdp-api:2026-07:labels:read tealium-corp:*:cdp-api:2026-07:audiences:write'
```


<blockquote>
トークンには、明示的にリクエストしたスコープのみが含まれます。アプリケーションに複数のスコープが付与されている場合でも、各操作に必要なものだけを指定してください。トークンをキャッシュして、有効期限が切れるまで再利用します。APIコールごとに新しいトークンをリクエストすると、スロットリングが発生します。
</blockquote>


成功したレスポンスは以下のパラメータを含むJSONオブジェクトを返します：

| フィールド | 説明 |
| --- | --- |
| `access_token` | APIリクエストに含めるJWT。 |
| `token_type` | 常に `Bearer`。 |
| `expires_in` | トークンの有効期間（秒）。 |
| `scope` | このトークンに付与されたスコープ。 |

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "Bearer",
  "expires_in": 7200,
  "scope": "my-account:main:cdp-api:2026-07:labels:read my-account:main:cdp-api:2026-07:audiences:write"
}
```

エンジン強制API（例えばコンテキストAPI）の場合、`scope`フィールドにはリソースレベルのスコープではなくエンジンレベルのスコープが含まれます：

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "Bearer",
  "expires_in": 7200,
  "scope": "my-account:main:context-api:2026-06:e01ce645-3964-4343-9a0c-7d165e653b35"
}
```

スコープ形式の詳細については、[スコープ](https://docs.tealium.com/dev-portal-scopes/)を参照してください。

## 認証済みリクエストの作成

各APIリクエストの`Authorization`ヘッダーにアクセストークンを含めます：

```bash
curl -X GET \
https://api.tealiumapis.com/v{YYYY-MM}/{api}/accounts/tealium-corp/profiles/main/labels \
-H 'Authorization: Bearer {access_token}'
```

URLパスで任意のプロファイルへのアクセスをリクエストするためにワイルドカード (`*`) を使用します。以下の両方のリクエストは `tealium-corp:*:cdp-api:2026-07:labels:read` トークンで動作します：

```bash
curl -X GET \
https://api.tealiumapis.com/v{YYYY-MM}/{api}/accounts/tealium-corp/profiles/main/labels \
-H 'Authorization: Bearer {access_token}'

curl -X GET \
https://api.tealiumapis.com/v{YYYY-MM}/{api}/accounts/tealium-corp/profiles/staging/labels \
-H 'Authorization: Bearer {access_token}'
```

## トークンの有効期限と更新

| 項目 | 詳細 |
| --- | --- |
| 形式 | RS256で署名されたJWT。 |
| 有効期限 | トークンレスポンスの `expires_in` 値によって構成されます（7200秒、または2時間）。 |
| 更新 | 有効期限前に新しいトークンをリクエストします。クライアント認証情報フローにはリフレッシュトークンがありません。 |
| スコープクレーム | JWTには、トークンに付与された複合スコープをリストする `scope` クレームが含まれます。 |

## スコープの強制

APIゲートウェイはすべてのリクエストでスコープを検証します：

1. ゲートウェイはJWTから `scope` クレームを抽出します。
1. リクエストコンテキスト（アカウント、プロファイル、リソース、およびアクション）をトークンのスコープと照合します。
1. 一致するスコープが見つかった場合、リクエストは進行します。
1. 一致するスコープが見つからない場合、ゲートウェイは `403 Forbidden` を返します。


<blockquote>
トークンをリクエストする際、購読しているスコープのサブセットをリクエストすることができます。このスコープのサブセッティングを使用して、特定のタスクに必要な権限のみを持つトークンを生成します。
</blockquote>


### Context APIエンジン強制

エンジンレベルの認証を持つAPI、例えばContext APIの場合、ゲートウェイはアカウントとプロファイルのスコープを検証した後、追加のチェックを行います：

1. ゲートウェイはリクエストURLパスからエンジンIDを抽出します（例：`/engines/{engineId}/...`）。
1. トークンの`scope`クレームが一致するエンジンスコープを含んでいるかどうかをチェックします：`{account}:{profile}:{apiFamily}:{apiVersion}:{engineId}`。
1. トークンが正確なエンジンスコープ、エンジンワイルドカード`{account}:{profile}:{apiFamily}:{apiVersion}:*`、またはプロファイルワイルドカード`{account}:*:*`を含んでいればチェックは通過します。
1. 一致するスコープが見つからない場合、ゲートウェイは`403 Forbidden`を返し、欠けているスコープを特定する本文を含みます：

```json
{"error":"insufficient_scope","message":"Token does not contain required scope: {account}:{profile}:{apiFamily}:{apiVersion}:{engineId}"}
```

エンジンリソースでないAPIは、メッセージに複合リソーススコープを含む同じエラー封筒を返します。

アカウントとプロファイルのアクセスだけでは、エンジン強制APIには不十分です。リソースオーナーは、アプリケーションがエンジン強制エンドポイントを呼び出す前に、エンジンレベルのアクセスも許可する必要があります。

| スコープ形式 | APIタイプ | 例 |
|---|---|---|
| `{account}:{profile}:{apiFamily}:{apiVersion}:{resource}:{action}` | リソーススコープAPI | `acme:main:cdp-api:2026-07:labels:read` |
| `{account}:{profile}:{apiFamily}:{apiVersion}:{engineId}` | エンジン強制API | `acme:main:context-api:2026-06:e01ce645-3964-...` |
| `{account}:{profile}:{apiFamily}:{apiVersion}:*` | エンジン強制API（ワイルドカード） | `acme:main:context-api:2026-06:*` |

## セキュリティのベストプラクティス

* **クライアントの秘密を公開しないでください。** 環境変数やシークレットマネージャーに保存します。ソースコントロールにはコミットしないでください。
* **最小限のスコープを要求します。** 各操作に必要なスコープのみを要求します。
* **トークンが期限切れになるまでキャッシュします。** 現在のトークンが期限切れになる直前にのみ新しいトークンを要求し、すべてのAPI呼び出しで要求しないでください。
* **漏洩した場合は直ちに秘密を回転させます。** 資格情報が漏洩したと思われる場合は、開発者ポータルのアプリケーション構成を通じて直ちに回転させます。一般的な習慣として定期的に回転させます。
* **サーバーサイドのリクエストのみを使用します。** クライアント資格情報はバックエンドサービス専用です。ブラウザーやモバイルクライアントでは使用しないでください。
* **特定のエンジンを選択します。** エンジン強制APIでは、すべてのエンジンではなく特定のエンジンを選択することで、最小権限の原則に従います。

## エラー応答

| HTTPステータス | 意味 | 解決策 |
| --- | --- | --- |
| 401 Unauthorized | 無効または期限切れのトークン | 新しいアクセストークンを要求します。 |
| 403 Forbidden | トークンは有効ですが、必要なスコープが不足しています。 | サブスクリプションのスコープとアカウント/プロファイルの割り当てを確認してください。 |
| 403 Forbidden | トークンにエンジンレベルの認証がありません。 | リソースオーナーが特定のエンジンへのアクセスを許可していることを確認してください。 |
| 400 Bad Request | トークンリクエストが無効です：`grant_type`が間違っているか、必要なフィールドが欠けています。 | トークンリクエストのパラメータを確認してください。 |