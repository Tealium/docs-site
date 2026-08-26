---
title: Tealium Configuration MCPへの接続
description: お客様の組織のためにTealium Configuration MCPを構成し、AIクライアントをサーバーサイドプロファイルに接続します。
url: https://docs.tealium.com/ja/server-side/config-mcp/connect-config-mcp/
---

<blockquote>
Tealium Configuration MCPは選ばれた顧客のみが利用可能です。この機能を試してみたい場合は、[サポートに連絡してください](https://docs.tealium.com/support/)。
</blockquote>


Tealium Configuration MCPの構成には、管理者とエンドユーザーの両方のステップが含まれます。順番にステップを完了してください。

## 始める前に

構成を開始する前に以下の点を確認してください：

* あなたのアカウントはTealium Platform Permissionsを使用しています。レガシー権限はサポートされていません。
* Claude Pro、Max、Team、またはEnterpriseプランを持っています。無料プランではカスタムコネクタを追加できません。
* エンドユーザーはClaude Desktopをインストールしているか、[claude.ai](https://claude.ai)へのアクセスがあります。
* Tealium Configuration MCPがあなたのアカウントで有効になっています。アクセスをリクエストするには、[サポートに連絡してください](https://docs.tealium.com/support/)。

## ステップ1: ClaudeでTealiumコネクタを追加する（管理者）

Claudeの組織にTealium Configuration MCPカスタムコネクタを追加して、ユーザーがTealiumプロファイルに接続できるようにします。

1. [claude.ai](https://claude.ai) に管理者としてログインします。
1. プロファイルアイコンをクリックし、**構成**を選択します。
1. **コネクタ**を選択します。
1. ページの下部までスクロールし、**カスタムコネクタを追加**をクリックします。
1. 信頼できるサービスへの接続に関する警告が表示された場合は、確認して続行します。
1. 次のコネクタの詳細を入力します：

   * **名前：** `Tealium Configuration MCP`
   * **リモートMCPサーバーURL：** `https://us-west-1.prod.developer.tealiumapis.com/2026-09/mcp/dcp`

1. **詳細構成**を展開し、次の情報を入力します：

   * **OAuthクライアントID：** `tealium-mcp-for-web-platforms`

1. **OAuthクライアントシークレット**フィールドは空白のままにします。
1. **追加**をクリックします。コネクタはコネクタリストに表示されます。

![](https://docs.tealium.com/images/server-side/config-mcp-setup-add-connector.png)


## ステップ2: Tealium AI構成でMCPを有効にする（管理者）

Tealium UIのアカウントレベルとプロファイルレベルでTealium Configuration MCPを有効にします。

1. Tealiumで、右上隅にあるイニシャルをクリックし、**AI構成**をクリックします。
1. アカウントの**MCPサーバー**トグルを**オン**に構成します。
1. MCPを有効にしたい各プロファイルに切り替え、プロファイルレベルで**MCPサーバー**トグルを**オン**に構成します。

特定のプロファイルでMCPを無効にするには、いつでもAI構成に戻り、トグルを**オフ**に構成します。

![](https://docs.tealium.com/images/server-side/config-mcp-setup-ai-settings-toggle.png)

## ステップ3: MCPアクセス権を持つユーザーグループを作成する（管理者）

MCPを通じてTealiumプロファイルに接続するための権限をユーザーに付与するために、適切なアクセスレベルを持つユーザーグループを作成します。

1. Tealiumで、**権限管理**に移動します。
1. **+新しいグループ**をクリックします。
1. グループ名を入力し、**次へ**をクリックします。
1. **AIアクセス**の下で、**MCPサーバー**を見つけ、次のいずれかのアクセスレベルを選択します。完了したら、**次へ**をクリックします。
    * **閲覧者ー：** 読み取り専用。MCPサーバーはプロファイルを探索し説明することができますが、エンティティの作成、変更、または削除はできません。
    * **エディター：** 読み書き可能。MCPサーバーは、サポートされているエンティティの探索、作成、変更、削除ができます。
     ![](https://docs.tealium.com/images/server-side/config-mcp-setup-user-group-access.png)
1. MCPサーバーの追加機能権限はありません。このステップをスキップするには、**次へ**をクリックします。
1. MCPアクセスが必要なプロファイルをグループに追加し、**次へ**をクリックします。
1. MCPアクセスが必要なユーザーをグループに追加し、**保存**をクリックします。

異なるニーズを持つユーザーに対応するために、閲覧と編集アクセスのための別々のグループを作成することができます。


<blockquote>
個々の製品コンポーネントの権限は、MCPアクセスに必要な最小限の権限に合わせて調整される場合があります。
</blockquote>


## ステップ4: ユーザー構成でプロファイルを選択する（ユーザー）

各ユーザーはMCPが使用するデフォルトのTealiumプロファイルを選択します。

1. Tealium UIで、右上隅にあるイニシャルをクリックし、**ユーザー構成の編集/表示**を選択します。
1. **Tealium Configuration MCP**の下で、デフォルトとして使用する**アカウント**と**プロファイル**を選択します。
1. **構成を適用**をクリックします。

後で別のプロファイルに接続する場合は、この画面に戻り、新しいプロファイルを選択して**構成を適用**をクリックします。プロファイルを変更すると、現在のMCPセッションが無効になります。プロファイルを切り替えた後は、Tealium Configuration MCPコネクタを再接続し、新しいチャットを開始してください。

## ステップ5: ClaudeをTealiumに接続する（ユーザー）

ClaudeでTealiumコネクタを認証し、チャットで有効にします。

**コネクタを接続する**

1. Claudeで、**構成 > コネクタ**に移動します。
1. **Tealium Configuration MCP**の隣の**接続**をクリックします。
1. Tealiumのサインインウィンドウが開きます。アカウント名を入力して**サインイン**をクリックします。

   ![](https://docs.tealium.com/images/server-side/config-mcp-setup-signin-account.png)

1. Tealiumの資格情報でサインインします：
   * **SSOなし：** ユーザー名またはメールとパスワードを入力し、**サインイン**をクリックします。

     ![](https://docs.tealium.com/images/server-side/config-mcp-setup-signin-credentials.png)

   * **SSOあり：** 身元確認プロバイダーがサインインするためにリダイレクトします。SSO資格情報を入力します。

1. プロンプトが表示されたら、AIクライアントがTealiumプロファイルにアクセスすることを許可するために**はい**を選択します。

   ![](https://docs.tealium.com/images/server-side/config-mcp-setup-grant-access.png)

1. ウィンドウが閉じた後、コネクタの状態は接続済みと表示されます。

   ![](https://docs.tealium.com/images/server-side/config-mcp-setup-connected.png)

いつでもコネクタを切断するには、Claudeで**構成 > コネクタ**に移動し、**Tealium Configuration MCP**を見つけて**切断**を選択します。

**チャットでコネクタを有効にする**

1. Claudeで新しいチャットを開きます。
1. メッセージコンポーザーで**+**アイコンをクリックします。
1. **Tealium Configuration MCP**をオンに切り替えます。

![](https://docs.tealium.com/images/server-side/config-mcp-setup-enable-in-chat.png)

コネクタは会話でアクティブになります。セッションの実行に関する詳細は、[Tealium Configuration MCPの管理](https://docs.tealium.com/manage-config-mcp/)を参照してください。