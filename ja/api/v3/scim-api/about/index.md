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

APIキーとベアラートークンは、それを生成したユーザーにリンクされています。必要なTealium権限を持つ専用のサービスユーザーを使用してください。サービスユーザーは、人物にリンクされていないリソースを管理するために使用されるユーザーアカウントです。このアプローチは、通常のユーザーアカウントが利用できなくなった場合のアクセス問題を防ぎます。

ベアラートークンを生成するには：

1. 専用のサービスユーザーとしてTealiumにログインします。
1. [APIキー]()を生成します。
1. 次のcURLコマンドを使用して長期間有効なベアラートークンを生成するための長期間有効なトークンエンドポイントを呼び出します。プレースホルダーをアカウント名、プロファイル名、専用ユーザー名、APIキーに置き換えてください：

```bash
curl --location &#39;https://developer.tealiumapis.com/v1/auth-long-lived/token&#39; \
--header &#39;Content-Type: application/x-www-form-urlencoded&#39; \
--data-urlencode &#39;account={ACCOUNT}&#39; \
--data-urlencode &#39;profile=main&#39; \
--data-urlencode &#39;username={USERNAME@EXAMPLE.COM}&#39; \
--data-urlencode &#39;key={API_KEY}&#39;
```

トークンは次の例のようになります：

```json
{
  &#34;access_token&#34;:&#34;eyJhbG...53UHg&#34;,
  &#34;expires_in&#34;:35999,
  &#34;refresh_expires_in&#34;:0,
  &#34;token_type&#34;:&#34;Bearer&#34;,
  &#34;not-before-policy&#34;:0,
  &#34;scope&#34;:&#34;profile email&#34;
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

SCIM APIは、[Tealiumシステム管理ロール]()に沿った組み込みグループを公開します。

次の組み込みグループがSCIM `/Groups`エンドポイントで利用可能です：

| グループ名 | 説明 |
| --- | --- |
| Account Admins | 全アカウント管理権限 |
| User Admins | ユーザー管理権限 |
| Privacy Admins | プライバシーおよび同意管理権限 |
| Technical Admins | 技術および統合権限 |
| Profile Admins | プロファイルレベルの管理権限 |
| Standard User | 基本的な読み取り専用アクセス（Account Viewersの別名） |

`Standard User`グループは内部の`Account Viewers`グループの別名です。両グループは同じUUIDを共有しています。`displayName eq &#34;Standard User&#34;`でフィルタリングするとこのグループに一致しますが、`Account Viewers`でフィルタリングすると結果は0になります。

### 継承グループ

特定の管理グループにユーザーを追加すると、継承グループのメンバーシップが自動的に付与されます：

| グループに追加 | 自動的に追加される |
| --- | --- |
| Account Admins | User Admins, Privacy Admins, Technical Admins, Profile Admins &#43; PIIアクセス |
| User Admins | Technical Admins &#43; PIIアクセス |
| Privacy Admins | User Admins, Technical Admins &#43; PIIアクセス |
| Technical Admins | (なし) |
| Profile Admins | (なし) |
| Standard User | (なし) |

Account Admins、User Admins、またはPrivacy Adminsのメンバーシップは、内部のPIIグループ（PII Admins/PII Viewers）のメンバーシップを自動的に付与します。セキュリティ上の理由から、これらの内部グループはSCIM APIでは表示されません。

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

組み込みグループと一致する`displayName`を持つカスタムグループを作成または更新すると、HTTP 400エラーが返されます。
