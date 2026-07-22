---
title: SCIM APIについて
description: SCIMプロビジョニングを使用して、IDプロバイダーからTealiumアカウントにユーザーを同期する方法を学びます。
url: https://docs.tealium.com/ja/api/v3/scim-api/about/
--- 
## 仕組み

クロスドメインアイデンティティ管理（SCIM）は、クラウドアプリケーション間でユーザーアカウントの作成、更新、削除を自動化し、簡素化するための標準です。

IDプロバイダー（IdP）からTealiumにユーザーを自動的に同期するためにSCIMプロビジョニングを使用します。SCIMはオンボーディング中に適切なアクセス権を持つユーザーを作成し、IDプロバイダーでユーザーが非プロビジョニングされたときにTealiumアクセスを削除することで、一貫したオフボーディングを保証し、不正アクセスを防ぎます。

IdPにSCIMプロビジョニングコネクタを使用するか、SCIM APIを直接呼び出します。

## 認証

TealiumのSCIM統合は、アプリケーションとの認証に長期間有効なベアラートークンを使用します。このベアラートークンをOAuthベアラートークンとして使用し、ユーザープロビジョニングアプリケーションを構成します。

すべてのSCIM API呼び出しは、このベアラートークンで認証されます。


<blockquote>
APIキーとベアラートークンは、それを生成したユーザーにリンクされています。必要なTealium権限を持つ専用のサービスユーザーを使用してください。サービスユーザーは、人物にリンクされていないリソースを管理するために使用されるユーザーアカウントです。このアプローチは、通常のユーザーアカウントが利用できなくなった場合のアクセス問題を防ぎます。
</blockquote>


ベアラートークンを生成するには：

1. 専用のサービスユーザーとしてTealiumにログインします。
1. [APIキー](https://docs.tealium.com/api-keys/)を生成します。
1. 次のcURLコマンドを使用して長期間有効なベアラートークンを生成するための長期間有効なトークンエンドポイントを呼び出します。プレースホルダーをアカウント名、プロファイル名、専用ユーザー名、APIキーに置き換えてください：

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
  "expires_in":35999,
  "refresh_expires_in":0,
  "token_type":"Bearer",
  "not-before-policy":0,
  "scope":"profile email"
}
```

トークンは90日後に期限切れになります。必要に応じてトークンを再生成してください。

トークンの生成や権限に関する質問がある場合は、Tealiumサポートに連絡してください。

## エンドポイントと権限

TealiumのSCIM実装は、次のHTTPメソッドをサポートしています：

| メソッド | 説明                          | Tealium権限 |
| ------ | ------------------------------------ | --------------------------- |
| `POST`   | ユーザーまたはグループを作成します。              | ユーザー管理者またはアカウント管理者 |
| `GET`    | ユーザーの詳細、グループの詳細、またはユーザーまたはグループのリストを取得します。 | すべてのアカウントユーザー |
| `PUT`    | ユーザーまたはグループを置き換えます。                      | ユーザー管理者またはアカウント管理者 |
| `DELETE` | ユーザーまたはグループを削除します。                       | ユーザー管理者またはアカウント管理者 |
| `PATCH`  | ユーザーまたはグループを部分的に更新します。             | ユーザー管理者またはアカウント管理者 |

## 組み込みグループ

SCIM APIは、[Tealiumシステム管理ロール](https://docs.tealium.com/admin-roles/)に沿った組み込みグループを公開します。

次の組み込みグループがSCIM `/Groups`エンドポイントで利用可能です：

| グループ名 | 説明 |
| --- | --- |
| Account Admins | 全アカウント管理権限 |
| User Admins | ユーザー管理権限 |
| Privacy Admins | プライバシーおよび同意管理権限 |
| Technical Admins | 技術および統合権限 |
| Profile Admins | プロファイルレベルの管理権限 |
| Standard User | 基本的な読み取り専用アクセス（Account Viewersの別名） |


<blockquote>
`Standard User`グループは内部の`Account Viewers`グループの別名です。両グループは同じUUIDを共有しています。`displayName eq "Standard User"`でフィルタリングするとこのグループに一致しますが、`Account Viewers`でフィルタリングすると結果は0になります。
</blockquote>


### 継承グループ

特定の管理グループにユーザーを追加すると、継承グループのメンバーシップが自動的に付与されます：

| グループに追加 | 自動的に追加される |
| --- | --- |
| Account Admins | User Admins, Privacy Admins, Technical Admins, Profile Admins + PIIアクセス |
| User Admins | Technical Admins + PIIアクセス |
| Privacy Admins | User Admins, Technical Admins + PIIアクセス |
| Technical Admins | (なし) |
| Profile Admins | (なし) |
| Standard User | (なし) |


<blockquote>
Account Admins、User Admins、またはPrivacy Adminsのメンバーシップは、内部のPIIグループ（PII Admins/PII Viewers）のメンバーシップを自動的に付与します。セキュリティ上の理由から、これらの内部グループはSCIM APIでは表示されません。
</blockquote>


### グループ削除の挙動

管理グループからユーザーを削除すると、継承グループからも自動的に削除されます：

* **Account Admins**：User Admins, Privacy Admins, Technical Admins, Profile Adminsから削除し、PIIアクセスを取り消します
* **User Admins**：Technical Adminsから削除し、PIIアクセスを取り消します
* **Privacy Admins**：User Admins, Technical Adminsから削除し、PIIアクセスを取り消します
* **Technical Admins**：自動削除なし
* **Profile Admins**：自動削除なし

### 組み込みグループの保護

組み込みグループには次の制限があります：

* SCIM PATCH操作で名前を変更することはできません。
* SCIM DELETE操作で削除することはできません。


<blockquote>
組み込みグループと一致する`displayName`を持つカスタムグループを作成または更新すると、HTTP 400エラーが返されます。
</blockquote>

