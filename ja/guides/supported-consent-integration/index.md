---
title: 同意統合
description: このガイドでは、Tealium iQタグ管理システムとサポートされているベンダー統合を構成し、ユーザーの同意が得られた場合にのみタグが発火するように構成を確認する方法について説明します。
url: https://docs.tealium.com/ja/guides/supported-consent-integration/
---
このガイドでは、Tealium iQタグ管理システムとOneTrust同意統合を使用しますが、この構成は[サポートされているベンダー統合](https://docs.tealium.com/vendor-specific-configuration/)のいずれにも適用できます。このガイドの終わりまでに、OneTrustまたは他のサポートされている同意管理プラットフォーム（CMP）を選択し、Tealium iQで関連する施行を統合して、ユーザーの構成を尊重するタグが正しく機能するように構成します。

![](https://docs.tealium.com/images/guides/consent-integration-guide.png)

Tealium iQでOneTrust同意統合を構成するには、以下の手順を完了します：

1. [CMPスクリプトをロードする](#load-the-cmp-script)
1. [統合を構成する](#step-1-configure-the-integration)
1. [施行ルールを構成する](#step-2-set-enforcement-rules)
1. [公開場所を選択する](#step-3-select-publish-location)
1. [目的グループを作成する](#step-4-create-a-purpose-group)
1. [目的グループを編集する](#step-5-edit-purpose-group)
1. [Tealium iQを目的に割り当てる](#step-4-assign-tealium-iq-to-a-purpose)
1. [タグを目的にマッピングする](#step-4-map-tags-to-purposes)
1. [構成を公開する](#step-4-publish-the-configuration)

さらに、以下の手順で構成を検証およびトラブルシューティングします：

1. [データレイヤーをチェックする](#check-the-data-layer)
1. [ブラウザコンソールから同意統合構成を検証する](#verify-your-consent-integration-setup-from-the-browser-console)
1. [追加情報を表示するためにデバッグモードを使用する](#use-the-debug-mode-to-view-additional-information)

## 要件

同意統合を作成するには、以下が必要です：

* Tealium iQタグ管理
* クライアント側の同意統合

統合を構成するには、以下のベンダー固有の情報が必要です：

* ベンダーID：同意統合がページ上のCMPを識別するために使用されます。
* 構成された同意カテゴリ：同意統合は、これらの各カテゴリを目的として参照し、1つのCMPからの目的の集合を目的グループと呼びます。

この情報は、すべてのトラッキングを受け入れた後に直接ウェブページから取得できます。それを取得する方法の詳細については、[サポートされているベンダー統合](https://docs.tealium.com/vendor-specific-configuration/#how-it-works)を参照してください。

## CMPスクリプトをロードする

まず、**Pre Loader**または**DOM Ready**拡張機能を使用して、OneTrust CMPスクリプトをウェブサイトに注入します。この構成には、CMPプロバイダーから取得した構成済みのCMPスクリプトが必要です。この例では、OneTrustコンソールから取得したOneTrust CMPスクリプトを使用します。

1. **タグ管理 > 拡張機能**に移動します。
1. **+ 拡張機能を追加 > 上級**をクリックします。
1. **JavaScriptコード**拡張機能を追加します。
1. 拡張機能を識別するための**タイトル**を入力します。
1. **スコープ**の下で、**Pre Loader**または**DOM Ready拡張機能**を選択します。
1. **構成**の下で、OneTrust CMPスクリプトを貼り付けます：
    ```javascript
    // ベンダーCMPスクリプトをロードする関数を定義する
    window.addCmp = function () {
      var domainId = '12345678-1234-1234-1234-1234567890ab-test';

      var head = document.getElementsByTagName('head')[0];
      var script = document.createElement('script');
      script.type = 'text/javascript';
      script.src = 'https://cdn.cookielaw.org/scripttemplates/otSDKStub.js';
      script.setAttribute("data-domain-script", domainId);
      // script.setAttribute("data-domain-script", b['OTDomainGUID']);
      script.async = true;
      head.appendChild(script);    
    };

    // スクリプトをロードするためにすぐに'addCmp'関数を呼び出す
    window.addCmp();
    ```

次に、ユーザーが提供する同意に基づいてのみタグが発火するように統合を構成します。

## Tealium iQでのOneTrust同意統合を構成する

### ステップ1: 統合を構成する

1. **タグ管理 > 同意統合**セクションに移動します。
1. **統合を追加**をクリックします。
1. 統合の目的を明確に識別する名前を入力します。
1. ベンダーのドロップダウンリストから**OneTrust**を選択します。
1. OneTrustコンソールから取得した**ベンダーID**を入力します。
1. OneTrustの標準目的から自動的に標準目的を作成する場合は、**OneTrust Default Categoriesで新しいPurpose Groupを作成**を選択します。
1. **次へ**をクリックします。

### ステップ2: 施行ルールを構成する

**施行ルール**は、CMPによってキャプチャされた同意信号が施行されるタイミングを決定します。同意が常に正しく施行されるようにするために、ウェブサイトの各ページビューまたはイベントは、重複なしに1つの同意統合または例外をトリガーする必要があります。

1. ドロップダウンリストから**すべてのページとイベント**を選択します。
1. **次へ**をクリックします。

### ステップ3: 公開場所を選択する

**公開場所**画面では、統合が適用される環境を選択できます。最初にテスト環境に公開してからライブにすることをお勧めします。この例では、すべての環境に公開します。

1. **Dev, QA**, および **Prod** 環境を選択します。
1. **次へ**をクリックします。

### ステップ4: 目的グループを選択する

1. **目的グループ**画面で、ドロップダウンリストから**OneTrust Default**を選択します。
1. **保存**をクリックして同意統合を保存します。

### ステップ5: 目的グループを編集する

同意統合を保存した後、Tealium iQを目的に割り当て、タグを目的にマッピングするために目的グループを編集する必要があります。

目的グループを編集するには：

1. **同意統合**画面で、**目的グループ**タブをクリックします。
1. [ステップ1](#step-1-configure-the-integration)で作成した**OneTrust Default**目的グループを選択します。

### ステップ6: Tealium iQを目的に割り当てる

**Tealium iQ目的**画面では、Tealium iQを特定の目的にマッピングできます。これは、すべてのタグ操作を管理するために重要です。同意が必要であり、ユーザーがその目的に同意しない場合、Tealium iQはロードされず、結果としてタグは機能しません。

1. **Tealium iQ目的**タブをクリックします。
1. Tealium iQが常にロードされるように、**厳密に必要**な目的にTealium iQを割り当てます。

### ステップ7: タグを目的にマッピングする

**タグマッピング**画面では、ユーザーの同意選択に基づいて正しいタグが発火するように、タグを特定の目的に割り当てます。すべてのタグに目的を割り当てることが重要です。目的が割り当てられていないタグは発火しません。この画面では、同じイベント内でユーザーの同意が更新された場合にタグを再発火させることも構成できます。

1. **タグマッピング**タブをクリックします。
1. 各タグを適切な目的に割り当てます。
1. Tealium Collectタグなどのタグを同意が同じイベント内で更新された場合に再発火させたい場合は、タグの再発火を有効にします。
1. **保存**をクリックして目的グループを保存します。

### ステップ8: 構成を公開する

Tealium iQプロファイルを保存して公開し、CMPとの同意統合を使用を開始します。

これで、Tealium iQ内のOneTrust統合が正常に構成されました。この構成により、CMPで構成した構成に従って、すべてのページとイベントでユーザーの同意が得られた場合にのみタグが発火します。選択した環境で統合が正しく機能していることを確認するために、テストを行ってください。テスト方法についての詳細は、以下のテストとトラブルシューティングを参照してください。

## テストとトラブルシューティング

同意統合を構成したので、それが正常に機能しているか確認しましょう。このセクションでは、Tealium iQのOneTrust同意統合が正しく機能しているかを検証します。データレイヤーで同意状態をチェックし、ブラウザコンソールを使用して構成を検証します。

始める前に、以下を確認してください：

* Tealium iQとOneTrust同意統合がウェブサイト上で稼働しています。
* ブラウザの開発者コンソールにアクセスできます。
### データレイヤーを確認する

タグが発火する直前に、同意状態がデータレイヤーに追加されます。同意状態が適切にロードされているかを確認するために、`tci`プレフィックスを持つTealium同意変数を確認してください：

* `tci.consent_type`: 同意のタイプ（暗黙的または明示的）を識別します。
* `tci.purposes_with_consent_all`: 同意された全ての目的を含む配列です。
* `tci.purposes_with_consent_unprocessed`: 未処理の同意された目的を全て含みます。
* `tci.purposes_with_consent_processed`: 処理済みの同意された目的を全て含みます。

未処理および処理済みの変数は、EventStreamおよびAudienceStreamコネクタが同じイベントに対して複数回発火しないようにロジックを構築するために使用できます。

### 同意統合セットアップを確認する

同意統合がアクティブになった後、ブラウザコンソールから直接現在の同意統合の詳細にアクセスできます。`tealiumCmpIntegration`ウィンドウスコープオブジェクト内には、統合を管理および操作するための[関数](https://docs.tealium.com/custom-cmp-integrations/#integration-functions)が用意されています。

ウェブページから関連情報を取得するには、以下の手順に従ってください：

1. CMPが実装されているウェブサイトを訪れます。
1. すべてのトラッキングを受け入れます。
1. 開発者ツールのJavaScriptコンソールを開きます。
1. 次のスニペットをブラウザコンソールに貼り付けます。

    ```
    var outputString = `${tealiumCmpIntegration.cmpName} - ${tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model

    Checks:
    - vendor id:            ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
    - well-formed decision: ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - explicit decision:    ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - consented purposes:   ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()).sort(),null, 8)}
    `
    console.log(outputString)
    ```

#### スクリプトの出力を分析する

* **同意前**：

    以下は、同意が与えられる前のスクリプトの出力の例です。

    ![](https://docs.tealium.com/images/guides/consent-integration-before-consent.png)

    示されているように、CMPはその運用モードで検出されました。この場合、ユーザーからの明示的な同意は提供されていないため、`C0001`（必要）目的のみが許可されています。

* **同意後**：

    いくつかのカテゴリに同意しましょう。ページをリロードした後、再びCMPとその運用モードを確認できます。今回は明示的な同意が与えられていますが、`C0001`（必要）および`C0002`（パフォーマンス）目的のみが許可されています。
    
    ![](https://docs.tealium.com/images/guides/consent-integration-after-consent.png)

### デバッグモードを使用して追加情報を表示する

同意統合はTealiumの[デバッグモード](https://docs.tealium.com/ja/platforms/javascript/debugging/)にも追加情報を提供します。

1. [デバッグモード](https://docs.tealium.com/ja/platforms/javascript/debugging/)を有効にして、同意統合情報を表示します。
1. デバッグモード出力で同意統合情報を簡単に見つけるために、正規表現 `/SENDING|****/` を使用して出力をフィルタリングし、タグ送信と同意統合通知のみを表示します。

デバッグモードフィルタを使用することで、以下のことが可能になります：

* 同意選択に基づいたタグの動作を迅速に確認：フィルタは、ユーザーの同意に応じて送信またはブロックされるタグを強調表示し、構成がユーザーの好みを尊重していることを保証します。
* 潜在的な構成問題を簡単に特定：関連するログエントリに焦点を当てることで、目的マッピングの欠落や意図しないタグブロッキングなどの問題を見つけ出し、効率的に解決できます。

デバッグモードフィルタを使用したいくつかのシナリオを以下に示します。

#### シナリオ1: CMPスクリプトのブロック

![](https://docs.tealium.com/images/guides/consent-integration-blocked-cmp-script.png)
このシナリオでは、CMPスクリプトがブロックされているか利用できません。デバッグ出力に示されているように、同意統合が有効であるため、Tealium iQのロードが防がれています。ページビューイベントはキューに入れられますが、CMPスクリプトがロードされるまで他のアクションは発生しません。

#### シナリオ2: クッキーが受け入れられる前のオプトインモードのCMP

![](https://docs.tealium.com/images/guides/consent-integration-opt-in-mode-before-cookies.png)

ここでは、CMPがオプトインモードで運用されており、ユーザーはまだ明示的な同意を提供していません。ユーザーがクッキーを受け入れる前に、同意統合は`Necessary`にマッピングされた目的のみの暗黙的な同意を検出し、他の目的のロードを防ぎます。オプトインモードでは、システムは明示的な同意決定を継続的にポーリングします。

#### シナリオ3: クッキーが受け入れられた後のオプトインモードのCMP

![](https://docs.tealium.com/images/guides/consent-integration-opt-in-mode-after-cookies.png)

このシナリオでは、ユーザーがクッキーに同意した後、同意統合は明示的な同意を検出し、新たに同意された目的を確認しますが、暗黙的な同意の下で既に処理されたものは除外します。その後、新たに同意された目的にマッピングされたタグをキューに入れて発火します。目的にマッピングされていないタグはロードがブロックされたままです。

詳細については、[同意統合の検証とデバッグ](https://docs.tealium.com/validate-and-debug-consent-integrations/)を参照してください。