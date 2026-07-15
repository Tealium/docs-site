---
title: SCIMとIDプロバイダーの構成
description: SCIMをサポートするIDプロバイダーとの構成方法を学びます。
url: https://docs.tealium.com/ja/api/v3/scim-api/example/
---
SCIM APIを使用して自動的に以下の操作を行います：

* ユーザーのプロビジョニングとデプロビジョニング
    * ユーザーの表示、作成、削除
    * ユーザーの削除（SCIM IDの非アクティブ化）
    * ユーザーの再追加（SCIM IDの再アクティブ化）
* ユーザーとグループの更新
    * ユーザーの更新
    * グループの表示、作成、更新、削除

TealiumでSCIMが有効になると、TealiumとIDプロバイダー間でユーザーメンバーシップが同期されます。

## 前提条件

* [アカウント管理者またはユーザー管理者]()の権限。
* 長期間有効なベアラートークン。ベアラートークンの生成方法については、[認証]()を参照してください。

## IDプロバイダーの構成

以下のIDプロバイダーを構成できます：

* Microsoft Entra ID（旧Azure Active Directory）
* Okta

これらのプロバイダーは完全に互換性があります。ただし、他のIdPでは追加の構成や調整が必要になる場合があります。詳細なガイダンスについては、IDプロバイダーおよびTealiumサポートに連絡して互換性を確認してください。

## Microsoft Entra IDの構成

SSO構成中に[Azure Active Directory](https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/view-applications-portal)用に作成されたSAMLアプリケーションは、SCIM用に構成する必要があります。

SCIMプロビジョニングは、以下の指示に従って正確に構成する必要があります。構成が誤っていると、ユーザープロビジョニングやサインインに問題が発生します。手順に関して問題や質問がある場合は、Tealiumサポートに連絡してください。

Microsoft Entra IDでSCIMを構成するには：

### TealiumをMicrosoft Entra IDに追加

