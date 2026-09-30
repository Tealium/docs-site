---
title: SCIM APIについて
description: SCIMプロビジョニングを使用して、アイデンティティプロバイダからTealiumアカウントにユーザーを同期する方法を学びます。
url: https://docs.tealium.com/ja/api/v3/scim-api/about/
---
## 仕組み

System for Cross-domain Identity Management (SCIM)は、クラウドアプリ間でユーザーアカウントの作成、更新、削除を自動化し、簡素化する標準です。

SCIMプロビジョニングを使用して、アイデンティティプロバイダ（IdP）からTealiumに自動的にユーザーを同期します。SCIMはオンボーディング中に適切なアクセス権を持つユーザーを作成し、アイデンティティプロバイダでユーザーが非プロビジョニングされたときにTealiumアクセスを削除することで、一貫したオフボーディングを保証し、不正アクセスを防ぎます。

IdPにSCIMプロビジョニングコネクタを使用するか、直接SCIM APIを呼び出します。

## 認証

TealiumのSCIM統合は、アプリケーションとの認証に長期間有効なベアラートークンを使用します。このベアラートークンをOAuthベアラートークンとして使用して、ユーザープロビジョニングアプリケーションを構成します。

このベアラートークンはすべてのSCIM API呼び出しを認証します。

APIキーとベアラートークンはそれを生成したユーザーにリンクされています。通常のユーザーアカウントが利用できなくなった場合のアクセス問題を防ぐために、`scim@example.com`のような専用のサービスユーザー（個人にリンクされていないアカウント）を使用します。

ベアラートークンを生成するには：

