---
title: Tealium Configuration MCPへの接続
description: お客様の組織のためにTealium Configuration MCPを構成し、AIクライアントをサーバーサイドプロファイルに接続します。
url: https://docs.tealium.com/ja/server-side/config-mcp/connect-config-mcp/
---

<blockquote>
Tealium Configuration MCPは選ばれた顧客のみが利用可能です。この機能を試してみたい場合は、[サポートに連絡してください](https://docs.tealium.com/support/)。
</blockquote>


Tealium Configuration MCPの構成には、管理者とエンドユーザーの両方のステップが含まれます。AIクライアントを構成する前に、Tealium UIでステップ1から3を完了してください。これらのステップをスキップすると認証エラーが発生します。

## ステップ1: Tealium AI構成でTealium Configuration MCPを有効にする（管理者）

Tealium UIでアカウントレベルとプロファイルレベルの両方でTealium Configuration MCPを有効にします。

1. Tealiumで右上隅にあるイニシャルをクリックし、**AI構成**をクリックします。
1. アカウントの**MCPサーバー**トグルを**オン**に構成します。
1. Tealium Configuration MCPを有効にしたい各プロファイルに切り替え、プロファイルレベルで**MCPサーバー**トグルを**オン**に構成します。

特定のプロファイルでTealium Configuration MCPを無効にするには、いつでもAI構成に戻り、トグルを**オフ**に構成します。

![](https://docs.tealium.com/images/server-side/config-mcp-setup-ai-settings-toggle.png)

## ステップ2: Tealium Configuration MCPアクセス委任を有効にする（管理者）

ユーザーがTealiumプロファイルにTealium Configuration MCPを介して接続できるように許可します。ステップは、アカウントがレガシー権限を使用しているかプラットフォーム権限を使用しているかによって異なります。

### アカウントがレガシー権限を使用している場合

Tealium Configuration MCPアクセスが必要な各ユーザーに必要なプロファイルレベルの権限を構成します。

1. Tealiumで**ユーザー管理**に移動します。
1. ユーザーを選択して**ユーザー編集**画面を開きます。
1. **次へ**をクリックして**プロファイル権限**画面に進みます。
1. **プロファイル権限**の下で、Tealium Configuration MCPアクセスを許可したい各プロファイルを見つけ、次のいずれかのアクセスレベルを構成します：
   * **リーダー：** 読み取り専用。Tealium Configuration MCPはプロファイルを探索し説明することができますが、エンティティの作成、変更、または削除はできません。
   * **エディター**または**パブリッシャー：** 読み書き可能。Tealium Configuration MCPは、サポートされているエンティティを探索、作成、変更、削除することができます。
1. **保存**をクリックします。

Tealium Configuration MCPアクセスが必要な各ユーザーに対して繰り返します。

### アカウントがプラットフォーム権限を使用している場合

適切なアクセスレベルを持つユーザーグループを作成することにより、ユーザーがTealiumプロファイルにTealium Configuration MCPを介して接続できるように許可します。

1. Tealiumで**権限管理**に移動します。
1. **+新規グループ**をクリックします。
1. グループ名を入力し、**次へ**をクリックします。
1. **AIアクセス**の下で**MCPサーバー**を見つけ、次のいずれかのアクセスレベルを選択します。完了したら**次へ**をクリックします。
    * **閲覧者ー：** 読み取り専用。Tealium Configuration MCPはプロファイルを探索し説明することができますが、エンティティの作成、変更、または削除はできません。
    * **エディター：** 読み書き可能。Tealium Configuration MCPは、サポートされているエンティティを探索、作成、変更、削除することができます。
     ![](https://docs.tealium.com/images/server-side/config-mcp-setup-user-group-access.png)
1. Tealium Configuration MCPの追加機能権限はありません。このステップをスキップするには**次へ**をクリックします。
1. Tealium Configuration MCPアクセスが必要なプロファイルをグループに追加し、**次へ**をクリックします。
1. Tealium Configuration MCPアクセスが必要なユーザーをグループに追加し、**保存**をクリックします。

異なるニーズを持つユーザーに対応するために、閲覧と編集アクセスのための別々のグループを作成することができます。


<blockquote>
Tealiumは、Tealium Configuration MCPアクセスに必要な最小限の権限に合わせて個々の製品コンポーネントの権限を調整する場合があります。
</blockquote>


## ステップ3: ユーザー構成でプロファイルを選択する（ユーザー）

各ユーザーは、Tealium Configuration MCPが使用するデフォルトのTealiumプロファイルを選択します。

1. サーバーサイドのTealium UIで、右上隅にあるイニシャルをクリックし、**ユーザー構成の編集/表示**を選択します。
1. **Tealium Configuration MCP**の下で、デフォルトとして使用する**アカウント**と**プロファイル**を選択します。
1. **構成を適用**をクリックします。

別のプロファイルを使用する場合は、この画面に戻り、プロファイルを選択して**構成を適用**をクリックします。


<blockquote>
プロファイルを変更した後は、AIクライアントでTealium Configuration MCPの接続を切断して再接続し、新しいチャットを開始してください。以前のセッションは無効になります。
</blockquote>


## ステップ4: AIクライアントを接続する（管理者およびユーザー）

AIクライアントをTealium Configuration MCPに接続します。クライアントの指示に従ってください。

### Claude Desktopを接続する

**開始する前に**

開始する前に以下のことを確認してください：

* Claude Pro、Max、Team、またはEnterpriseプランを持っています。無料プランではカスタムコネクタを追加することはできません。
* Claude Desktopがインストールされているか、[claude.ai](https://claude.ai)にアクセスできます。
* Tealium Configuration MCPがアカウントで有効になっています。アクセスをリクエストするには、[サポートに連絡してください](https://docs.tealium.com/support/)。

**コネクタを追加する**

1. [claude.ai](https://claude.ai)で管理者としてサインインします。
1. プロファイルアイコンをクリックし、**構成**を選択します。
1. **コネクタ**を選択します。
1. ページの一番下までスクロールし、**カスタムコネクタを追加**をクリックします。
1. 信頼できるサービスに接続する際の警告が表示された場合は、確認して続行します。
1. 次のコネクタの詳細を入力します：

   * **名前：** `Tealium Configuration MCP`
   * **リモートMCPサーバーURL：** `https://us-west-1.prod.developer.tealiumapis.com/2026-09/mcp/dcp`

1. **詳細構成**は空白のままにします。
1. **追加**をクリックします。コネクタがコネクタリストに表示されます。

![](https://docs.tealium.com/images/server-side/config-mcp-setup-add-connector.png)

**認証して接続する**

1. Claudeで**構成 > コネクタ**に移動します。
1. **Tealium Configuration MCP**の隣にある**接続**をクリックします。
1. [ステップ5: 認証する](#step-5-authenticate-user)でTealiumのサインイン手順を完了します。
1. 認証が完了すると、コネクタのステータスが接続済みと表示されます。

   ![](https://docs.tealium.com/images/server-side/config-mcp-setup-connected.png)

いつでもコネクタを切断するには、Claudeで**構成 > コネクタ**に移動し、**Tealium Configuration MCP**を見つけて**切断**を選択します。

**チャットでコネクタを有効にする**

1. Claudeで新しいチャットを開きます。
1. メッセージコンポーザーで**+**アイコンをクリックします。
1. **Tealium Configuration MCP**をオンに切り替えます。

![](https://docs.tealium.com/images/server-side/config-mcp-setup-enable-in-chat.png)

### Claude Code CLIを接続する

**開始する前に**

開始する前に以下のことを確認してください：

* Claude Codeがインストールされ、認証されています。
* 任意のプロジェクトディレクトリでターミナルが開いています。空のディレクトリを含む任意のディレクトリで動作します。

**Tealium Configuration MCPを登録する**

Claudeセッションを開始する前に、ターミナルで次のコマンドを実行します：

```bash
claude mcp add --transport http tealium-configuration-mcp https://us-west-1.prod.developer.tealiumapis.com/2026-09/mcp/dcp
```

サーバーが追加されたことを確認します：

```bash
claude mcp list
```

**認証して接続する**

1. `claude`を実行してClaudeセッションを開始します。
1. `/mcp`を実行して構成されたMCPサーバーをリストします。
1. `tealium-configuration-mcp`を見つけます。**認証が必要**と表示されます。
1. **認証**アクションを選択します。Claude CodeがデフォルトのブラウザでTealiumのログイン画面を開きます。
1. [ステップ5: 認証する](#step-5-authenticate-user)でTealiumのサインイン手順を完了します。
1. 認証が完了すると、サーバーのステータスが接続済みに更新されます。

いつでも切断するには、Claudeセッション内で`/mcp`に移動し、`tealium-configuration-mcp`を見つけて**無効にする**を選択します。
## ステップ5: 認証 (ユーザー)

Tealium構成MCP接続をアクティブにするために、Tealiumサインインチャレンジを完了してください。この手順は、Claude DesktopとClaude Code CLIの両方に適用されます。

1. Tealiumのサインインウィンドウが開きます。アカウント名を入力して**サインイン**をクリックします。組織がSSOを使用している場合は、SSOアカウント名を入力します。わからない場合は、アカウント管理者に連絡してください。

   ![](https://docs.tealium.com/images/server-side/config-mcp-setup-signin-account.png)

1. Tealiumの認証情報でサインインします：
   * **SSOなし：** ユーザー名またはメールアドレスとパスワードを入力し、**サインイン**をクリックします。

     ![](https://docs.tealium.com/images/server-side/config-mcp-setup-signin-credentials.png)

   * **SSOあり：** 身元確認プロバイダーがサインインページにリダイレクトします。SSO認証情報を入力します。

1. プロンプトが表示されたら、Tealiumプロファイルへのアクセスを許可するために**はい**を選択します。

   ![](https://docs.tealium.com/images/server-side/config-mcp-setup-grant-access.png)

1. ウィンドウが閉じた後、AIクライアントに戻ります。コネクタのステータスが接続済みと表示されます。

"アカウントは認証されましたが、Tealium MCP Early Accessが接続時にエラーを返しました"というエラーが表示された場合は、サポートに連絡する前にTealium UIで以下を確認してください：

* AI構成のアカウントとプロファイルで**MCPサーバー**トグルが**オン**に構成されていること。
* Tealium構成MCPアクセス用にユーザー権限が正しく構成されていること（[ステップ2](#step-2-enable-tealium-configuration-mcp-access-delegation-admin)を参照）。
* **ユーザー構成の編集/表示**の下でデフォルトのアカウントとプロファイルが選択されていること（[ステップ3](#step-3-select-a-profile-in-user-preferences-user)を参照）。

コネクタは現在アクティブです。セッションの実行に関する詳細は、[Tealium構成MCPの管理](https://docs.tealium.com/manage-config-mcp/)を参照してください。