1. [Azure Portal](https://portal.azure.com/)にアクセスします。
1. **Microsoft Entra ID &gt; Enterprise applications**に移動します。
1. **&#43; New application**をクリックし、**Create your own application**をクリックします。
1. **Name**（例：Tealium）を入力し、**Integrate any other application you don’t find in the gallery**を選択します。
1. **Create**をクリックします。

### SCIMプロビジョニングの構成

1. アプリで**Provisioning**タブをクリックし、**Connect your application**をクリックします。
1. **Admin Credentials**の下で、次の値を入力します：
   * **Tenant URL**フィールドに、TealiumからのSCIM APIエンドポイントURLを入力します：`https://developer.tealiumapis.com/scim/v2?aadOptscim062020`。`aadOptscim062020`フラグは、Microsoft Entra IDのグループ管理を特に有効にします。
   * **Secret Token**フィールドに、TealiumからのSCIMベアラートークンを入力します。
1. **Test Connection**をクリックします。成功メッセージが表示されます。
1. **Create**をクリックします。
1. **Get Started**をクリックし、その後**Start provisioning**をクリックします。

### ユーザー割り当ての構成

SCIMグループプロビジョニングは現在Early Accessではサポートされていません。

1. **Provisioning**をクリックします。
1. **Provisioning Status**を`ON`に構成します。
1. **Mappings**セクションを展開します。
1. 各マッピングをクリックし、すべての**Target Object Actions**が有効になっていることを確認します。
1. **Attribute mapping**をクリックし、Microsoft Entra IDとTealium間の属性マッピングを構成します。詳細については、[Microsoft: Customize user provisioning attribute-mappings for SaaS applications in Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity/app-provisioning/customize-application-attributes)を参照してください。

次の表は、TealiumがMicrosoft Entra IDを介してSCIMで認証するために構成する必要がある属性マッピングをリストしています。他のすべてのマッピングを削除し、次のマッピングのみが残るようにします：

| Microsoft Entra IDソース属性 | `customappsso`ターゲット属性 | マッチング優先度 |
|-------------------------------------------------------------------|-------------------|-----|
| `userPrincipalName`                                               | `userName`        |  1  | 
| `Switch([IsSoftDeleted], , &#34;False&#34;, &#34;True&#34;, &#34;True&#34;, &#34;False&#34;)` \*  | `active`          |     |
| `displayName`                                                     | `displayName`     |     |
| `givenName`                                                       | `name.GivenName`  |     |
| `surname`                                                         | `name.familyName` |     |
| `mailNickname`                                                    | `externalId`      |     |

\* これは直接のマッピングではなく、式タイプです。**Mapping type**リストから**Expression**を選択します。

MicrosoftがAzure Active DirectoryからEntra IDの命名スキームに移行する間、ユーザーインターフェースに不整合が見られるかもしれません。問題がある場合は、Tealiumサポートに連絡してください。

各属性マッピングには次のものが含まれます：

* `customappsso`属性はターゲット属性に対応します。
* Microsoft Entra ID属性はソース属性に対応します。

各属性について、次の手順を使用します：

1. 既存の属性を編集するか、新しい属性を追加します。
1. リストから必要なソースとターゲットの属性マッピングを選択します。
1. **Ok**をクリックします。
1. **Save**をクリックします。

推奨されるSAML構成と異なるSAML構成を使用している場合は、マッピング属性を選択してそれに応じて変更します。`externalId`ターゲット属性にマッピングするソース属性は、SAMLの`mailNickname`で使用される属性と一致する必要があります。

表にリストされていないマッピングを使用する場合は、Microsoft Entra IDのデフォルトを使用します。必要な属性のリストについては、[Microsoft: Develop and plan provisioning for a SCIM endpoint in Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity/app-provisioning/use-scim-to-provision-users-and-groups)を参照してください。

### グループの割り当て

1. **Provision Microsoft Entra ID Groups**を選択します。
1. **Attribute Mapping**ページで、**Provisioning Status**トグルを`ON`に構成します。
1. **Save**をクリックします。

### ユーザーの割り当て

1. **Users and groups**に移動します。
1. **&#43; Add user/group**をクリックします。
1. 同期したいユーザーまたはグループを選択します。
1. **Assign**をクリックします。

### 最終構成の構成とプロビジョニングの開始

次の構成を構成します：

1. （オプション）**Send an email notification when a failure occurs**チェックボックスを選択します。
1. （オプション）**Prevent accidental deletion**チェックボックスを選択します。
1. 変更がすべて保存されていることを確認するために**Save**をクリックします。
1. **Provisioning**に移動し、**Start provisioning**をクリックします。

プロビジョニングは通常数分以内に開始されますが、最初の同期には最大40分かかる場合があります。

## Oktaの構成

OktaでSCIMを構成するには：

1. Oktaにログインします。
1. **Applications &gt; Applications**に移動します。
1. **Browse App Catalog**をクリックします。
1. **SCIM 2.0 Test App (OAuth Bearer Token)**を選択し、**Add Integration**をクリックします。
1. **Next**および**Done**をクリックして、**General Settings**および**Sign-On Options**ページをスキップします。

### Tealium SCIM APIに接続

1. **SCIM Application**画面で、**Provisioning**タブをクリックします。
1. **Configure API integration**をクリックします。
1. **Enable API integration**チェックボックスを有効にします。
1. 次の情報を入力します：
    * **Base URL**の下に、Tealium SCIM構成ページの**SCIM API endpoint URL**からコピーしたURLを貼り付けます：`https://developer.tealiumapis.com/scim/v2/`
    * **OAuth Bearer Token**の下に、Tealium SCIM構成ページの**Your SCIM token**からコピーしたSCIMベアラートークンを貼り付けます。
    * 構成を確認するために、**Test API Credentials**をクリックします。
1. **Save**をクリックします。

### プロビジョニング構成の構成

1. **Provisioning**タブの下で、**Settings**までスクロールダウンし、**To App**をクリックします。
1. **Provisioning to App**セクションで、**Edit**をクリックします。
1. **Create Users**、**Update User Attributes**、**Deactivate Users**のための**Enable**チェックボックスを有効にします。
1. **Save**をクリックします。
## ユーザーアクセス

同期プロセス中、すべての新規ユーザーはTealiumアカウントを受け取り、招待メールでアイデンティティプロバイダーグループへの歓迎を受けます。確認済みドメインを使用することで、メール確認をスキップすることができます。

プロビジョニング中には、主要なメールと副次的なメールの両方がTealiumユーザーアカウントの存在を確認する際に考慮されます。重複するユーザー名は、ユーザーを作成する際に接尾辞`1`を追加することで処理されます。例えば、`test_user`が既に存在する場合、`test_user1`が使用されます。`test_user1`が既に存在する場合、Tealiumは未使用のユーザー名を見つけるために接尾辞を増やします。4回試しても未使用のユーザー名が見つからない場合は、ランダムな文字列がユーザー名に添付されます。

次回以降の訪問時には、新規および既存のユーザーは、アイデンティティプロバイダーのダッシュボードを通じて、または直接リンクを訪れることでアイデンティティプロバイダーグループにアクセスできます。

## アクセスの削除

アイデンティティプロバイダーでユーザーを削除または非アクティブ化して、そのアクセスを削除します。

アイデンティティプロバイダーが構成されたスケジュールに基づいて同期を実行した後、アイデンティティプロバイダーはユーザーのメンバーシップを取り消し、彼らはアクセスを失います。

アイデンティティプロバイダーでユーザーを削除または非アクティブ化しても、Tealiumユーザーアカウントは削除されません。Tealiumユーザーアカウントは非アクティブ化され、アイデンティティプロバイダーにユーザーを再追加することで再アクティブ化できます。

## アクセスの再アクティブ化

SCIMを通じてユーザーが削除または非アクティブ化された後、そのユーザーをSCIMアイデンティティプロバイダーに追加することで再アクティブ化します。

アイデンティティプロバイダーが構成されたスケジュールに基づいて同期を実行した後、アイデンティティプロバイダーはユーザーのSCIMアイデンティティを再アクティブ化し、彼らのグループメンバーシップを復元します。