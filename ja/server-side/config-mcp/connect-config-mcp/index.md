---
title: Tealium Configuration MCP への接続
description: 組織向けに Tealium Configuration MCP を構成し、AI クライアントをサーバーサイドプロファイルに接続します。
url: https://docs.tealium.com/ja/server-side/config-mcp/connect-config-mcp/
---

<blockquote>
Tealium Configuration MCP は、一部のお客様のみご利用いただけます。この機能の利用を希望する場合は、[サポートにお問い合わせください](https://docs.tealium.com/support/)。
</blockquote>


Tealium Configuration MCP のセットアップには、管理者とエンドユーザーの両方による手順が必要です。ステップ 4 で AI クライアントを構成する前に、Tealium UI でステップ 1～3 を完了してください。これらの手順を省略すると、認証エラーが発生します。

## ステップ 1：Tealium AI Settings で Tealium Configuration MCP を有効にする（管理者）

Tealium UI で、アカウントレベルとプロファイルレベルの両方について Tealium Configuration MCP を有効にします。

1. Tealium で、右上隅にある自分のイニシャルをクリックし、**AI Settings** をクリックします。
1. アカウントの **MCP Server** トグルを **On** に構成します。
1. Tealium Configuration MCP を有効にする各プロファイルに切り替え、同じ操作を繰り返します。プロファイルレベルの **MCP Server** トグルを **On** に構成してください。

特定のプロファイルについて Tealium Configuration MCP を無効にするには、いつでも AI Settings に戻り、トグルを **Off** に構成します。

![](https://docs.tealium.com/images/server-side/config-mcp-setup-ai-settings-toggle.png)

## ステップ 2：Tealium Configuration MCP のアクセス委任を有効にする（管理者）

Tealium Configuration MCP を通じて Tealium プロファイルに接続する権限をユーザーに付与します。手順は、アカウントで従来の権限とプラットフォーム権限のどちらを使用しているかによって異なります。

### アカウントで従来の権限を使用している場合

Tealium Configuration MCP へのアクセスが必要な各ユーザーに、必要なプロファイルレベルの権限を構成します。

1. Tealium で、**Manage Users** に移動します。
1. ユーザーを選択して **Edit Users** 画面を開きます。
1. **Next** をクリックして **Profile Permissions** 画面に移動します。
1. **Profile Permissions** で、Tealium Configuration MCP へのアクセス権を付与する各プロファイルを見つけ、次のいずれかのアクセスレベルを構成します。
   * **Reader：** 読み取り専用。Tealium Configuration MCP はプロファイルを調査して説明できますが、エンティティの作成、変更、削除はできません。
   * **Editor** または **Publisher：** 読み取りと書き込み。Tealium Configuration MCP は、サポート対象のエンティティを調査、作成、変更、削除できます。
1. **Save** をクリックします。

Tealium Configuration MCP へのアクセスが必要なユーザーごとに、この手順を繰り返します。

### アカウントでプラットフォーム権限を使用している場合

適切なアクセスレベルを持つユーザーグループを作成し、Tealium Configuration MCP を通じて Tealium プロファイルに接続する権限をユーザーに付与します。

1. Tealium で、**Manage Permissions** に移動します。
1. **+New Group** をクリックします。
1. グループの名前を入力し、**Next** をクリックします。
1. **AI Access** で **MCP Server** を見つけ、次のいずれかのアクセスレベルを選択します。完了したら **Next** をクリックします。
    * **Viewer：** 読み取り専用。Tealium Configuration MCP はプロファイルを調査して説明できますが、エンティティの作成、変更、削除はできません。
    * **Editor：** 読み取りと書き込み。Tealium Configuration MCP は、サポート対象のエンティティを調査、作成、変更、削除できます。
     ![](https://docs.tealium.com/images/server-side/config-mcp-setup-user-group-access.png)
1. Tealium Configuration MCP に追加の機能権限はありません。**Next** をクリックして、この手順をスキップします。
1. Tealium Configuration MCP へのアクセスが必要なプロファイルをグループに追加し、**Next** をクリックします。
1. Tealium Configuration MCP へのアクセスが必要なユーザーをグループに追加し、**Save** をクリックします。

ニーズが異なるユーザーに対応するため、表示アクセス用と編集アクセス用に別々のグループを作成できます。


<blockquote>
Tealium は、Tealium Configuration MCP へのアクセスに最低限必要な権限に合わせて、個々の製品コンポーネントの権限を調整する場合があります。
</blockquote>


## ステップ 3：ユーザー構成でプロファイルを選択する（ユーザー）

各ユーザーは、Tealium Configuration MCP で使用するデフォルトの Tealium プロファイルを選択します。

1. サーバーサイドの Tealium UI で、右上隅にある自分のイニシャルをクリックし、**Edit/View User Settings** を選択します。
1. **Tealium Configuration MCP** で、デフォルトとして使用する **Account** と **Profile** を選択します。
1. **Apply Configuration** をクリックします。

別のプロファイルを使用するには、この画面に戻ってプロファイルを選択し、**Apply Configuration** をクリックします。


<blockquote>
プロファイルを変更した後は、AI クライアントで Tealium Configuration MCP を切断して再接続し、新しいチャットを開始してください。以前のセッションは無効になります。
</blockquote>


## ステップ 4：AI クライアントを接続する（管理者およびユーザー）

AI クライアントを Tealium Configuration MCP に接続します。お使いのクライアント向けの手順に従ってください。

### Claude Desktop を接続する

**開始する前に**

開始前に、次の項目を確認してください。

* Claude Pro、Max、Team、または Enterprise プランを契約していること。無料プランではカスタムコネクターを追加できません。
* Claude Desktop がインストールされているか、[claude.ai](https://claude.ai) にアクセスできること。
* アカウントで Tealium Configuration MCP が有効になっていること。アクセスをリクエストするには、[サポートにお問い合わせください](https://docs.tealium.com/support/)。

**コネクターを追加する**

1. 管理者として [claude.ai](https://claude.ai) にサインインします。
1. プロファイルアイコンをクリックし、**Settings** を選択します。
1. **Connectors** を選択します。
1. ページの下部までスクロールし、**Add custom connector** をクリックします。
1. 信頼できるサービスへの接続に関する警告が表示された場合は、その内容を確認し、続行を承認します。
1. 次のコネクター情報を入力します。

   * **Name:** `Tealium Configuration MCP`
   * **Remote MCP server URL:** `https://us-west-1.prod.developer.tealiumapis.com/2026-09/mcp/dcp`

1. **Advanced settings** は空欄のままにします。
1. **Add** をクリックします。コネクターが Connectors リストに表示されます。

![](https://docs.tealium.com/images/server-side/config-mcp-setup-add-connector.png)

**認証して接続する**

1. Claude で、**Settings > Connectors** に移動します。
1. **Tealium Configuration MCP** の横にある **Connect** をクリックします。
1. [ステップ 5：認証する](#step-5-authenticate-user)に記載されている Tealium のサインイン手順を完了します。
1. 認証が完了すると、コネクターのステータスが接続済みと表示されます。

   ![](https://docs.tealium.com/images/server-side/config-mcp-setup-connected.png)

コネクターを切断するには、Claude で **Settings > Connectors** に移動し、**Tealium Configuration MCP** を見つけて **Disconnect** を選択します。

**チャットでコネクターを有効にする**

1. Claude で新しいチャットを開きます。
1. メッセージ作成欄の **+** アイコンをクリックします。
1. **Tealium Configuration MCP** をオンに切り替えます。

![](https://docs.tealium.com/images/server-side/config-mcp-setup-enable-in-chat.png)
### Claude Code CLI に接続する

**開始する前に**

開始前に、以下を確認してください。

* Claude Code がインストールされ、認証済みであること。
* 任意のプロジェクトディレクトリでターミナルが開いていること。空のディレクトリを含め、どのディレクトリでも使用できます。

**Tealium Configuration MCP を登録する**

Claude セッションを開始する前に、ターミナルで次のコマンドを実行します。

```bash
claude mcp add --transport http \
  --client-id tealium-mcp-for-web-platforms \
  tealium-configuration-mcp \
  https://us-west-1.prod.developer.tealiumapis.com/2026-09/mcp/dcp
```

サーバーが追加されたことを確認します。

```bash
claude mcp list
```

**認証して接続する**

1. `claude` を実行して Claude セッションを開始します。
1. `/mcp` を実行して、構成済みの MCP サーバーを一覧表示します。
1. `tealium-configuration-mcp` を見つけます。ステータスは **認証が必要** と表示されます。
1. **認証**アクションを選択します。Claude Code により、デフォルトのブラウザーで Tealium のログイン画面が開きます。
1. [ステップ5：認証](#step-5-authenticate-user)の手順に従って、Tealium へのサインインを完了します。
1. 認証が完了すると、サーバーのステータスが接続済みに更新されます。

切断するには、Claude セッション内で `/mcp` に移動し、`tealium-configuration-mcp` を見つけて **無効化**を選択します。

## ステップ5：認証（ユーザー）

Tealium Configuration MCP への接続を有効にするため、Tealium のサインインチャレンジを完了します。以下の手順は、Claude Desktop と Claude Code CLI の両方に適用されます。

1. Tealium のサインインウィンドウが開きます。アカウント名を入力し、**サインイン**をクリックします。組織で SSO を使用している場合は、SSO アカウント名を入力します。アカウント名がわからない場合は、アカウント管理者にお問い合わせください。

   ![](https://docs.tealium.com/images/server-side/config-mcp-setup-signin-account.png)

1. Tealium の認証情報を使用してサインインします。
   * **SSO を使用しない場合：** ユーザー名またはメールアドレスとパスワードを入力し、**サインイン**をクリックします。

     ![](https://docs.tealium.com/images/server-side/config-mcp-setup-signin-credentials.png)

   * **SSO を使用する場合：** ID プロバイダーによってサインイン画面にリダイレクトされます。SSO の認証情報を入力します。

1. プロンプトが表示されたら、**はい**を選択して、AI クライアントに Tealium プロファイルへのアクセスを許可します。

   ![](https://docs.tealium.com/images/server-side/config-mcp-setup-grant-access.png)

1. ウィンドウが閉じたら、AI クライアントに戻ります。コネクターのステータスが接続済みと表示されます。

「アカウントは認証されましたが、Tealium MCP Early Access への接続時にエラーが返されました」などのエラーが表示された場合は、サポートに問い合わせる前に、Tealium UI で以下を確認してください。

* AI Settings で、アカウントとプロファイルの両方について **MCP Server** トグルが **オン**に構成されていること。
* Tealium Configuration MCP へのアクセスに必要なユーザー権限が正しく構成されていること（[ステップ2](#step-2-enable-tealium-configuration-mcp-access-delegation-admin)を参照）。
* **Edit/View User Settings** でデフォルトのアカウントとプロファイルが選択されていること（[ステップ3](#step-3-select-a-profile-in-user-preferences-user)を参照）。

これでコネクターが有効になりました。セッションの実行方法について詳しくは、[Tealium Configuration MCP を管理する](https://docs.tealium.com/manage-config-mcp/)を参照してください。