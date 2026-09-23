---
title: Tealium Developer Portalの使い方
description: アプリケーションを作成し、Tealium APIに登録し、アクセストークンを取得し、最初の認証済みAPIコールを行います。
url: https://docs.tealium.com/ja/administration/early-access/developer-portal/dev-portal-getting-started/
---
このチュートリアルでは、サインインから最初の認証済みAPIコールを行うまでの完全なセットアップフローを説明します。開始する前に、[Tealium Developer Portalについて](https://docs.tealium.com/dev-portal-about/)を読んで、アプリケーション、登録、スコープ、トークンがどのように関連しているかを理解してください。

## サインイン

[app.tealiumapis.com](https://app.tealiumapis.com/)にアクセスし、アカウントタイプに合ったログイン方法を選択してください：

* **Tealiumユーザーとしてログイン：** 既存のTealiumアカウントを持つユーザー向け。Tealium SSOまたはパスワード認証を使用します。
* **Developer Portalユーザーとしてログイン：** Tealiumアカウントを持っていない外部開発者向け。Developer Portalユーザーアカウントを持っていない場合は、`/register`にアクセスして、名、姓、メールアドレスでサインアップしてください。


<blockquote>
アーリーアクセス中は、セルフサービスの登録が無効になっている場合があります。"Registration Unavailable"と表示された場合は、Tealiumに連絡してアクセスをリクエストしてください。
</blockquote>


![](https://docs.tealium.com/images/api/developer-portal/01-sign-in.png)

認証後、ダッシュボードにリダイレクトされます。ダッシュボードでは、利用可能なAPI、アプリケーション、アクティブな登録、最近のAPIトラフィックの概要が表示されます。

![](https://docs.tealium.com/images/api/developer-portal/02-dashboard.png)

## ステップ1: APIカタログを閲覧する

アプリケーションを作成する前に、必要なAPIを特定するためにAPIカタログを閲覧してください。

左サイドバーの**APIカタログ**をクリックするか、ダッシュボードから**APIカタログを閲覧**をクリックしてください。

![](https://docs.tealium.com/images/api/developer-portal/03-api-catalog.png)

カタログでは、各APIがカードで表示され、その名前、バージョン、サポート終了日、簡単な説明が示されます。Model Context Protocol（MCP）をサポートするAPIにはMCPバッジが表示されます。

検索ボックスを使用して、名前や説明でフィルタリングします。**すべてのバージョン**ドロップダウンを使用してバージョンでフィルタリングするか、**MCP**トグルを使用してMCP対応のAPIのみを表示します。

APIカードをクリックすると、その詳細ページが開きます。詳細ページはタブで整理されています：

* **説明：** APIの説明と概要。
* **概要：** バージョン、ステータス、所有者情報。
* **プラン：** 利用可能な登録プランとそのセキュリティタイプ。
* **RESTエンドポイント：** リソースごとにグループ化されたすべてのエンドポイント。グループを展開して個々の操作を表示します。
* **MCP：** 利用可能なMCPツール、パラメータ、および予想される動作。
* **ドキュメント：** APIリファレンスドキュメントへのリンク。

![](https://docs.tealium.com/images/api/developer-portal/04-api-detail-rest-endpoints.png)

詳細については、[APIカタログ](https://docs.tealium.com/dev-portal-api-catalog/)を参照してください。

## ステップ2: アプリケーションを作成し、登録する

1. 左サイドバーの**アプリケーション**をクリックし、**アプリケーションを作成**をクリックします。

   ![](https://docs.tealium.com/images/api/developer-portal/05-applications.png)

1. アプリケーションの名前とオプションの説明を入力します。この統合が何をするかを反映する名前を選んでください。例えば、`Analytics Dashboard`や`Data Pipeline`などです。**作成**をクリックします。

   ![](https://docs.tealium.com/images/api/developer-portal/06-create-application-form.png)

1. 登録ウィザードで、登録したいAPIを選択し、**次へ: スコープを構成**をクリックします。

   ![](https://docs.tealium.com/images/api/developer-portal/07-subscription-wizard-api-selection.png)

1. 各APIセクションを展開して利用可能なスコープを表示します。アプリケーションが必要とするリソースとアクションのペアをチェックします。統合に必要なスコープのみをリクエストしてください。

   ![](https://docs.tealium.com/images/api/developer-portal/08-subscription-wizard-scopes.png)

1. Tealiumユーザーとしてログインしている場合、**アカウントプロファイル**ステップが表示されます。この登録がカバーするTealiumアカウントとプロファイルを選択します。ポータルは、公開権限を持っているプロファイルのみを表示します。**次へ: エンジンを選択**または**次へ: レビュー**をクリックします。
   
<blockquote>
外部開発者はアカウントプロファイルとエンジンのステップをスキップします。彼らは自身のTealiumアカウントを持っていません。リソース所有者によってTealiumの顧客リソースへのアクセスが許可されます。[サードパーティアプリアクセス](https://docs.tealium.com/dev-portal-third-party-app-access/)を参照してください。
</blockquote>

   ![](https://docs.tealium.com/images/api/developer-portal/09-subscription-wizard-account-profiles.png)
1. Context APIなどのエンジンアクセスが必要なAPIを選択した場合、**エンジンを選択**ステップが表示されます。エンジンはアカウントとプロファイルごとにグループ化されています。特定のエンジンを選択するか、後で作成されるエンジンも自動的に含めるために**すべてのエンジン（現在および将来）**を選択します。無効になっているエンジンも将来の使用のために選択できます。このステップをスキップして、後でエンジンアクセスを構成することもできます。
1. 構成を確認して**登録を作成**をクリックします。
1. **アプリケーションを表示**をクリックして、新しいアプリケーションの詳細ページに移動します。

   ![](https://docs.tealium.com/images/api/developer-portal/10-application-detail.png)

詳細については、[アプリケーション](https://docs.tealium.com/dev-portal-applications/)を参照してください。

Tealiumの顧客のアカウントとプロファイルへのアクセスが必要な外部開発者の場合：

1. Tealiumの連絡先に**アプリケーションID**を共有します。
1. Tealiumユーザーは、[サードパーティアプリアクセス](https://docs.tealium.com/dev-portal-third-party-app-access/)ページからアカウント、プロファイル、エンジンへのアプリケーションアクセスを許可します。
1. アクセスが許可されると、トークンにはそれらのリソースのスコープが含まれます。

### 資格情報を保存する

アプリケーションの詳細ページには、**クライアントID**と**アプリケーションID**が表示されます。作成直後に表示される確認画面からクライアントシークレットをコピーします。その画面を離れると、シークレットはもう表示されません。


<blockquote>
ナビゲートする前にクライアントシークレットをコピーしてください。シークレットマネージャーや環境変数に保存します。資格情報をソースコントロールにコミットしないでください。保存していない場合は、**シークレットを回転**して新しいものを生成します。古いシークレットは直ちに無効になります。
</blockquote>

## ステップ3: アクセストークンをリクエストする

アプリケーション画面から、またはクライアントIDとクライアントシークレットを使用してトークンエンドポイントからベアラートークンをリクエストすることでアクセストークンを生成します。TealiumのAPIはOAuth2クライアントクレデンシャルグラントを使用します。

スコープは `{account}:{profile}:{apiFamily}:{apiVersion}:{resource}:{action}` の形式を使用します。詳細については、[スコープ](https://docs.tealium.com/dev-portal-scopes/)を参照してください。

```bash
curl -X POST \
https://api.tealiumapis.com/oauth/token \
-u '{client_id}:{client_secret}' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=client_credentials' \
-d 'scope={space-separated-scopes}'
```

例えば：

```bash
curl -X POST \
https://api.tealiumapis.com/oauth/token \
-u 'a1b2c3d4e5f6:s3cr3tk3y' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'grant_type=client_credentials' \
-d 'scope=acme-corp:main:cdp-api:2026-07:audiences:read acme-corp:main:cdp-api:2026-07:labels:read'
```

成功したレスポンスはJSONオブジェクトを返します：

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "Bearer",
  "expires_in": 7200,
  "scope": "my-account:main:cdp-api:2026-07:audiences:read my-account:main:cdp-api:2026-07:labels:read"
}
```

`access_token` の値はあなたのベアラートークンです。これは7200秒（2時間）後に期限切れになります。キャッシュして後続のリクエストで再利用してください。APIコールごとに新しいトークンをリクエストすると、スロットリングが発生します。

詳細については、[認証](https://docs.tealium.com/dev-portal-authentication/)を参照してください。

## ステップ4: APIコールを行う

各リクエストの `Authorization` ヘッダーにアクセストークンを含めます：

```bash
curl -X GET \
https://api.tealiumapis.com/{version}/{api}/{api-endpoint} \
-H 'Authorization: Bearer {access_token}' \
-H 'Accept: application/json'
```

成功したレスポンスは `2xx` ステータスコードとデータを返します。リクエストが失敗した場合は、エラーコードと解決策の完全なリストについて [エラーレスポンス](https://docs.tealium.com/dev-portal-authentication/#error-responses) を参照してください。

### 開発者ポータルからテストする

コードを書かずに開発者ポータルから直接APIコールをテストすることもできます。

1. 左サイドバーの **API Reference** に移動し、APIを開きます。
1. アクションを展開し、エンドポイントを選択します。
1. 画面の右下隅にある **⋮** アイコンをクリックし、次に **Bearer Token** キーアイコンをクリックします。
1. ドロップダウンからアプリケーションを選択し、**Generate Token** をクリックします。
1. **Copy Token** をクリックし、ダイアログを閉じます。
1. アクション画面の **Token** フィールドにトークンを貼り付け、必要なパラメータを入力し、**Send API Request** をクリックします。

![](https://docs.tealium.com/images/api/developer-portal/11-api-reference-bearer-token.png)

詳細については、[APIリファレンスからベアラートークンを生成する](https://docs.tealium.com/dev-portal-api-reference/#generate-a-bearer-token-from-the-api-reference)を参照してください。