1. 専用のサービスユーザーとしてTealiumにログインします。
1. [APIキー](https://docs.tealium.com/api-keys/)を生成します。
1. 次のcURLコマンドを使用して、長期間有効なトークンエンドポイントを呼び出し、ベアラートークンを生成します。プレースホルダーをアカウント名、プロファイル名、専用ユーザー名、APIキーに置き換えてください：

```bash
curl --location 'https://developer.tealiumapis.com/v1/auth-long-lived/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'account={ACCOUNT}' \
--data-urlencode 'profile=main' \
--data-urlencode 'username={USERNAME@EXAMPLE.COM}' \
--data-urlencode 'key={API_KEY}'
```

トークンは次の例のようになります：

```json
{
  "access_token":"eyJhbG...53UHg",
  "token_type": "Bearer",
  "expires_in": 7776000,
  "scope": "profile email"
}
```

トークンは90日後に期限切れになります。必要に応じて再生成するか、トークンが期限切れになる前にトークンを無効にするためにトークンを無効にするエンドポイントを使用します。

トークン生成エンドポイントは、IPアドレスごとに分あたり10リクエストのレート制限があります。

トークンの生成に関する支援が必要な場合や、権限に関する質問がある場合は、[Tealiumサポート](https://docs.tealium.com/support/)に連絡してください。

## トークンを無効にする

トークンが期限切れになる前にすぐにトークンを無効にするには、無効にするエンドポイントを使用します。セキュリティインシデントに対応するとき、資格情報をローテーションするとき、または統合を廃止するときにトークンを無効にします。

無効化は数秒以内に有効になり、永続的です。トークンを無効にすることは元に戻すことができません。アクセスを復元するには新しいトークンを生成します。

トークンを無効にするには、それを生成するのに使用した同じ資格情報を使用して、次のエンドポイントを呼び出します：

```bash
curl --location 'https://developer.tealiumapis.com/v1/auth-long-lived/revoke' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'token={ACCESS_TOKEN}' \
--data-urlencode 'account={ACCOUNT}' \
--data-urlencode 'profile=main' \
--data-urlencode 'username={USERNAME@EXAMPLE.COM}' \
--data-urlencode 'key={API_KEY}'
```

### トークンを無効にするパラメータ

| パラメータ | 必須 | タイプ | 説明 |
| --- | --- | --- | --- |
| `token` | はい | 文字列 | 無効にするアクセストークン |
| `account` | はい | 文字列 | トークンを生成するために使用されたアカウント |
| `profile` | はい | 文字列 | トークンを生成するために使用されたプロファイル |
| `username` | はい | 文字列 | トークンを生成するために使用されたユーザー名 |
| `key` | はい | 文字列 | トークンを生成するために使用されたAPIキー |
| `token_type_hint` | いいえ | 文字列 | オプションのヒント："access_token"または"refresh_token" |

### 応答

成功した無効化はHTTP 200を返し、レスポンスボディは空です。

エンドポイントは、トークンがすでに期限切れであったり、以前に無効にされていた場合でも200 OKを返します。すでに無効なトークンを無効にすることはエラーではありません。

401 Unauthorizedの応答は、提供された資格情報がトークンを生成するために使用された資格情報と一致しないことを示します。

無効にするエンドポイントは、IPアドレスごとに分あたり20リクエストのレート制限があります。

## エンドポイントと権限

TealiumのSCIM実装は、次のHTTPメソッドをサポートしています：

| メソッド | 説明                          | Tealiumの権限 |
| ------ | ------------------------------------ | --------------------------- |
| `POST`   | ユーザーまたはカスタムグループを作成します。              | ユーザー管理者またはアカウント管理者 |
| `GET`    | ユーザーの詳細、グループの詳細を取得するか、ユーザーやグループのリストを表示します。 | すべてのアカウントユーザー |
| `PUT`    | ユーザーまたはグループメンバーシップを置き換えます。                      | ユーザー管理者またはアカウント管理者 |
| `DELETE` | ユーザーまたはカスタムグループを削除します。                       | ユーザー管理者またはアカウント管理者 |
| `PATCH`  | ユーザーまたはグループメンバーシップを部分的に更新します。             | ユーザー管理者またはアカウント管理者 |

## グループ

SCIM APIは、組み込みグループとカスタムグループの2種類のグループを公開します。

SCIMはカスタムグループを作成し、両方のタイプのグループメンバーシップを管理できますが、グループの権限を変更することはできません。グループの権限を構成するには、Tealium UIを使用する必要があります。

## 組み込みグループ

組み込みグループは、[Tealium管理ロール](https://docs.tealium.com/admin-roles/)に対応するシステムレベルのグループであり、すべてのアカウントに存在し、SCIMを通じて作成、名前変更、削除することはできません。

SCIMの`/Groups`エンドポイントで利用可能な次の組み込みグループがあります：

| グループ名 | 説明 |
| --- | --- |
| Account Admins | 全アカウント管理権限 |
| User Admins | ユーザー管理権限 |
| Privacy Admins | プライバシーおよび同意管理権限 |
| Technical Admins | 技術および統合権限 |
| Profile Admins | プロファイルレベルの管理権限 |
| Standard User | 基本的な読み取り専用アクセス（Account Viewersの別名） |


<blockquote>
`Standard User`グループは内部の`Account Viewers`グループの別名です。両方のグループは同じUUIDを共有しています。`displayName eq "Standard User"`でフィルタリングするとこのグループに一致しますが、`Account Viewers`でフィルタリングすると結果はゼロになります。
</blockquote>


### 継承グループ

特定の管理グループにユーザーを追加すると、継承グループのメンバーシップが自動的に付与されます：

| グループに追加 | 自動的に追加される |
| --- | --- |
| Account Admins | User Admins, Privacy Admins, Technical Admins, Profile Admins + PIIアクセス |
| User Admins | Technical Admins + PIIアクセス |
| Privacy Admins | User Admins, Technical Admins + PIIアクセス |
| Technical Admins | （なし） |
| Profile Admins | （なし） |
| Standard User | （なし） |


<blockquote>
Account Admins、User Admins、またはPrivacy Adminsのメンバーシップは、内部のPIIグループ（PII Admins/PII Viewers）へのメンバーシップを自動的に付与します。セキュリティ上の理由から、これらの内部グループはSCIM APIでは表示されません。
</blockquote>


### グループ削除の動作

管理グループからユーザーを削除すると、継承グループからも自動的に削除されます：

* **Account Admins**：User Admins, Privacy Admins, Technical Admins, Profile Adminsから削除し、PIIアクセスを取り消します。
* **User Admins**：Technical Adminsから削除し、PIIアクセスを取り消します。
* **Privacy Admins**：User Admins, Technical Adminsから削除し、PIIアクセスを取り消します。
* **Technical Admins**：自動削除なし。
* **Profile Admins**：自動削除なし。

### 組み込みグループの保護

組み込みグループには次の制限があります：

* SCIM PATCH操作で名前を変更することはできません。
* SCIM DELETE操作で削除することはできません。


<blockquote>
組み込みグループと一致する`displayName`を持つカスタムグループを作成または更新すると、HTTP 400エラーが返されます。
</blockquote>

## カスタムグループ

カスタムグループはTealium UIで作成された権限グループです。これらはSCIMの`/Groups`エンドポイントで組み込みグループと並んで表示されます。

SCIMはカスタムグループに対して以下の操作をサポートしています：

* 初期メンバーシップでカスタムグループを作成する（`POST`）。
* カスタムグループにユーザーを追加または削除する（`PATCH`, `PUT`）。
* カスタムグループの名前を変更する（`PATCH`, `PUT`）。
* カスタムグループを削除する（`DELETE`）。

SCIMはカスタムグループの権限を構成または変更することはできません。SCIMを通じてグループを作成した後、Tealium UIを使用して[グループ権限](https://docs.tealium.com/permission-groups/)を構成してください。