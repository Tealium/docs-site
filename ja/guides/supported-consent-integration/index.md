---
title: 同意連携
description: このガイドでは、Tealium iQタグ管理システムでサポート対象ベンダーとの連携を構成し、ユーザーが同意した場合にのみタグが配信されることを確認する方法について説明します。
url: https://docs.tealium.com/ja/guides/supported-consent-integration/
---
このガイドでは、OneTrustとTealium iQタグ管理システムの同意連携を使用しますが、この構成はどの[サポート対象ベンダー連携](https://docs.tealium.com/vendor-specific-configuration/)にも適用できます。このガイドを完了すると、OneTrustまたは任意のサポート対象同意管理プラットフォーム（CMP）とTealium iQの関連する適用ルールを正常に連携し、タグがユーザーの構成を尊重するように構成できます。

![](https://docs.tealium.com/images/guides/consent-integration-guide.png)

Tealium iQでOneTrust同意連携を構成するには、次の手順を実行します。

1. [CMPスクリプトを読み込む](#load-the-cmp-script)
1. [連携を構成する](#step-1-configure-the-integration)
1. [適用ルールを構成する](#step-2-set-enforcement-rules)
1. [パブリッシュ先を選択する](#step-3-select-publish-location)
1. [目的グループを作成する](#step-4-create-a-purpose-group)
1. [目的グループを編集する](#step-5-edit-purpose-group)
1. [Tealium iQを目的に割り当てる](#step-4-assign-tealium-iq-to-a-purpose)
1. [タグを目的にマッピングする](#step-4-map-tags-to-purposes)
1. [構成をパブリッシュする](#step-4-publish-the-configuration)

さらに、次の手順で構成を検証し、トラブルシューティングを行います。

1. [データレイヤーを確認する](#check-the-data-layer)
1. [ブラウザーコンソールから同意連携の構成を検証する](#verify-your-consent-integration-setup-from-the-browser-console)
1. [デバッグモードを使用して追加情報を表示する](#use-the-debug-mode-to-view-additional-information)

## 要件

同意連携を作成するには、次のものが必要です。

* Tealium iQタグ管理
* クライアント側の同意連携

連携を構成するには、ベンダー固有の次の情報が必要です。

* ベンダーID：ページ上のCMPを識別するために同意連携で使用されます。
* 構成済みの同意カテゴリー：同意連携では、各カテゴリーを目的と呼び、1つのCMPに含まれる目的の集合を目的グループと呼びます。

すべてのトラッキングを許可した後、Webページからこの情報を直接取得できます。取得方法の詳細については、[サポート対象ベンダー連携](https://docs.tealium.com/vendor-specific-configuration/#how-it-works)を参照してください。

## CMPスクリプトを読み込む

まず、**Pre Loader**または**DOM Ready**拡張機能を使用して、OneTrust CMPスクリプトをWebサイトに挿入します。この構成には、CMPプロバイダーから取得できる構成済みのCMPスクリプトが必要です。この例では、OneTrustコンソールから取得したOneTrust CMPスクリプトを使用します。

1. **Tag Management > Extensions**に移動します。
1. **+ Add Extension > Advanced**をクリックします。
1. **Javascript Code**拡張機能を追加します。
1. 拡張機能を識別するための**Title**を入力します。
1. **Scope**で、**Pre Loader**または**DOM Ready Extensions**を選択します。
1. **Configuration**に、OneTrust CMPスクリプトを貼り付けます。
    ```javascript
    // Define a function to load the Vendor CMP script
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

    // Immediately call the 'addCmp' function to load the script
    window.addCmp();
    ```

次に、ユーザーが提供した同意に基づいてのみタグが配信されるように、連携を構成します。

## Tealium iQでOneTrust同意連携を構成する

### ステップ1：連携を構成する

1. **Tag Management > Consent Integrations**セクションに移動します。
1. **Add Integration**をクリックします。
1. 用途が明確に分かる連携名を入力します。
1. ベンダーのドロップダウンリストから**OneTrust**を選択します。
1. OneTrustコンソールから取得した**Vendor ID**を入力します。
1. OneTrustの標準目的を自動的に作成するには、**Create new Purpose Group with OneTrust Default Categories**を選択します。
1. **Next**をクリックします。

### ステップ2：適用ルールを構成する

**Enforcement Rules**は、CMPによって取得された同意シグナルをいつ適用するかを決定します。同意が常に正しく適用されるように、Webサイト上の各ページビューまたはイベントでは、重複することなく、1つの同意連携または適用除外のみがトリガーされるようにしてください。

1. この例では1つの連携のみを構成するため、ドロップダウンリストから**All Pages and Events**を選択します。
1. **Next**をクリックします。

### ステップ3：パブリッシュ先を選択する

**Publish Location**画面では、連携を適用する環境を選択できます。本番公開する前に、まずテスト環境にパブリッシュすることをお勧めします。この例では、すべての環境にパブリッシュします。

1. **Dev、QA**、および**Prod**環境を選択します。
1. **Next**をクリックします。

### ステップ4：目的グループを選択する

1. **Purpose Group**画面で、ドロップダウンリストから**OneTrust Default**を選択します。
1. **Save**をクリックして、同意連携を保存します。

### ステップ5：目的グループを編集する

同意連携を保存した後、Tealium iQを目的に割り当て、タグを目的にマッピングするために目的グループを編集する必要があります。

目的グループを編集するには、次の手順を実行します。

1. **Consent Integrations**画面で、**Purpose Groups**タブをクリックします。
1. [ステップ1](#step-1-configure-the-integration)で作成した**OneTrust Default**目的グループを選択します。

### ステップ6：Tealium iQを目的に割り当てる

**Tealium iQ Purpose**画面では、Tealium iQを特定の目的にマッピングできます。これは、すべてのタグ操作を管理するうえで重要です。同意が必要な場合に、ユーザーがその目的に同意しなければ、Tealium iQは読み込まれず、その結果、どのタグも機能しません。

1. **Tealium iQ Purpose**タブをクリックします。
1. Tealium iQが常に読み込まれるように、ユーザーがオプトアウトできない**Strictly Necessary**目的にTealium iQを割り当てます。

### ステップ7：タグを目的にマッピングする

**Map Tags**画面では、タグを特定の目的に割り当て、ユーザーの同意の選択に基づいて適切なタグが配信されるようにします。目的が割り当てられていないタグは配信されないため、すべてのタグに目的を割り当てることが重要です。この画面では、タグの再配信も構成できます。これにより、同じイベント内でユーザーの同意が更新された場合に、タグを再度配信できます。

1. **Map Tags**タブをクリックします。
1. 各タグを適切な目的に割り当てます。
1. Tealium Collectタグなどのタグを、同じイベント内で同意が更新されたときに再度配信する場合は、タグの再配信を有効にします。
1. **Save**をクリックして、目的グループを保存します。

### ステップ8：構成をパブリッシュする

CMPで同意連携の使用を開始するには、Tealium iQプロファイルを保存してパブリッシュします。

これで、Tealium iQ内でOneTrust連携が正常に構成されました。この構成により、CMPで構成した内容に従って、すべてのページおよびイベントでユーザーの同意が得られた場合にのみタグが配信されます。選択した環境でテストし、連携が正しく機能していることを確認してください。テスト方法の詳細については、以下のテストおよびトラブルシューティングを参照してください。

## テストとトラブルシューティング

同意連携の構成が完了したので、正しく機能していることを確認します。このセクションでは、Tealium iQのOneTrust同意連携が正しく機能していることを検証します。データレイヤーで同意の状態を確認し、ブラウザーコンソールを使用して構成を検証します。

開始する前に、次の点を確認してください。

* Tealium iQとOneTrust同意連携がWebサイトで稼働していること。
* ブラウザーの開発者コンソールにアクセスできること。
### データレイヤーを確認する

タグが配信される直前に、同意状態がデータレイヤーへ追加されます。同意状態が正しく読み込まれていることを確認するには、`tci` プレフィックスが付いた以下の Tealium 同意変数を確認します。

* `tci.consent_type`: 同意タイプ（暗黙的または明示的）を識別します。
* `tci.purposes_with_consent_all`: 同意済みのすべての目的を含む配列です。
* `tci.purposes_with_consent_unprocessed`: 未処理の同意済み目的をすべて含みます。
* `tci.purposes_with_consent_processed`: 処理済みの同意済み目的をすべて含みます。

未処理および処理済みの変数を使用してロジックを構築することで、EventStream と AudienceStream のコネクタが同じイベントに対して複数回実行されるのを防止できます。

### 同意統合の構成を確認する

同意統合が有効になると、現在の同意統合の詳細にブラウザーコンソールから直接アクセスできます。統合を管理および操作するための一連の[関数](https://docs.tealium.com/custom-cmp-integrations/#integration-functions)が、ウィンドウスコープの `tealiumCmpIntegration` オブジェクト内で使用できます。

Web ページから関連情報を取得するには、次の手順を実行します。

1. CMP が実装されている Web サイトにアクセスします。
1. すべてのトラッキングを許可します。
1. 開発者ツールの JavaScript コンソールを開きます。
1. 次のスニペットをブラウザーコンソールに貼り付けます。

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

* **同意前**:

    次は、同意が付与される前のスクリプト出力の例です。

    ![](https://docs.tealium.com/images/guides/consent-integration-before-consent.png)

    図に示すように、CMP とその動作モードが検出されています。この例では、ユーザーから明示的な同意が得られていないため、`C0001`（必須）の目的のみが許可されています。

* **同意後**:

    次に、いくつかのカテゴリに同意してみます。ページを再読み込みすると、CMP とその動作モードを再度確認できます。今回は明示的な同意が付与されていますが、許可されている目的は `C0001`（必須）と `C0002`（パフォーマンス）のみです。
    
    ![](https://docs.tealium.com/images/guides/consent-integration-after-consent.png)

### デバッグモードを使用して追加情報を表示する

同意統合では、Tealium の[デバッグモード](https://docs.tealium.com/ja/platforms/javascript/debugging/)にも追加情報が表示されます。

1. [デバッグモード](https://docs.tealium.com/ja/platforms/javascript/debugging/)を有効にして、同意統合に関する追加情報を表示します。
1. デバッグモードの出力から同意統合の情報を見つけやすくするため、正規表現 `/SENDING|****/` を使用して出力をフィルタリングし、タグ送信と同意統合の通知のみを表示します。

デバッグモードのフィルターを使用すると、同意に関連する重要なメッセージを分離でき、次のことが可能になります。

* 同意の選択に基づくタグの動作をすばやく確認する: ユーザーの同意に応じて、送信またはブロックされたタグがフィルターによって強調表示されるため、構成がユーザーの選択を尊重していることを確認できます。
* 潜在的な構成上の問題を簡単に特定する: 関連するログエントリに絞り込むことで、目的のマッピング漏れや意図しないタグのブロックなどの問題を特定し、より効率的に解決できます。

デバッグモードのフィルターを使用すると、次のようなシナリオが発生する場合があります。

#### シナリオ 1: CMP スクリプトがブロックされている

![](https://docs.tealium.com/images/guides/consent-integration-blocked-cmp-script.png)
このシナリオでは、CMP スクリプトがブロックされているか、使用できません。デバッグ出力に示すように、有効な同意統合が存在するため、同意統合によって Tealium iQ の読み込みが停止されています。ページビューイベントはキューに追加されますが、CMP スクリプトが読み込まれるまで、それ以上の処理は行われません。

#### シナリオ 2: Cookie の許可前に CMP がオプトインモードで動作している

![](https://docs.tealium.com/images/guides/consent-integration-opt-in-mode-before-cookies.png)

この例では、CMP はオプトインモードで動作しており、ユーザーはまだ明示的な同意を行っていません。ユーザーが Cookie を許可する前は、同意統合によって `Necessary` にマッピングされた目的に対する暗黙的な同意のみが検出され、その他の目的は読み込まれません。オプトインモードで動作しているため、システムは明示的な同意の決定を継続してポーリングします。

#### シナリオ 3: Cookie の許可後に CMP がオプトインモードで動作している

![](https://docs.tealium.com/images/guides/consent-integration-opt-in-mode-after-cookies.png)

このシナリオでは、ユーザーが Cookie に同意すると、同意統合によって明示的な同意が検出され、新たに同意された目的が確認されます。その際、暗黙的な同意ですでに処理された目的は除外されます。次に、新たに同意された目的にマッピングされたタグが確認され、配信用のキューに追加されます。どの目的にもマッピングされていないタグは、引き続き読み込みがブロックされることに注意してください。

詳細については、[同意統合の検証とデバッグ](https://docs.tealium.com/validate-and-debug-consent-integrations/)を参照してください。